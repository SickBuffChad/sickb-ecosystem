# Sick Buffalo (SickB)

Sick Buffalo began as a community token in January 2025. It now operates SickB Chain, a live Arbitrum Orbit AnyTrust Layer 3 on Arbitrum One, with an Ethereum asset bridge and applications built around trading, launch infrastructure, Social and smart-contract Vaults.

This repository is the **current official engineering documentation and public technical reference** for [SickB Digital LLC](https://sickb.io). It describes the deployed systems, integration boundaries, historical records and supporting evidence. Production application source and privileged operational materials remain private.

Project lead: **Joshua Spoehr, Owner and Founder of SickB Digital LLC, Systems Architect, Developer and Infrastructure Operator**. SickB has been self-funded and developed with AI assistance beginning with GPT-4, under Joshua's direction and testing. His GitHub contribution activity was reported as **2,561 contributions for the preceding year on November 25, 2026**. This is a founder-provided GitHub activity figure, not a commit count or a count of deployed changes. Ethereum, Arbitrum and Offchain Labs provided the technology on which SickB Chain was built.

## Start here: five areas

| Area | First document | What you will find |
| --- | --- | --- |
| 1. History and founding story | [Our history](docs/history.md) | Sick Buffalo's origins, voluntary migration, original founder records, reported refunds and burns, and the founding dedication |
| 2. Architecture and deployed products | [Architecture and products](docs/architecture-products.md) | Orbit topology, self-operated nodes, Baht Bus, DEX, Vault, Social, Android and ChadBot |
| 3. Developer onboarding and integration | [Developer start](docs/developer-start.md) | Chain settings, public RPC, contract addresses, gas sponsorship, read-only checks and integration boundaries |
| 4. Verifiable engineering evidence | [Evidence index](evidence/INDEX.md) | Genesis receipt, matched L1/L3 transfers, mobile debugging, proof gaps and reserve-reconciliation method |
| 5. Roadmap and collaboration | [Current priorities and collaboration](docs/collaboration.md) | Existing milestones, integration opportunities, technical review and mentorship objectives |

A developer unfamiliar with SickB should start with the chain ID and RPC in the [developer guide](docs/developer-start.md), inspect a transaction in the [evidence index](evidence/INDEX.md), and then follow the contract-specific architecture references.

## What exists today

| System | Current position |
| --- | --- |
| SickB Chain | Live since June 3, 2026. Arbitrum Orbit AnyTrust L3, chain ID 5016, parented to Arbitrum One |
| Infrastructure | Founder-operated Ethereum Reth and Lighthouse nodes, Arbitrum One Nitro node, SickB sequencer and AnyTrust services |
| Baht Bus Bridge | Mainnet Ethereum to SickB asset routes in both directions for SICKB, WETH and USDC; supported flows incorporate gSICKB sponsorship |
| SickB DEX | Mainnet trading and swap interfaces |
| SickPad | Deployed founder-launch infrastructure; general third-party adoption should not be assumed |
| SickB Vault | Owner-controlled contracts with mainnet-tested, passkey-authorized supported sends and swaps |
| SickB Social | Live wallet-linked social and discovery application |
| Android Product Zero | Google Play internal testing, not a claim of general public Play distribution |
| ChadBot | Community memory, research and read-only blockchain functionality; some operational integrations still require individual validation |
| Explorer and governance | Chain-explorer entry point and governance work in progress; future treasury stewardship is not described as already deployed |

The bridge is a specific Ethereum asset-service connection. Arbitrum One is SickB's parent chain, not an intermediate Baht Bus asset hop.

~~~text
ASSETS                                CHAIN ARCHITECTURE

Ethereum canonical tokens            Ethereum
       |                                   |
Ethereum Baht Bus lockbox              Arbitrum One
       |                                   |
Independent verification               SickB Orbit L3
       |                               AnyTrust + sequencer
SickB wrapped tokens
       |
DEX / Vault / Social / SickPad
~~~

The architecture uses a single-operator sequencer and committee-based data availability assumptions. Smart contracts and services are not represented as independently audited or fully decentralized.

## History worth preserving

When Pepe Unchained's infrastructure changed in 2025, SickB holders voluntarily entrusted legacy tokens to Joshua for a manually checked 1:1 Ethereum migration. Founder announcements and a participant's receipt confirmation are preserved in the project archive. The complete wallet-by-wallet reconciliation is still an evidence task.

PinkSale and GemPad were discontinued. The original community record includes a PinkSale refund acknowledgement and instructions for GemPad participants to obtain refunds; confirming the full ETH returned to all participants requires the underlying sale and refund transactions. September 2025 founder announcements also describe two 250-million-SICKB Ethereum-era burns. The larger historical burn total remains subject to complete ERC-20 event reconstruction rather than being presented as verified supply.

The chain's first deliberate application transaction, on June 3, 2026 in mainnet block 10, preserved a message written to the community on May 29:

> The blocks can drop, and the goal can be reached.

The [full dedication and chain-specific receipt](evidence/genesis-block-10.md) remain unchanged.

In December 2025, Joshua lost a phone containing wallet and authentication access. That experience helped shape the later Vault principle: a device may authorize a specific action while ownership of the assets remains with the original owner wallet. The project's early discussions also proposed DAO governance, subDAOs, community infrastructure participation, entertainment, RWA projects and a Sick Buffalo Bar. Those are historical ideas, not claims of deployed functionality or new commitments.

Read the [founding history](docs/history.md), the [original-record provenance register](evidence/historical-provenance.md), and the [verification backlog](evidence/verification-gaps.md).

## Engineering evidence you can inspect

- [Baht Bus architecture](docs/baht-bus-bridge.md) covers both directions, verification roles, gas sponsorship, the L3 atomicity boundary and the Ethereum lockbox.
- [November 25 cross-chain transaction evidence](evidence/bridge-matched-transfers-2026-11-25.md) records ten selected exact-ID matches and two later mobile follow-ups, with source and destination transaction hashes and UTC block timestamps. The first ten had a 45-second median inclusion-to-inclusion time. This is a test sample, not a performance guarantee.
- [MetaMask Mobile relay recovery](docs/metamask-mobile-relay-recovery.md) documents the controlled communication failure reproduction and a verified Android background-network workaround on one physical device. The bridge continued to work as designed; no SickB production changes were necessary for the successful post-workaround tests.
- [Genesis block 10](evidence/genesis-block-10.md) preserves the immutable dedication and transaction fields.
- [Collateral reconciliation procedure](evidence/reconciliation-method.md) explains how to compare Ethereum lockbox balances with SickB wrapped supply and in-flight transactions without inventing a reserve total.
- [Outstanding verification gaps](evidence/verification-gaps.md) identifies still-missing parent-chain recovery receipts, full-history matching, token burn/refund proof bundles, audited-style backing data and broader testing.

Market capitalization is not corporate funding, bridge locked value, protocol revenue or an estimate of capital invested in SickB. Those measures must be evidenced independently.

## Network and public references

| Resource | Reference |
| --- | --- |
| Chain ID | 5016 (0x1398) |
| Native gas | gSICKB |
| Public SickB RPC | https://rpc-mainnet.sickb.io |
| Mainnet explorer | [SickB Scan](https://sickb.io/explorer), labeled SickB Chain mainnet, chain ID 5016 |
| Ethereum lockbox, chain 1 | [0x86734D2fc365231b8502254e08aE635Ae949DA0A](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A) |
| Main product | [sickb.io](https://sickb.io) |
| Ethereum asset bridge | [sickb.io/bridge](https://sickb.io/bridge) |
| Developer contract list | [Chain-specific mainnet references](docs/developer-start.md#contracts-and-supported-assets) |

The [mainnet explorer](https://sickb.io/explorer) identifies SickB Chain as chain **5016** and displays recent mainnet blocks and transactions. For reproducible checks, use the [read-only RPC instructions](docs/developer-start.md) and exact transaction hashes.

## Collaboration and mentorship

SickB has submitted an application to the Arbitrum Foundation **ARB02 Mentorship Program** and has publicly announced this repository. Submission does not imply acceptance.

The immediate priorities are developer collaboration, user adoption, outside scrutiny, practical guidance and a sustainable operating model. Financial support would be welcome but is not the primary reason for applying.

Read [current collaboration priorities](docs/collaboration.md) and [our AI-assisted engineering workflow](docs/engineering-workflow.md) before proposing work. This portfolio does not publish private deployment code, signing infrastructure or credentials, grant an unstated software license, or authorize changes to live services.

No third-party security audit of the entire ecosystem is claimed. Corrections and independently reproducible observations are welcome.

SickB Digital LLC | [sickb.io](https://sickb.io)
