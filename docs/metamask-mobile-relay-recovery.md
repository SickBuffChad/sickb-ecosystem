# MetaMask Mobile: background network restrictions and relay recovery

**SickB engineering case study · November 25, 2026**

**Status:** Android workaround verified on one physical device; candidate upstream repair demonstrated in a controlled harness; no production wallet or bridge code changed.

## Why this matters

SickB is an independently operated Arbitrum Orbit L3 ecosystem. Its Baht Bus Bridge connects Ethereum directly to SickB Chain (5016). A mobile bridge journey may require a network switch, token spending approval and a subsequent bridge transaction.

During Product Zero testing, MetaMask Mobile would sometimes open its normal wallet home screen instead of displaying an outstanding confirmation. Ethereum-to-SickB deposits were particularly affected after approval. Network switching could also trigger the symptom in either direction. Waiting or returning to the existing MetaMask activity did not reliably help; removing MetaMask from Recents and reopening it consistently surfaced the outstanding request in the founder's tests.

This was a wallet communication problem observed before signing the affected transaction, not evidence of a failed onchain bridge settlement.

Rather than modify the bridge's transaction sequence, add arbitrary delays or automatically resubmit transactions, we investigated the mobile wallet transport and the Android lifecycle.

## Test environment

| Component | Version |
| --- | --- |
| Physical Android device | CPH2749 |
| Android | 16 (API 36) |
| MetaMask Mobile | 8.21.0 |
| Legacy MetaMask SDK used by SickB | 0.33.1 |
| Network | Ethereum mainnet (1) / SickB Chain (5016) |
| Investigation | Source review, local fault-injection harness, read-only ADB diagnostics, founder-operated device testing |

## Finding 1: the relay can reconnect without recovering channel membership

The legacy MetaMask communication layer uses a relay channel between the dApp and wallet. In the inspected wallet-side implementation, a transport reconnection can occur without the wallet rejoining the existing channel. Local connection status can continue to indicate readiness even when requests cannot reach the wallet through that channel.

SickB's local reproduction harness used the actual MetaMask communication library and a local model of the publicly available relay behavior. It deliberately interrupted the transport and examined the subsequent request and response delivery.

| Harness scenario | Reported result |
| --- | --- |
| Existing wallet-side behavior after transport interruption | Failure reproduced in 16 of 16 runs |
| Candidate wallet-side channel-rejoin repair | 32 of 32 checks passed in each of three runs |
| Relay-only connection-state recovery experiment | Duplicate request delivery observed in 13 of 15 runs |

The candidate upstream repair queues the existing channel-join operation when the wallet transport is about to reconnect. In the harness this recovered delivery and the response path without resubmitting the transaction from the dApp.

These results establish a reproducible failure mechanism under the harness conditions. The deployed relay's exact configuration is unknown. Successful rejoin acknowledgement and possible duplicate delivery when replacing connections remain issues to address before considering the candidate patch production-ready.

## Finding 2: Android applies a real background network restriction

Read-only ADB diagnostics on November 25 captured seven transitions to an effective `APP_BACKGROUND` network block while MetaMask's process remained alive. The block was first observed approximately 6–8 seconds after the wallet activity stopped, using policy snapshots sampled roughly every three seconds. Foreground return removed the effective block.

The observations occurred while the phone was charging and without observed Doze entry.

One representative cycle:

| PC local time (November 25, Pacific time) | Observation |
| --- | --- |
| 17:10:37 | MetaMask stops; SickB resumes. Effective block: NONE. |
| 17:10:44 | Same wallet process; effective block: APP_BACKGROUND. |
| 17:11:02 | MetaMask receives a new intent and returns to foreground. |
| 17:11:03 | Same wallet process; effective block: NONE. |

This is a sanitized summary of the physical-device capture, not a packet capture or a relay server trace. The recording did not retain an explicit socket disconnect reason or transaction markers, so it cannot conclusively associate this particular cycle with a failed bridge transaction.

The background restriction is a plausible physical trigger for the transport defect reproduced in the harness. Rapid requests on SickB may avoid the restriction window more often than sequential requests separated by Ethereum receipt confirmation. That explanation is consistent with the observed asymmetry, not a measured causal proof for every failure.

## Verified Android workaround

On the test phone, enabling unrestricted background battery usage for MetaMask removed the effective background network block.

1. Open Android **Settings → Apps → MetaMask → Battery** (menu names vary by manufacturer).
2. Allow unrestricted background activity or select **Unrestricted**, where available.
3. Return to SickB and use the normal bridge workflow.

The follow-up ADB capture retained the following sanitized policy fields, including after the wallet UID reached idle at approximately 60 seconds:

```text
uid.allowed=POWER_SAVE_ALLOWLIST|POWER_SAVE_EXCEPT_IDLE_ALLOWLIST
uid.effective=NONE
```

The underlying `APP_BACKGROUND` reason could still be listed; the exemption removed its effective application.

The founder then completed Ethereum-to-SickB and SickB-to-Ethereum bridging, including a network switch between the journeys, without manually restarting MetaMask.

