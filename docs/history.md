# Sick Buffalo: history and founding record

Sick Buffalo began as a community token on the original Pepe Unchained network in January 2025. The project now operates SickB Chain, an Arbitrum Orbit AnyTrust L3. The important part of that transition is not the price history. It is the decisions made when the original infrastructure changed.

## From a meme to an independently deployed token

The Sick Buffalo name came from a familiar joke about a sick water buffalo in Thailand. The first SickB contract and liquidity pool were deployed independently, before Pepe Unchained's automated PumpPad launchpad became available. The community began organizing in January 2025.

The ecosystem also experimented with additional token and governance ideas. Those early arrangements belong to the project's history, not to a list of products that should be assumed active today.

## The April and May 2025 voluntary migration

When Pepe Unchained announced changes to its original blockchain infrastructure in April 2025, SickB holders needed a path to Ethereum. This was a separate, voluntary SickB migration, not a claim that SickB operated the Pepe Unchained network or that the two projects were the same entity.

The founder organized a manual 1:1 migration for eligible SICKB holdings. Participants sent legacy tokens to a designated migration wallet and entrusted their assets to the founder personally. The original transaction amounts were checked and replacement Ethereum SICKB tokens were distributed transaction by transaction. That was a meaningful custody and execution risk for everyone who participated.

Contemporaneous community records place the opening on April 27, 2025, the Ethereum trading launch on May 5, and closure of the migration in late May. The founder reports that every verified migration swap was fulfilled. The project's historical whitepaper also describes that outcome. This portfolio does not yet include a published wallet-by-wallet reconciliation proving the whole migration independently.

That trust was honored, and the experience directly influenced the decision to build and operate independent infrastructure. The point is accountability, not a claim that manual migration is an ideal permanent bridge architecture.

## Cancelled presales, full ETH refunds and token burns

