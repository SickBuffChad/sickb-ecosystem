# SickB Ecosystem

**Built independently. Powered by Arbitrum. Open to collaboration.**

Welcome to the official technical documentation and development portfolio for SickB.

SickB is a live Arbitrum Orbit AnyTrust Layer 3 ecosystem, built and operated primarily by one self-funded developer.

What began as a small cryptocurrency community has grown into an operating blockchain with its own Ethereum bridge, decentralized exchange, smart-contract Vaults, launch infrastructure, Social platform, Android application, and AI-powered community agent.

This repository exists to make that work accessible.

Here you'll find architecture explanations, technical references, user guides, verified development milestones, and our roadmap. Developers can explore what we've built, understand how our systems work, and identify opportunities to contribute or integrate.

We believe good engineering should be understandable and verifiable. That doesn't require publishing private infrastructure configurations, security credentials, or proprietary implementation details.

**The infrastructure is running. The ecosystem is growing. And we're opening the door to the people who want to help build what comes next.**

## The first deliberate transaction: a message to the Herd

SickB Chain did not begin with a token sale or a marketing announcement. Its **first deliberate application transaction** was a permanent dedication written by the founder on **May 29, 2026** and deployed on **June 3, 2026**, in **SickB Chain mainnet block 10**. Initialization occupied blocks 1–8, with a gas deposit in block 9.

From that dedication:

> I remember setting up my first purchase of Litecoin over a decade ago, never did I think I would eventually create something like this.

> The blocks can drop, and the goal can be reached.

> Never forget, "All roads lead to SickB" and this community that will build from here into the future needs you to tell the story.

[**Read the complete founder dedication and successful block-10 transaction receipt**](evidence/genesis-block-10.md).

The complete 907-byte message is embedded in the immutable `SickBGenesis` contract. Anyone can verify the message through `getMessage()` and the canonical `messageHash()` on **SickB Chain (5016)**.

| Founding record | Value |
| --- | --- |
| Mainnet block | **10** |
| Transaction | `0xaf525995884b1c6f0b0086ff5554ec952523d095ce2dbc3f66d213954da99ab8` |
| SickBGenesis contract (chain 5016) | `0x86734D2fc365231b8502254e08aE635Ae949DA0A` |
| Contract message hash (keccak256) | `0x34c0404f3fe18f5a68027de66dc43c9252855d7a1d6599af0e04af1a1355ac7c` |
| Canonical message file SHA-256 | `df41ef3015e9f73f7154a0755c76189a7173e8d6be95a290ed0e9fa892e0b1fa` |

This dedication was placed onchain **20 days before the founder's June 23 target date**. It is a record of gratitude, perseverance and the people who helped SickB survive the transition from a meme-token community into an operating blockchain.

## The architecture at a glance

SickB has **two related but distinct architectures**: the Ethereum ↔ SickB **Baht Bus asset bridge**, and the **Orbit L3 rollup parent relationship** with Arbitrum One.

```text
BAHT BUS — ASSET MOVEMENT                 ORBIT — CHAIN ARCHITECTURE
Ethereum mainnet (lockbox)               Ethereum mainnet (settlement)
              ⇅                                     │
  independently verified bridge                    ▼
   events / transfer releases                  Arbitrum One
              ⇅                                     │
SickB Chain (L3, chain 5016)                       ▼
  wrapped assets + gSICKB                     SickB Chain L3
  DEX / Vault / Social                        AnyTrust / sequencer
```

**Arbitrum One is SickB's parent chain, not an intermediary asset bridge.** The actual Baht Bus asset flow connects Ethereum's lockbox directly to SickB's L3 bridge contracts.

**Infrastructure we operate:** Ethereum execution and consensus nodes (**Reth + Lighthouse**), an **Arbitrum One Nitro node**, SickB's **L3 sequencer**, and its **AnyTrust infrastructure**, plus bridge relayers, an auditor and independent verification/attestation services.

SickB relies on Ethereum/Arbitrum settlement and open-source Arbitrum technology, while independently operating its own node and application stack. [**Detailed Baht Bus architecture**](docs/baht-bus-bridge.md).