No SickB production connector, bridge contract, bridge bot, Vault or transaction-sequencing changes were required.

### Post-workaround bridge settlement: matched mainnet receipts

The founder identified **the final two transactions in the follow-up set** as the physical-device bridge journeys performed **after** changing MetaMask's Android background battery setting. The Ethereum and SickB transactions were subsequently matched using their **exact bridge IDs**. These are **November 25, 2026 Pacific time (November 26 UTC)** observations; they are not the complete set of five L3 events discovered in the same later activity query.

| Journey | Asset amount | Source block inclusion (UTC, November 26) | Destination block inclusion (UTC, November 26) | Inclusion-to-inclusion time |
| --- | ---: | --- | --- | ---: |
| Ethereum → SickB | **9,351.5625 SICKB** | Ethereum block **26,496,216** · 01:55:11 | SickB block **352,983** · 01:55:33 | **22 seconds** |
| SickB → Ethereum | **997,500 SICKB net** | SickB block **352,986** · 01:56:48 | Ethereum block **26,496,229** · 01:57:47 | **59 seconds** |

**Exact onchain references**

- **Ethereum → SickB deposit ID:** `0x6dd022dc6fa4b10fc7239475d02a6c39b7911a19ff7063e060d6fc2d19618f65`; [Ethereum source transaction](https://etherscan.io/tx/0xb987f458c26969477db3945528aec2a04d202e3963dda364454aa9762d5d30fa) `0xb987f458c26969477db3945528aec2a04d202e3963dda364454aa9762d5d30fa`; SickB mint transaction `0xd110aa52dab583a0a8e66f18ed9ffd008197370dcd687f7fce7c556aeabe5ca6`.
- **SickB → Ethereum withdrawal ID:** `0x2bbca1c3d140a03b26a53770538652c5f74aa3dbfa2a9200ccac080d16b3a5c5`; SickB initiation transaction `0x0d99d8b3c9b81a74bc87b605222092bf8282dd8e4848ca4ed74b079715c4a625`; [Ethereum release transaction](https://etherscan.io/tx/0xfbc36d2c47f1a70c7c0acef48cb8bf92bbf2ee6f1cf1fedf932656107d5c57f2) `0xfbc36d2c47f1a70c7c0acef48cb8bf92bbf2ee6f1cf1fedf932656107d5c57f2`.

**Verification scope:** a read-only H#3 query selected five later L3 bridge events, then matched all five to successful Ethereum lockbox deposit/release receipts, using exact IDs and matching token/amount (and recipient where applicable), with canonical Ethereum block-hash checks. The L3 side came from the existing confirmed-activity indexer rather than an independent L3 receipt re-fetch in that matching run. **The founder specifically identified only the last two** as post-setting-change tests; the other three must not be labeled as such without separate confirmation.

These times are **source-chain transaction inclusion → destination-chain transaction inclusion**, **not** tap-to-completion times, wallet approval duration, MetaMask notification latency, or Ethereum consensus finality. The observation of successful wallet handoffs on the founder's test device is separate from the onchain timing. **Two selected observations cannot establish that the battery workaround accelerated bridge settlement or that these timings generalize to other devices.** The relevant matched-receipt ledger is also documented in the [bridge evidence appendix](../evidence/bridge-matched-transfers-2026-11-25.md#post-workaround-physical-device-follow-up-two-additional-transfers).

This setting may increase battery consumption. Change the MetaMask app setting only; do not disable device-wide power management. The setting can be reverted through Android Settings. This is a verified workaround for the tested device and software combination, not a guarantee for every Android model, wallet or iOS device.

If a confirmation is missing, do not initiate another transaction blindly. An outstanding request may still be pending or a transaction may already have been broadcast. Reconcile its status before submitting anything again.

## Engineering outcome and upstream opportunity

The workaround preserves the normal SickB user experience while leaving the underlying wallet recovery defect for an upstream fix. It does not repair the wallet's reconnection behavior or protect against every other transport interruption.

The broader lesson for mobile dApp developers is that a live wallet process, a connected transport and active relay-channel membership are different states. Connection recovery should re-establish the required application-level state and safely reconcile outstanding requests.

SickB has prepared an upstream issue draft, source-level investigation reports and a reproducible harness. A separately sanitized public reproduction package and formal upstream issue are planned; this case study is a public summary, not a claim that either has already been published or that MetaMask has accepted a patch.

## References and evidence scope

- [MetaMask Mobile v8.21.0](https://github.com/MetaMask/metamask-mobile/tree/v8.21.0)
- [MetaMask SDK repository](https://github.com/MetaMask/metamask-sdk)
- [Baht Bus Bridge architecture](baht-bus-bridge.md)
- [SickB Ecosystem](../README.md)

The results above are reported by SickB's engineering investigation. No independent security audit or universal mobile compatibility certification is claimed. Private production source, wallet identifiers, session credentials, encrypted deeplink contents and raw device logs are intentionally omitted.

**SickB Digital LLC · [sickb.io](https://sickb.io)**