SickB explored public fundraising in 2025, but the proposed offerings were discontinued. The February 2026 [technical whitepaper, Chapter 13](https://sickb.io/whitepaper.pdf) states that **both PinkSale and GemPad were cancelled and all participants received full ETH refunds**. The project did not retain those cancelled presales as development financing. Contemporaneous community notes separately document the PinkSale cancellation in June and the GemPad cancellation in November 2025. The whitepaper is the documentary source for the full-refund statement; this portfolio has not reproduced a participant-by-participant ETH refund transaction ledger.

The whitepaper also records **1,484,000,000 SICKB burned through November 27, 2025**, or **59.36% of the original 2,500,000,000 SICKB supply**, leaving approximately 1,016,000,000 after those burns. These are historical Ethereum-era token supply figures, not a new burn event or a claim about current circulating or bridged balances. The whitepaper describes sending tokens to a dead address. Such transfers remove tokens from practical circulation but do not automatically change an ERC-20 contract's `totalSupply()`; the precise supply semantics must be checked against the token implementation.

| Whitepaper record | Amount | Date or period | Published transaction reference |
| --- | ---: | --- | --- |
| First Ethereum-era burn | 250,000,000 SICKB | September 18, 2025 | [Etherscan transaction](https://etherscan.io/tx/0x7a5804d93228b35b1cffce9fb4ad604098a6d353df02aeed3fbaadea580c05a5) |
| Second Ethereum-era burn | 250,000,000 SICKB | September 26, 2025 | [Etherscan transaction](https://etherscan.io/tx/0x979bb2872bff835da758ce123bb3e1affc15c4face3d8768bd1cd9b4a0a597fd) |
| Additional burns | 250,000,000 SICKB total | Through October 2025 | Aggregated in whitepaper; exact matching transaction references not yet indexed here |
| November milestone burn | 734,000,000 SICKB | November 27, 2025 | [Etherscan transaction](https://etherscan.io/tx/0xfdb8b44d6e1600634e01fcd38f1a6a0d17d93900ab630870b39d1d6bfebaaca7) |
| **Whitepaper total** | **1,484,000,000 SICKB** | Through November 2025 | **59.36% of the original supply** |

For the November 27 transaction, the whitepaper records Ethereum block **23,887,026**, timestamp **02:18:23 UTC**, and 734 million SICKB sent to `0xdEad000000000000000000000000000000000000`. The transaction URLs above come from the whitepaper; while public links are provided, the full 1.484 billion transaction-level reconciliation has not been rerun independently for this review.

Earlier burns of the original Pepe Unchained-era SICKB token, including a February 2025 announcement involving 154,344,445 tokens, are a **different chain and token era**. They are not added to the Ethereum-era 1.484 billion figure.

The founder continued personally financing infrastructure and development. Token market capitalization was not cash raised by the project, and burned supply is not a measure of operating expenditure.

## December 2025: the lost phone and the later Vault design

During a trip to Thailand in December 2025, Joshua Spoehr lost a phone holding wallet access. The [historical whitepaper, Chapter 13](https://sickb.io/whitepaper.pdf) describes **25 million personally purchased SICKB** becoming inaccessible along with approximately **165 million additional SICKB in operational and development wallets** affected during that period. The document describes roughly **190 million tokens** in total as inaccessible.

This is the founder's historical account of lost keys, **not an onchain burn**. Inaccessibility cannot be treated as independently proved permanent merely from a lack of later transfers, and the 190 million is not added to the 1.484 billion confirmed-burn narrative.

The experience was a direct design lesson for SickB Vault: losing a device should not automatically mean losing control of the asset-holding contract. Vault architecture separates **device authorization for specific supported actions** from **ownership and recovery authority held by the original wallet**. An owner who still controls the wallet can remove or replace a lost device's authorization without giving SickB custody of the wallet keys. This does not recreate a lost owner private key or eliminate the need for secure wallet backup. The deployed Vault design is described in [architecture and products](architecture-products.md).

## Building SickB Chain

| Date | Recorded milestone |
| --- | --- |
| January 2025 | Sick Buffalo token and community launched on the original Pepe Unchained network |
| April 26, 2025 | Ethereum SICKB contract deployment recorded in the historical project timeline |
| April 27 to May 2025 | Voluntary migration to Ethereum, manually coordinated |
| June 2025 | Decision to develop an independent chain |
| August 2025 | Early chain development and devnet blocks |
| September to November 2025 | Arbitrum Sepolia development, cross-chain experiments and AnyTrust testing |
| February 2026 | Baht Bus bidirectional flows demonstrated in the development environment |
| June 3, 2026 | SickB Chain mainnet launch, chain ID 5016 |
| June to July 2026 | Mainnet bridge, trading, launch infrastructure and liquidity migration |
| August to November 2026 | Parent-chain batch-posting incident, rehearsal and posting recovery |
| November 2026 | Passkey Vault workflows, Social and Android internal testing, ChadBot V3 development |

Dates above are assembled from project history and founder records. Transaction-specific proof is published separately wherever it is available.

## The founding dedication: block 10

On May 29, 2026, the founder wrote a dedication to the community. It was deployed on June 3 in SickB Chain mainnet block 10, as the first deliberate application transaction after initialization and gas setup.

The [complete original dedication, message hash and receipt](../evidence/genesis-block-10.md) are preserved verbatim. That immutable text should not be modernized to suit an application or marketing document.

## Historical whitepaper

The [SickB technical whitepaper v2.0](https://sickb.io/whitepaper.pdf) is a historical source for the ambitions, architecture and thinking of the project at the time of publication. It is valuable even when individual proposals changed.

It is not an authoritative list of deployed contracts or features today. For current status, use [architecture and products](architecture-products.md), [developer onboarding](developer-start.md) and the [evidence index](../evidence/INDEX.md). Whitepaper versions and specific historical claims should be checked against dated primary sources before being promoted as current functionality.

## Original long-term vision

The whitepaper described Sick Buffalo as more than a chain and token. Its longer-term ambition included a **Sick Buffalo DAO**, specialized **subDAOs**, community-run node and validator participation, entertainment and gaming, integration of **real-world assets (RWAs)**, and a physical **Sick Buffalo Bar** where community members could meet.

These ideas explain why the ecosystem developed governance, Social, trading and launch infrastructure. The bar, revenue-producing property arrangements, community validator program and proposed asset-backed subDAO structures are **historical ambitions**, not businesses, decentralization milestones, profit distributions or technical deployments being claimed as live here. Reprinting them does not create new release dates, spending commitments or a revised technical roadmap.

## How the project was developed

Joshua Spoehr is **Founder, Systems Architect, Developer and Infrastructure Operator**.

AI-assisted engineering has been part of the work since GPT-4. Subsequent AI tools have supported investigation, implementation, test design, documentation and review. They are tools within an owner-directed engineering workflow, not substitutes for onchain receipts, observed service behavior or the founder's responsibility for production systems.

Ethereum, Arbitrum and the open-source work of Offchain Labs made this project technically possible. SickB's work consists of designing, integrating, operating and maintaining its own chain and application stack on those foundations.

## Verification boundaries

This page combines historical community records, the founder's account and separately documented blockchain evidence. The [evidence index](../evidence/INDEX.md) identifies what can already be checked independently and what still needs public source transactions. None of these historical milestones is a claim of audited profitability, third-party security certification or guaranteed investment outcomes.
