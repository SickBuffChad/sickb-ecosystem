# Baht Bus: matched cross-chain transaction evidence

**Observation date:** November 25, 2026 (UTC)  
**Networks:** Ethereum mainnet (chain 1) ↔ SickB Chain (Arbitrum Orbit AnyTrust L3, chain 5016)  
**Status:** Read-only sample of the five most recent L3 deposit mints and five most recent L3 withdrawal initiations in the inspected H#3 activity state; **not** a comprehensive historical dataset, third-party audit or a service-level guarantee.

## Result

| Direction | Matched | Inclusion-to-inclusion times | Median | Mean | Under 60 seconds |
| --- | ---: | --- | ---: | ---: | ---: |
| Ethereum → SickB | 5/5 | 70, 34, 34, 46, 45 s | **45 s** | 45.8 s | 4/5 |
| SickB → Ethereum | 5/5 | 42, 45, 88, 85, 34 s | **45 s** | 58.8 s | 3/5 |
| **Combined** | **10/10** | Range **34–88 s** | **45 s** | **52.3 s** | **7/10** |

**Definition:** for deposits, elapsed seconds = SickB mint block timestamp minus Ethereum lockbox deposit block timestamp. For withdrawals, elapsed seconds = Ethereum lockbox release block timestamp minus SickB withdrawal-initiation block timestamp. These measurements **exclude** time spent connecting a wallet, approving token spending, showing confirmation prompts, signing, or any time before the source transaction enters a block. They **do not** establish Ethereum proof-of-stake consensus finality.

The samples include founder-operated test transfers, including mobile wallet interaction testing. They are **not** a randomly selected representation of all users or a statistically justified November-wide performance estimate.

## Deposit evidence: Ethereum source → SickB destination

| Asset / amount minted | Bridge deposit ID | Ethereum lockbox deposit tx | Ethereum inclusion (UTC) | SickB mint tx | SickB inclusion (UTC) | Seconds |
| --- | --- | --- | --- | --- | --- | ---: |
| USDC · 4.987500 | `0x8d95a736a857dc85d1763bcddecd166340cf3c219d4b364dbae57a010f576d3e` | `0xdf1a6f8e2cab71fc5f82472a080ea36ddeef4454a5eb0eb0e577da202a2b3f4e` | 19:32:23 | `0xbe3fecb6c3e60f72c88acacdbefbce8c84fe775003314205b40ebc69b0d05204` | 19:33:33 | 70 |
| SICKB · 99,750.9975 | `0x5b0bc3a7c4e85bd8e7c2fdddc69eb28634bf08ba96cd7bdaf56b131ea7e7610e` | `0xad532c6a4344bbe9218689bf51835f4127db9d4d8239192d0608718b243fe7d4` | 19:19:59 | `0x669f213bcb322a204ee0c79497423bad7bb6ba36fea14c491d754989d13800be` | 19:20:33 | 34 |
| SICKB · 99,750 | `0x5ba8de237555b4ef6a150c5d0af78aec8d44aadcac1600d0685cdcc0c3d0753c` | `0xdb7c0bc849eb0249ef931bfb1ff51e06ac24a06e4ecb8e1ff592ce5d74071893` | 19:09:59 | `0x0bc1a4fcd66ac463341001d219534c628981880e4cbd9cd334522faaf4eb9466` | 19:10:33 | 34 |
| USDC · 3.897137 | `0xe5dfe84e1e47b212e42bb9134074f17c058320346a563c90eee38c47a553fb26` | `0xa435ed78bba8cd03356baab4db78f85f79cd2edd131f9f2427b20a154e0d0014` | 16:06:47 | `0xbc3ee37c2da23a6c076c032aeb0fa6c6b7d066a3beebfb71229e3ba3c5dc1b2e` | 16:07:33 | 46 |
| WETH · 0.09975 | `0x6298939376a3369e6f25dec1488295e23551eb213edc9364ef71c0c36dca7264` | `0x8cb2504d5df583f7c60f7498717cfcf86a32fd8dc0bc0fa00c2d2b615b1a1c45` | 03:04:47 | `0xc9c4dc3ea256d744ce90fec70ca7f56806c6ad77f7b7cfbb1bb1acb7ea9defe9` | 03:05:32 | 45 |