## What is built

| Component | Current status | Purpose |
| --- | --- | --- |
| **SickB Chain** | Live mainnet since June 2026 | EVM-compatible Arbitrum Orbit AnyTrust L3, chain ID **5016** |
| **Baht Bus Bridge** | Deployed and exercised with real assets | Ethereum ↔ SickB Chain routes for SICKB, WETH and USDC, with sponsored-gas onboarding |
| **SickB DEX** | Mainnet product | Onchain swaps and trading terminal |
| **SickPad** | Mainnet founder-launch implementation | Project registration and launch infrastructure; broader ecosystem launches are a growth objective |
| **SickB Vault** | Mainnet contracts and tested human flows | Individual owner-controlled Vaults, passkey-authorized Social payments and DEX swaps, sponsored execution |
| **Automated trading** | Existing bot infrastructure | Configurable trading permissions and limits, distinct from the human Vault path |
| **SickB Social** | Live website; continuing development | Wallet-linked discovery, social interaction and paths to onchain activity |
| **Android Product Zero** | Google Play **internal testing** | Mobile access to the integrated SickB experience, not yet a claim of general public Play release |
| **ChadBot** | V3 capabilities implemented; operational integrations vary | Community history and memory, web research, read-only chain and bridge knowledge |
| **Explorer and governance** | Explorer live; governance evolving | Chain transparency now, greater community stewardship as a future goal |

### 1. Baht Bus Bridge: SickB's native bridge to Ethereum

**SickB is the blockchain. Baht Bus is the bridge we engineered to serve it.** Rather than rely on an external interoperability provider, we built an Ethereum ↔ SickB asset bridge as part of the chain's own infrastructure.

The system was developed and repeatedly tested on our Sepolia-based L3 testnet before mainnet. It has operated with real-asset transfers in **both directions since June 2026**, with SICKB, WETH and USDC supported through a registry-driven design.

- **Ethereum → SickB:** canonical assets are locked on Ethereum; authorized L3 finalization combines wrapped-token minting and native **gSICKB** sponsorship in an atomic L3 transaction.
- **SickB → Ethereum:** a single L3 transaction receives wrapped tokens, burns the net withdrawal amount, and delivers a native gas ticket. If sponsorship fails, the L3 transaction reverts. A separate verifier/attester authorizes the later Ethereum release.
- **Controls:** verified routes, unique transfer IDs, processed/released checks, reconciliation, and separately operated verification and transaction-submission functions.
- **Backing and economics:** wrapped assets are designed to remain collateral-backed on Ethereum. Mainnet V2 product configuration specifies a **0.25% withdrawal fee**, with protocol-owned wrapped fee reserves intended to remain backed; live onchain settings are authoritative.

**Atomicity applies to the relevant L3 transaction—not to all transactions across Ethereum and SickB simultaneously.** Cross-chain processing and recovery are separate steps. The founder reports approximately five months of successful bidirectional operations, without claiming infallibility or guaranteed timing.

**[Read the Baht Bus engineering architecture, both flows, safety boundaries and design rationale](docs/baht-bus-bridge.md).**

**Public Ethereum-side contract:** [UniversalLockBoxL1 on Etherscan](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A).

Future community/DAO-multisig stewardship of protocol-owned reserves is a roadmap goal, **not an existing governance arrangement**.

### 2. SickB Vault: remove repeated wallet friction without taking the keys

The Vault system grew from a practical problem: on mobile, repeated external wallet connections and transaction prompts can make ordinary Web3 interactions unnecessarily difficult.

Each Vault is an **individual smart contract**. The original wallet remains its owner and its recovery and withdrawal authority. A registered passkey can confirm an exact supported action, including:

- Sending supported tokens to another registered Vault through SickB Social.
- Trading on the SickB DEX with the amount, path and minimum output bound to the confirmation.
- Locking or unlocking the **device-confirmed human action path**.

