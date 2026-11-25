# SickB Ecosystem

**One independent founder. A live Arbitrum Orbit L3. An ecosystem built to be used.**

[**Explore SickB**](https://sickb.io) · [**Bridge**](https://sickb.io/bridge) · [**Trade**](https://sickb.io/dex) · [**SickPad**](https://sickb.io/sickpad) · [**Chain explorer**](https://sickb.io/scan)

SickB started as a meme-token community in January 2025. When the infrastructure underneath that community changed, its founder organized a manual migration to Ethereum instead of abandoning holders. The experience led to a bigger decision: build and operate the infrastructure the project depends on.

On **June 3, 2026**, SickB Chain launched on mainnet. Today the ecosystem combines an independently operated **Arbitrum Orbit AnyTrust Layer 3**, a purpose-built **Ethereum asset bridge**, DEX and launch infrastructure, individual smart-contract Vaults, Social, an Android app in **Google Play internal testing**, and **ChadBot**, an AI community agent.

This is a **public technical and product portfolio** for prospective users, collaborators, reviewers, and the Arbitrum ecosystem. It is not a token offering, an assertion of a completed independent security certification, or a dump of operational credentials and private production source.

## The architecture at a glance

```text
Ethereum mainnet (L1)
    │
    │  SickB's custom Baht Bus asset bridge
    │  Ethereum lockbox ↔ L3 minting / withdrawal / verification
    ▼
Arbitrum One (parent chain)
    │
    │  Arbitrum Orbit / AnyTrust
    ▼
SickB Chain (Layer 3, chain ID 5016)
    │
    ├── DEX, trading terminal and automated trading
    ├── SickPad project-launch infrastructure
    ├── Owner-controlled Vaults and device-authorized actions
    ├── SickB Social and Android Product Zero
    ├── ChadBot, community history and live chain information
    └── Explorer, oracle services and evolving DAO governance
```

**Important distinction:** SickB is an **Arbitrum Orbit L3 using Arbitrum One as its parent**. It is not a claim to have invented the underlying Arbitrum technology or to be a native application deployed directly on Arbitrum One. The founder built and operates the SickB-specific chain configuration, cross-chain bridge architecture, services and applications on top of open-source foundations including Arbitrum.

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

### 1. Baht Bus Bridge: infrastructure, not a third-party widget

The bridge was **engineered for SickB** rather than added as a front end to an existing third-party bridge. Its architecture includes:

- Ethereum L1 lockbox contracts and L3 asset minting and withdrawal contracts.
- Registry-driven support for **SICKB, WETH and USDC**.
- Automated verification, reconciliation and safety checks around cross-chain movement.
- **Sponsored native gas** for supported onboarding, so users can transact after bringing assets to the L3.
- A route model designed around **1:1 Ethereum collateral backing** of wrapped assets.
- A configured **0.25% (25-basis-point) mainnet withdrawal fee**, with protocol-owned wrapped fee reserves intended to remain backed by L1 collateral.
- No intentional fixed aggregate bridge-capacity ceiling; transfers remain subject to route controls, collateral and operational constraints.

Transfers have completed in **tens of seconds in observed cases**, but that is not a guaranteed completion time. A public evidence pack will supply matched receipts and dated backing/reconciliation snapshots rather than rely on marketing claims.

**Public L1 contract:** [UniversalLockBoxL1 on Etherscan](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A).

The planned next stage is community/DAO-multisig stewardship of protocol-owned reserves. **That governance transition is not represented as completed.**

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
| Chain ID | `5016` |

**Evidence release plan:** Add a dated, read-only proof bundle with representative L1/L3 bridge receipts, collateral and supply reconciliations by asset, operator batch-posting recovery records, deployed contract references, and Product Zero screenshots with personal information removed. No unverified TVL, user counts, bridge volume or performance guarantees will be published.

## Why Arbitrum mentorship, why now?

The infrastructure exists. Contracts are deployed. Real asset transfers, transactions and internally tested app journeys exist. The next bottleneck is **adoption and sustainable growth**, not funding an idea that has not yet been built.

SickB is applying for Arbitrum mentorship to gain:

- Experienced product and go-to-market guidance.
- Distribution and partnerships across the Arbitrum ecosystem.
- More independent technical scrutiny and external contributors.
- A sharper onboarding and retention strategy for Product Zero.
- A sustainable path from self-funded solo development to an ecosystem serving real users.

> **I am not asking Arbitrum to build SickB for me. I have already built the foundation. I am asking for help turning it into something that can grow.**

---

**Status note (November 25, 2026):** This repository is a public-facing portfolio and evidence index. It does **not** contain the complete private production codebase or operational infrastructure configuration, and its existence does not imply code licensing or security certification.

**SickB Digital LLC** · [sickb.io](https://sickb.io)