## Withdrawal evidence: SickB source → Ethereum destination

Amounts below are **net withdrawal/release amounts**, not necessarily gross input before a withdrawal fee.

| Asset / net amount released | Bridge withdrawal ID | SickB initiation tx | SickB inclusion (UTC) | Ethereum release tx | Ethereum inclusion (UTC) | Seconds |
| --- | --- | --- | --- | --- | --- | ---: |
| USDC · 4.987500 | `0x6e1ab3c6c6ae3e29adb0e5947ee125132d976d9e056c3200d06efdca4536269d` | `0x6b50fbb4f7c48f69ca423b317f6d36719b4cf00b1f6adb3b19101ea01f046905` | 19:24:05 | `0x640d3500878580197292c69601efd3914201941a434f4275611461bfe21be8c8` | 19:24:47 | 42 |
| SICKB · 99,750.9975 | `0xc788303ceb26b55eb33dfef6f71dabe7696bc826653576edb05903880c57be3a` | `0x18a16c56e26d1c556944985cf8de9bd7ec4e963721e03c4362e3f8ca82da5f22` | 19:13:02 | `0xa7f4d4c5d1587fed20fbd0723406098ba1040d98b6e68c27d7bac3649656db6e` | 19:13:47 | 45 |
| SICKB · 99,750 | `0xf1a20d7d18f460c6d3e069359a09bd7682686ad9920ba7831edeea9cdd18089e` | `0x9d9775d72e7f734c80e28ca998c024c2b2213d617349bf4fbb06f401a265b3dc` | 18:57:19 | `0x49b98a7a8dff5dbfd62b2e790743e4f418a44bd7787312e69f85c676bcc723b0` | 18:58:47 | 88 |
| WETH · 0.09975 | `0x6d5cf75738a5c90e77ac06e9adab7750fe76905637d3f611c3c6ea66c41e8d30` | `0x5c4f2182af63e9a3389ffc544d9ed1b5932a17e1e69cd38dc8245959a85298fd` | 03:01:22 | `0x73f37b2c61351f76540acc065f8e5993a1548eecf0e40423de6f8225f5a0a3e6` | 03:02:47 | 85 |
| SICKB · 997,500 | `0x498f39257fc78ae59e81ab7896f87a59de3b0379361b6d95f172c3d2f22d337f` | `0x682701b700c9c65bbc72ff515afd419dcf5ddb5db68c55e1546a51281af31549` | 00:23:13 | `0xb945b23d4bcaad10c705263b17f10bbaa62ebc5f5aa417ede9188f4632853836` | 00:23:47 | 34 |

**All times are November 25, 2026 UTC.**

## How the sample was checked

1. Read the current H#3 `buffabull-activity` state and selected its five latest L3 deposit mint events and five latest L3 withdrawal-initiation events. The service reports chain 5016 confirmed activity, with the inspected state scanning from SickB block 201,011.
2. Use a read-only Ethereum mainnet JSON-RPC to scan blocks **26,463,542–26,495,542** for exact-ID `Deposit` events on the configured lockbox and ERC-20 `Transfer` logs leaving that lockbox.
3. For deposits, match `depositId`, token and raw amount. For withdrawals, decode the lockbox `release(withdrawId,token,to,amount,...)` input and independently match the transfer's token, recipient and amount. **Do not match using timestamp proximity alone.**
4. For each L1 destination/source match, require a successful Ethereum receipt and a receipt block hash equal to the fetched canonical Ethereum block hash. Retain the L3 event's indexed transaction hash, block and timestamp. Confirm chronological order, compute inclusion-to-inclusion intervals, and flag negatives instead of silently discarding them.
5. The script found **10 matches out of 10 requested IDs** in that search window. This does not mean all SickB bridge transfers across mainnet history were identified.