The H#3 operator relays approved actions and sponsors gas; the device credential does not itself hold the user's tokens. **Automated bot execution is a separate permissioned path and is not stopped by the human lock.** The owner wallet retains powerful administrative authority, and delegated operator/factory permissions remain part of the security model. The project does not custody users' wallet private keys, but that fact should not be confused with having no delegated administrative privileges.

**Public mainnet contract references (SickB Chain, chain ID 5016):**

| Contract | Address |
| --- | --- |
| SickbVaultDevices | `0x483D8267cd21c3733d21e27be063163B2fA7beDD` |
| SickbVaultExecutor | `0xfE329B2Fe4a5b1cCb945abb965a538E19590d2a9` |
| BotVaultFactory | `0x443f069f778F0080Bd704aD9212D9232441A2818` |

The two new contracts' deployment identity and compiled runtime were independently reproduced against source, alongside **195 passing fork checks** in the November 2026 engineering review. This is **not a full third-party audit of every live component**. Production-relay and wider device-testing limitations are documented internally and are being addressed before broader distribution.

### 3. Product Zero: put a working ecosystem in people's hands

SickB Social is intended to be a **front door**, not a replacement for X, Telegram, Reddit or Facebook. Community conversations and outward sharing help people discover the project; linked Vault, bridge and trading experiences give them something useful to do when they arrive.

The Android app is distributed through **Google Play internal testing**. The founder and testers have exercised real onboarding and mainnet Vault flows. Public Play distribution, additional device-compatibility testing and release polish are separate milestones.

### 4. ChadBot: a community agent with context

ChadBot began as a Telegram personality and was rebuilt around historical community material. The V3 engineering work includes persistent community notes and lore, a daily diary, contextual web research, read-only wallet/bridge/chain information and guides that can help new users identify their next step.

The agent is designed to work from actual ecosystem data rather than inventing balances or onchain events. Some monitoring and proactive features are implemented but still depend on operational activation; proposed V4 capabilities are **future work**, not claims of current production behavior.

### 5. Operational engineering: maintaining the chain when things fail

SickB is personally funded and predominantly built and operated by **one founder who also works full-time**.

This includes more than the initial Orbit deployment: nodes, sequencer, parent-chain batch submission, data availability, cross-chain services, monitoring and incident recovery.

During 2026, a **55-day Arbitrum parent-chain batch-posting backlog** required investigation, recovery rehearsal and restoration of production posting. That experience matters because a blockchain must be operated and recovered, not merely launched. Dated posting and reconciliation evidence will be added to the public proof package.

### 6. Mobile wallet engineering: diagnose the fault before changing the bridge

SickB's Android testing exposed a frustrating failure: MetaMask Mobile could open to its home screen instead of showing a pending confirmation after an Ethereum approval or network switch. We treated this as an **interoperability and transport-recovery investigation**, not an excuse to modify otherwise successful bridge settlement code.

The November 25, 2026 [MetaMask Mobile relay-recovery case study](docs/metamask-mobile-relay-recovery.md) documents three layers of evidence:

1. **Reproducible transport behavior.** A local fault-injection harness using the inspected MetaMask communication library reproduced a lost relay-channel membership problem **16/16 times**. A candidate wallet-side rejoin repair passed **32/32 checks in three separate runs**. The controlled harness is not a trace of the deployed MetaMask relay.
2. **Read-only physical-device diagnostics.** On one Android 16 device running MetaMask Mobile 8.21.0, ADB captured seven transitions into an effective `APP_BACKGROUND` network block while the wallet process was still alive. These observations support a possible interruption mechanism but do not prove the cause of every missed confirmation.
3. **A reversible workaround, tested end to end.** Allowing **unrestricted background battery activity for MetaMask** removed the effective network block on that device. The founder then completed **Ethereum → SickB and SickB → Ethereum bridge journeys, including network switching, without restarting MetaMask**. No SickB production connector, bridge contracts, bots, Vault or transaction sequencing were changed. This device-specific workaround may increase battery use.

