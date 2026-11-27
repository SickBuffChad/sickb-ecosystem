# Historical source provenance

This register distinguishes original founder and community records from independently reproducible onchain evidence. The historical messages were preserved in SickB's internal community archive and reviewed for this documentation update. The archive message IDs below are research identifiers, not publicly accessible links or a substitute for a blockchain receipt.

This repository, maintained for SickB Digital LLC, is the current official SickB engineering documentation and public technical reference. Current application status and deployed contract configuration should be checked in the [architecture](../docs/architecture-products.md), [developer guide](../docs/developer-start.md), and [engineering evidence index](INDEX.md).

## Source register

| History | Original record or public source | What it supports | Independent verification still needed |
| --- | --- | --- | --- |
| Ethereum SICKB token | [Ethereum SICKB ERC-20 contract](https://etherscan.io/token/0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3) | The chain-specific token address can be checked on Ethereum | Historical supply and holder changes must be reconstructed at the relevant blocks |
| Voluntary migration, April to May 2025 | Founder migration announcement #26694; migration channel #26688; recipient confirmation #28387; archived migration transaction roster | Migration window, manual 1:1 distribution process, evidence that at least one participant received tokens | Complete legacy sends, Ethereum recipient receipts and totals for all participants |
| PinkSale discontinuation, June 18, 2025 | Founder cancellation #49084; participant refund acknowledgement #49098 | Presale closure and one reported successful refund | Reconstruct all ETH contributions and all individual refunds before asserting every participant received the full amount |
| GemPad discontinuation, November 26, 2025 | Founder announcement #55794 instructing refunds through the sale page | Presale cancellation and communicated refund procedure | Onchain sale contract, contribution records, withdrawal/refund transactions and completeness check |
| September 2025 burns | Founder/community messages #53877, #53882 (September 18), and #54117 (September 26) | Two contemporaneously reported 250-million-token Ethereum-era burns | Receipt and ERC-20 `Transfer` event checks against the Ethereum token, plus other burn events for the aggregate |
| Later cumulative burn statements | Founder/community archive #56315; later founder statement #60382 | A larger historical burn total was reported by the project | Verify all events, destination addresses, cumulative sums, chain separation and supply terminology before publishing a verified aggregate |
| December 2025 lost phone | Founder-authored accounts #56408 and #61334 | Lost device access and wallet-recovery difficulties, which informed later Vault design choices | Wallet-level holdings or permanently inaccessible balances, if any numerical amount is to be published |
| DAO, validators, RWAs and community venue | Founder messages #29263 and #29270 (community venue); #49836 (long-term ecosystem ideas); #52800 (validator/governance concept) | Earlier founder aspirations, independent of later narrative documents | Deployed contract references or operating records before claiming an idea was implemented |
| SickB Chain founding dedication | [Mainnet chain 5016 block 10](genesis-block-10.md), transaction `0xaf525995884b1c6f0b0086ff5554ec952523d095ce2dbc3f66d213954da99ab8` | Original founder dedication, chain-specific transaction and message hash | Independently reread receipt and contract from the public SickB RPC |
| Mainnet bridge operation | [Matched cross-chain receipts](bridge-matched-transfers-2026-11-25.md) | Exact-ID Ethereum/SickB samples and published inclusion timings | Extend sample to full history before presenting historical reliability statistics |

## How to check historical economic claims

For an Ethereum burn, inspect the exact chain-1 token address, the transaction receipt status, the token's `Transfer` event(s), the recipient's identity and accessibility, raw amounts with 18 decimals, and the contract's `totalSupply()` semantics. A transfer to a dead address can remove spendable circulation without reducing contract total supply. Keep original Pepe Unchained-era tokens separate from the later Ethereum ERC-20.

For presale refunds, obtain the original sale contract and participant contribution ledger, then match each refund transaction and amount in ETH. A cancellation announcement and a single confirmed refund are not proof of complete reimbursement.

For the 2025 migration, match each eligible legacy transfer with the Ethereum replacement transfer by the recorded recipient and amount. The present public portfolio does not disclose individual participant records or unpublished wallet rosters.

## Evidence boundaries

The original community archive is maintained privately by SickB and is not offered as public verification. Message numbers are provenance aids, not invented public citations. A chain receipt is distinct from an archived founder statement. See the [verification backlog](verification-gaps.md) for pending economic totals.

Original chain records and the [block-10 dedication](genesis-block-10.md) remain unmodified.
