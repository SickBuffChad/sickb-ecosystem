# Evidence still required

This register separates published proof from reported history, internal testing and work that has not yet been independently checked. It does not authorize infrastructure changes or new feature development.

## Evidence backlog

| Topic | Current position | What a public reviewer still needs |
| --- | --- | --- |
| Mainnet launch | Chain ID 5016 and [block-10 transaction](genesis-block-10.md) are documented | Independent RPC receipt reproduction and dated deployment identifiers for parent-chain architecture |
| Orbit parent relationship | Arbitrum One parent and self-operated components are documented | Public Arbitrum One batch-poster and sequencer-inbox contract/transaction references, with dates |
| Bridge history | [Ten sampled exact-ID pairs plus two mobile follow-ups](bridge-matched-transfers-2026-11-25.md) | Historical scan of all deployment eras and supported routes; explicit outstanding and unmatched items |
| Collateral accounting | [Read-only method](reconciliation-method.md) and asset references | Dated three-asset numerical reconciliation with both chain heads and in-flight/fee adjustments |
| Withdrawal fees | The mainnet website configuration specifies 25 basis points; see [actual registry ABI and query method](reconciliation-method.md) | Effective V2 withdrawal contract setting still needs a correctly scoped live onchain read or a complete gross/net receipt reconciliation |
| Parent-chain posting recovery | Founder reports a 55-day batch-posting backlog and successful recovery rehearsal | Before/after dates, affected batch ranges, onchain postings, derivation checks and completeness evidence |
| Vault | Deployed addresses, founder mainnet tests and 195 reproduced fork checks reported | Deployment receipts, safe test suite provenance, roles/permissions and unresolved security-review scope |
| Mobile MetaMask issue | [Physical-device case study](../docs/metamask-mobile-relay-recovery.md) | Independently sanitized reproduction package and upstream report if or when published; more device coverage |
| Product Zero | Android Google Play internal testing reported | Redacted release screenshots, date/version and tested journeys, without tester identities |
| ChadBot | Product records describe V3 memory and read-only blockchain context | Dated evidence of which integrations are actively running, not just code merged |
| Migration and burns | [Founder archive evidence](historical-provenance.md) includes September 2025 burn announcements and a later **reported aggregate of 1,484,000,000 SICKB (59.36% of the original 2.5 billion)**. This aggregate is a verification target, not an independently established chain finding | Reconstruct complete chain-1 SICKB ERC-20 Transfer logs, recipient addresses and supply semantics; separately index legacy-chain burns and the complete 1:1 migration ledger before accepting the aggregate |
| Cancelled presales | Founder archive documents PinkSale closure and a participant refund acknowledgement, plus GemPad closure and instructions for refunds | Identify both sale contracts, deposits, claims and refunds; confirm whether **all participants received full ETH refunds** using the complete transaction ledger before asserting this as verified |

## Matters for founder approval

Founder and community records have been separated from public chain receipts in the [historical provenance register](historical-provenance.md). Before presenting the reported aggregate burns or complete refunds as verified, reconcile them against public Ethereum transfer logs, sale contract receipts and the original migration distribution roster.

The website configuration supports **25 bps** for mainnet withdrawals. The independent contract-level check must use the verified V2 ABI and route registry, not the unsupported `withdrawFeeBps()` getter. Older 0.1% explorer copy should not be cited as current mainnet configuration.

The intended [SickB mainnet explorer](https://sickb.io/explorer) displays **SickB Chain mainnet, chain 5016**, with live block and transaction listings. The public page's network label was inspected; independent JSON-RPC `eth_chainId` is available as a separate check in [developer start](../docs/developer-start.md).

Any collateral, total bridge volume, transaction throughput or uptime number should be supported by a dated read-only artifact rather than a token-price or market-cap snapshot.

## Review boundaries

The public documentation may invite external assessment. It must not claim that third-party security certification has occurred or disclose wallet identities, private keys, operator addresses not already publicly documented, protected infrastructure configuration or source files from private production repositories.

The [evidence index](INDEX.md) is the reviewer entry point. This list is an evidence and editorial backlog, not a new product roadmap.