**Why share it?** A wallet process being alive, a transport reporting connected, and a relay channel being joined are not equivalent guarantees of message delivery. Mobile dApp and wallet developers can use the documented failure mode to inform reconnect logic, state restoration and safe handling of outstanding requests **without duplicate transaction submission**. SickB has prepared upstream investigation material and a reproducible harness; a sanitized public reproduction and formal MetaMask upstream issue remain planned, not published or accepted fixes.

This is one example of the engineering approach behind SickB: **observe the real fault → reproduce it under controlled conditions → distinguish evidence from hypotheses → verify the smallest safe intervention → publish limitations and reusable lessons.**

## Project history

| Date | Milestone |
| --- | --- |
| **January 2025** | Sick Buffalo launches as an independently deployed token and community project |
| **April–May 2025** | Voluntary, manually coordinated 1:1 migration to Ethereum |
| **June–November 2025** | Decision to build an independent chain; devnet, testnet, early cross-chain proofs and AnyTrust development |
| **February 2026** | Baht Bus bridge operating in both directions in the development environment |
| **June 3, 2026** | **SickB Chain mainnet** launches, chain ID 5016 |
| **June–July 2026** | Mainnet DEX, SickPad founder-launch infrastructure and liquidity migration |
| **August–November 2026** | Batch-posting incident investigation, recovery and resumed posting |
| **November 2026** | Mainnet passkey Vault actions, Social and Android internal testing, ChadBot upgrades |
| **November 25, 2026** | Published MetaMask Mobile relay-recovery case study and validated an Android background-network workaround for bidirectional bridging and network switching on one physical device |

## Public links and evidence

| Resource | Link |
| --- | --- |
| Main website and Social | [sickb.io](https://sickb.io) |
| Ethereum ↔ SickB bridge | [Baht Bus Bridge](https://sickb.io/bridge) |
| DEX and trading | [SickB Trade](https://sickb.io/dex) |
| Launch infrastructure | [SickPad](https://sickb.io/sickpad) |
| Chain explorer | [SickB Scan](https://sickb.io/scan) |
| Ethereum lockbox | [Etherscan contract](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A) |
| Mainnet read-only RPC | `https://rpc-mainnet.sickb.io` |
| Mobile-wallet relay recovery | [MetaMask Mobile: technical case study](docs/metamask-mobile-relay-recovery.md) |
| Mainnet bridge transfer evidence | [10 cross-chain transaction matches, November 25, 2026](evidence/bridge-matched-transfers-2026-11-25.md) |
| Chain ID | `5016` |

**Evidence status and release plan:** The public repository now includes a documented [launch-era block-10 proof](evidence/genesis-block-10.md), a [mobile-wallet case study](docs/metamask-mobile-relay-recovery.md), and a [November 25 sample of ten matched L1/L3 bridge transfers](evidence/bridge-matched-transfers-2026-11-25.md). Still to add: comprehensive historical bridge coverage, dated collateral/supply reconciliation by asset, parent-chain batch-posting recovery receipts, and privacy-safe Product Zero screenshots. A ten-transfer sample is **not** a performance guarantee or a complete historical audit. No unverified TVL, user counts, bridge volume or uptime claims will be published.

## Why Arbitrum mentorship, why now?

The infrastructure exists. Contracts are deployed. Real asset transfers, transactions and internally tested app journeys exist. The next bottleneck is **adoption and sustainable growth**, not funding an idea that has not yet been built.

SickB is applying for Arbitrum mentorship to gain:

- Experienced product and go-to-market guidance.
- Distribution and partnerships across the Arbitrum ecosystem.
- More independent technical scrutiny and external contributors.
- Connections with mobile-wallet and Orbit developers to turn our documented integration and recovery findings into reusable community knowledge.
- A sharper onboarding and retention strategy for Product Zero.
- A sustainable path from self-funded solo development to an ecosystem serving real users.

> **I am not asking Arbitrum to build SickB for me. I have already built the foundation. I am asking for help turning it into something that can grow.**

---

**Status note (November 25, 2026):** This repository is a public-facing portfolio and evidence index. It does **not** contain the complete private production codebase or operational infrastructure configuration, and its existence does not imply code licensing or security certification.

**SickB Digital LLC** · [sickb.io](https://sickb.io)