**Limits:** The recent matching script did not independently re-fetch every L3 receipt in the same run; its L3 side relies on the existing canonical-chain activity indexer and its confirmation checks. It did not establish end-user confirmation-display time, mobile SDK behavior, proof-of-stake finality, gas-sponsorship receipt data, fees, reserve backing, or complete historical service availability. Different sampling dates/traffic can produce different results. These receipts are public evidence that can be checked independently using the shown hashes and chain RPCs, not an independent audit.

## Post-workaround physical-device follow-up (two additional transfers)

**Timing:** November 25, 2026 in Pacific time / **November 26, 2026 UTC**. These **two additional transfers were not among the ten baseline transfers in the tables above**. In a later H#3 query, five new L3 bridge events were matched 5/5 to Ethereum. **The founder identified only the final two by time as the bridge-direction tests conducted after enabling MetaMask's unrestricted background activity setting on the physical Android device.** This classification comes from the test operator, not from an attribute encoded onchain.

| Direction | Net/credited asset amount | Bridge ID | Ethereum transaction and block | SickB transaction and block | Source UTC → destination UTC (Nov 26) | Seconds |
| --- | ---: | --- | --- | --- | --- | ---: |
| Ethereum → SickB | **9,351.5625 SICKB** | `0x6dd022dc6fa4b10fc7239475d02a6c39b7911a19ff7063e060d6fc2d19618f65` | `0xb987f458c26969477db3945528aec2a04d202e3963dda364454aa9762d5d30fa` · **26,496,216** | `0xd110aa52dab583a0a8e66f18ed9ffd008197370dcd687f7fce7c556aeabe5ca6` · **352,983** | 01:55:11 → 01:55:33 | **22** |
| SickB → Ethereum | **997,500 SICKB net** | `0x2bbca1c3d140a03b26a53770538652c5f74aa3dbfa2a9200ccac080d16b3a5c5` | `0xfbc36d2c47f1a70c7c0acef48cb8bf92bbf2ee6f1cf1fedf932656107d5c57f2` · **26,496,229** | `0x0d99d8b3c9b81a74bc87b605222092bf8282dd8e4848ca4ed74b079715c4a625` · **352,986** | 01:56:48 → 01:57:47 | **59** |

**Matching query:** Ethereum blocks **26,488,339–26,496,339**, filtered to five selected bridge IDs. Exact-ID deposit event and exact-ID `release()` calldata/lockbox ERC-20 transfer checks matched all five, and the Ethereum transaction receipts were successful with canonical block-hash matches. Only the **final two records** are founder-confirmed post-workaround. The initial ten-transfer baseline remains unchanged.

These measurements exclude wallet connection, approvals, user signing, pre-inclusion waits and Ethereum consensus finality. Successful post-workaround mobile interaction is a separately observed test outcome. This two-transfer follow-up **does not support a causal claim that the Android setting decreased the bridge's intrinsic settlement latency**. The SickB side relies on the H#3 confirmed activity index rather than fresh independent revalidation of every L3 receipt in the matching script.

See [MetaMask Mobile relay-recovery case study](../docs/metamask-mobile-relay-recovery.md#post-workaround-bridge-settlement-matched-mainnet-receipts) for the physical-device investigation and limits.

## Engineering context

- [Baht Bus architecture and trust boundaries](../docs/baht-bus-bridge.md)
- [MetaMask Mobile relay recovery case study](../docs/metamask-mobile-relay-recovery.md) : distinguishes pre-signature wallet transport problems from onchain bridge settlement
- [SickB ecosystem portfolio](../README.md)

**SickB Digital LLC · Public technical evidence · November 25, 2026**
