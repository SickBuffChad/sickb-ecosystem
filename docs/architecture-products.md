# Architecture and deployed products

**As documented November 2026.** SickB Chain is a live EVM-compatible Arbitrum Orbit AnyTrust Layer 3, chain ID 5016, parented to Arbitrum One. The system includes the chain, an ecosystem-specific Ethereum asset bridge and applications running on top of the L3.

The project uses Ethereum and Arbitrum infrastructure rather than replacing those security and settlement systems.

## Two architectures, not one bridge route

~~~text
ASSET MOVEMENT                              CHAIN / PARENT RELATIONSHIP

Ethereum mainnet (L1)                      Ethereum mainnet
  L1 lockbox and canonical tokens                    |
            |                                        v
   independently verified                     Arbitrum One
   SickB bridge workflow                             |
            |                                        v
            v                                SickB Orbit AnyTrust L3
SickB Chain (L3, 5016)                     sequencer, batches, DA
  wrapped assets + gSICKB
  DEX, Vault, Social and SickPad
~~~

Baht Bus moves supported canonical assets directly between Ethereum's lockbox and SickB's L3 contracts. Arbitrum One is the L3's parent for the Orbit architecture, not an intermediate asset custody hop on those routes.

For the underlying protocol distinction between Rollup and AnyTrust, see [Arbitrum's AnyTrust documentation](https://docs.arbitrum.io/how-arbitrum-works/deep-dives/anytrust-protocol).

## Infrastructure SickB operates

The founder runs and maintains the relevant node and application infrastructure, including:

| Layer | Public description | Boundary |
| --- | --- | --- |
| Ethereum mainnet | Reth execution client and Lighthouse consensus client | The Ethereum network itself is not operated by SickB |
| Arbitrum One | Self-operated Nitro node | Arbitrum One is the parent chain, not SickB's own L2 |
| SickB L3 | Sequencer, block execution and operational monitoring | Single-operator sequencing remains a centralization consideration |
| Data availability | AnyTrust data-availability services and committee arrangement | Committee and fallback assumptions require explicit trust analysis |
| Cross-chain operations | Lockbox, verifier/attester, relayer and audit or reconciliation functions | Settlement spans separate transactions and is not cross-chain atomic |
| Applications | Social, DEX, Vault, SickPad, explorer and supporting services | Production application source and operational credentials are not public here |

No hostnames for nonpublic nodes, machine access instructions, signing configuration or credentials are included.

## Deployed or demonstrated components

| Product | Status | What it does | Scope to keep clear |
| --- | --- | --- | --- |
| SickB Chain | Mainnet since June 3, 2026 | EVM transactions and application deployment on chain 5016 | An Orbit L3, not a new Ethereum L1 |
| Baht Bus | Mainnet transfer routes exercised | Ethereum to SickB and SickB to Ethereum for SICKB, WETH and USDC | Independent matching evidence is sampled, not complete historical assurance |
| Native gas sponsorship | Used in supported bridge and onboarding paths | Supplies gSICKB so a newly arrived user can transact | Route, ticket and sponsor conditions apply |
| DEX and trading terminal | Mainnet product | Onchain swaps and trading interfaces | No independently published trading-volume or TVL totals here |
| SickPad | Founder-launch implementation deployed | Token/project launch infrastructure | External project adoption is not assumed |
| Vault | Mainnet contracts and founder-tested human workflows | Owner-held contracts with passkey confirmations for supported sends and swaps | Operator and factory privileges remain security considerations |
| Social | Live website | Wallet-linked posts, profiles, discovery and interactions | Does not imply established mass adoption |
| Android Product Zero | Google Play internal testing | Mobile access to Social and related onchain workflows | General Play production release not claimed |
| ChadBot | V3 functionality implemented, integrations vary | Community history, memory, web research and read-only chain context | Server-side capabilities must be confirmed separately |
| Explorer and governance | Explorer available; governance still evolving | Network inspection and a framework for future stewardship | Planned DAO reserve custody is not presented as complete |

## Bridge and Vault trust boundaries

The [Baht Bus architecture](baht-bus-bridge.md) describes the lockbox, route registry, L3 mint and burn, verification, gas tickets, fees, and the distinction between local L3 atomicity and cross-chain completion. The [transaction evidence](../evidence/bridge-matched-transfers-2026-11-25.md) contains exact source and destination IDs with block timestamps.

Vaults are individual smart contracts owned through the user's wallet. A registered passkey can authorize specific supported human actions. It does not transfer wallet ownership to SickB. However, it would be inaccurate to describe the entire system as having no delegated authority: administrative permissions, relaying privileges, and separate bot authorization are part of the design. The human device lock does not halt the separate owner and bot paths. An independent security audit of the entire deployed system has not been completed.

## Practical experience and known limits

In 2026, the team investigated and recovered from an extended parent-chain batch-posting backlog. That experience is relevant to operational reliability, but complete dated posting receipts and reconciliation artifacts remain a separate publication task.

The [MetaMask Mobile investigation](metamask-mobile-relay-recovery.md) documented a physical-device wallet-confirmation issue and a reversible Android workaround. Successful bidirectional bridge tests after the workaround required no SickB production code changes. A proposed wallet-side recovery repair remains experimental.

For contract addresses, network connection details, read-only queries and collaboration options, start with [developer onboarding](developer-start.md). For proof and unverified claims, use the [evidence index](../evidence/INDEX.md).
