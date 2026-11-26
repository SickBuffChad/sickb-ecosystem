# Evidence still required

This register separates published proof from reported history, internal testing and work that has not yet been independently checked. It does not authorize infrastructure changes or new feature development.

## Evidence backlog

| Topic | Current position | What a public reviewer still needs |
| --- | --- | --- |
| Mainnet launch | Chain ID 5016 and [block-10 transaction](genesis-block-10.md) are documented | Independent RPC receipt reproduction and dated deployment identifiers for parent-chain architecture |
| Orbit parent relationship | Arbitrum One parent and self-operated components are documented | Public Arbitrum One batch-poster and sequencer-inbox contract/transaction references, with dates |
| Bridge history | [Ten sampled exact-ID pairs plus two mobile follow-ups](bridge-matched-transfers-2026-11-25.md) | Historical scan of all deployment eras and supported routes; explicit outstanding and unmatched items |
| Collateral accounting | [Read-only method](reconciliation-method.md) and asset references | Dated three-asset numerical reconciliation with both chain heads and in-flight/fee adjustments |
| Withdrawal fees | Mainnet V2 configuration described as 25 basis points | Live contract query, historical fee periods and actual fee custody accounting |
| Parent-chain posting recovery | Founder reports a 55-day batch-posting backlog and successful recovery rehearsal | Before/after dates, affected batch ranges, onchain postings, derivation checks and completeness evidence |
| Vault | Deployed addresses, founder mainnet tests and 195 reproduced fork checks reported | Deployment receipts, safe test suite provenance, roles/permissions and unresolved security-review scope |
| Mobile MetaMask issue | [Physical-device case study](../docs/metamask-mobile-relay-recovery.md) | Independently sanitized reproduction package and upstream report if or when published; more device coverage |
| Product Zero | Android Google Play internal testing reported | Redacted release screenshots, date/version and tested journeys, without tester identities |
| ChadBot | Product records describe V3 memory and read-only blockchain context | Dated evidence of which integrations are actively running, not just code merged |
| Migration and burns | [Historical record](../docs/history.md) describes a voluntary 1:1 migration and token burn announcements | Public, chain-specific token transfer/burn hashes and a reconciled migration distribution register |
| Cancelled presales | Pinksale and GemPad cancellations and refund paths recorded historically | Public participant-receipt scope and completion accounting; do not imply a full independent refund audit |
| Whitepaper | [Project-hosted PDF](https://sickb.io/whitepaper.pdf) identified | Version/date crosswalk mapping historical proposals to currently deployed systems |

## Matters for founder approval

Before the history and economics sections can be presented as independently verified, the founder should approve the wording and supply public-safe transaction references for the cancelled offerings, burns and the original migration if those are to be described with finality.

Current mainnet fee claims need a live contract query and reconciliation with older explorer copy that has displayed 0.1% while current mainnet V2 product configuration describes 0.25%.

The project site has been seen serving a testnet scan surface from the /scan route. The README should not use that route as a verified SickB mainnet explorer until the owner confirms the intended public mainnet URL. The project /explorer route is linked with this limitation.

Any collateral, total bridge volume, transaction throughput or uptime number should be supported by a dated read-only artifact rather than a token-price or market-cap snapshot.

## Review boundaries

The public documentation may invite external assessment. It must not claim that third-party security certification has occurred or disclose wallet identities, private keys, operator addresses not already publicly documented, protected infrastructure configuration or source files from private production repositories.

The [evidence index](INDEX.md) is the reviewer entry point. This list is an evidence and editorial backlog, not a new product roadmap.
