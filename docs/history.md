# Sick Buffalo: history and founding record

Sick Buffalo began as a community token on the original Pepe Unchained network in January 2025. The project now operates SickB Chain, an Arbitrum Orbit AnyTrust L3. The important part of that transition is not the price history. It is the decisions made when the original infrastructure changed.

## From a meme to an independently deployed token

The Sick Buffalo name came from a familiar joke about a sick water buffalo in Thailand. The first SickB contract and liquidity pool were deployed independently, before Pepe Unchained's automated PumpPad launchpad became available. The community began organizing in January 2025.

The ecosystem also experimented with additional token and governance ideas. Those early arrangements belong to the project's history, not to a list of products that should be assumed active today.

## The April and May 2025 voluntary migration

When Pepe Unchained announced changes to its original blockchain infrastructure in April 2025, SickB holders needed a path to Ethereum. This was a separate, voluntary SickB migration, not a claim that SickB operated the Pepe Unchained network or that the two projects were the same entity.

The founder organized a manual 1:1 migration for eligible SICKB holdings. Participants sent legacy tokens to a designated migration wallet and entrusted their assets to the founder personally. The original transaction amounts were checked and replacement Ethereum SICKB tokens were distributed transaction by transaction. That was a meaningful custody and execution risk for everyone who participated.

Founder-authored migration announcements and archived community messages date the opening to April 27, 2025, Ethereum trading to May 5, and the closing period to late May. A participant confirmed receiving replacement tokens, and Joshua reports fulfilling every verified migration request. The archived migration-channel transaction roster is not yet reconciled publicly wallet by wallet; see the [historical source ledger](../evidence/historical-provenance.md).

That trust was honored, and the experience directly influenced the decision to build and operate independent infrastructure. The point is accountability, not a claim that manual migration is an ideal permanent bridge architecture.

## Cancelled presales, refund records and token burns

SickB explored fundraising in 2025. Both proposed presales were discontinued, and neither should be described as an active offering or counted as current project financing.

Contemporaneous community records include Joshua's June 18, 2025 announcement cancelling PinkSale (archive message #49084) and a participant's confirmation of a refund (#49098). On November 26, 2025, Joshua announced the GemPad cancellation and directed participants to the sale page for refunds (#55794). These records document cancellation and refund activity. A complete transaction-level ledger showing the amount of ETH returned to **every** participant in both sales has not yet been independently assembled; the project does not claim such reconciliation here.

There were token burns on the original Pepe Unchained deployment and later on Ethereum. These must be counted separately, using the contract address and chain for each event. The archived September 18 and September 26, 2025 announcements describe two Ethereum-era burns of **250 million SICKB each** (archive messages #53877, #53882 and #54117). A subsequent founder record reports a larger cumulative burn, but its complete transaction breakdown still requires an Ethereum ERC-20 transfer-event audit. The [evidence backlog](../evidence/verification-gaps.md) records the proposed aggregate and the exact verification needed; it is not presented here as an independently verified current supply figure.

The Ethereum token contract is [SICKB on chain 1](https://etherscan.io/token/0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3). Transfers to an inaccessible address may reduce practical circulation without reducing the ERC-20 contract's reported `totalSupply()`. A published burn count needs the matching contract, destination, transaction hashes, logs and accounting convention.

Joshua continued paying for development and infrastructure personally. Neither token market capitalization nor a cancelled presale is a measure of capital committed to SickB Digital LLC.

## December 2025: the lost phone and the later Vault design

During travel in December 2025, Joshua lost a phone containing important authentication and wallet access. In his own subsequently archived community messages, he described wallets without recoverable backups and the practical difficulty of replacing an unavailable two-factor-authentication device (founder archive references #56408 and #61334). Any precise value of inaccessible tokens should be verified against wallet records before publication.

That experience informed the later SickB Vault design. **A registered device can authorize specific supported operations without becoming the owner of the Vault's assets.** The original owner wallet retains contract ownership and the authority to remove a lost device or authorize another. This separation makes device replacement possible when the owner wallet remains accessible; it cannot restore an unrecoverable owner's signing keys. See [Vault architecture](architecture-products.md).

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

## Current official engineering reference

This public repository is the **current official SickB engineering documentation and technical reference** maintained for SickB Digital LLC. Its [architecture](architecture-products.md), [developer configuration](developer-start.md), and [evidence index](../evidence/INDEX.md) distinguish deployed functionality from founder history and proposals. Older project ideas are not substitutes for current contract state or transaction evidence.

## Original long-term vision

Founder and community discussions in 2025 described a **Sick Buffalo DAO**, specialized **subDAOs**, broader community node and validator participation, entertainment and gaming, possible **real-world asset (RWA)** projects, and a physical **Sick Buffalo Bar** in Pattaya. The founder's archived April and June 2025 messages and earlier governance experiments document these ideas independently of later narrative summaries. In particular, the Sick Buffalo Bar was discussed by the founder during the April-to-May migration, and community participation in infrastructure and RWAs appeared in June and August development discussions.

These remain **historical ambitions**. A public governance repository or prototype is not evidence that the corresponding DAO, validator program, real-world asset ownership, entertainment venue or physical bar has been deployed. Nothing in this record adds development commitments or launch dates.

## How the project was developed

Joshua Spoehr is **Owner and Founder of SickB Digital LLC, Systems Architect, Developer and Infrastructure Operator**.

AI-assisted engineering has been part of the work since GPT-4. Subsequent AI tools have supported investigation, implementation, test design, documentation and review. They are tools within an owner-directed engineering workflow, not substitutes for onchain receipts, observed service behavior or the founder's responsibility for production systems.

Ethereum, Arbitrum and the open-source work of Offchain Labs made this project technically possible. SickB's work consists of designing, integrating, operating and maintaining its own chain and application stack on those foundations.

## Verification boundaries

This page combines historical community records, the founder's account and separately documented blockchain evidence. The [evidence index](../evidence/INDEX.md) identifies what can already be checked independently and what still needs public source transactions. None of these historical milestones is a claim of audited profitability, third-party security certification or guaranteed investment outcomes.
