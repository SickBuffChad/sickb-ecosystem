# Engineering evidence index

This is the entry point for reviewers who want transaction hashes, dates, contract addresses and the limits of what has been established. The public repository is an engineering portfolio, not a replacement for onchain verification or a completed independent security audit.

## Evidence inventory

| Topic | Published material | Evidence currently available | Gap or qualification |
| --- | --- | --- | --- |
| Founding transaction, June 3, 2026 | [Block-10 dedication and receipt](genesis-block-10.md) | Chain 5016 block, transaction hash, genesis contract, message and message hash | Original receipt was provided from founder records; readers can query RPC independently |
| Orbit mainnet architecture | [Architecture and products](../docs/architecture-products.md), [developer network settings](../docs/developer-start.md) | Chain ID, public RPC, deployment epoch, documented node/client roles | External parent-chain deployment identifiers and a dated complete topology evidence package remain to be published |
| Ethereum to SickB bridge | [Baht Bus architecture](../docs/baht-bus-bridge.md), [ten matched transfers](bridge-matched-transfers-2026-11-25.md) | Exact deposit IDs, L1/L3 transaction hashes and inclusion timestamps | Ten-transfer set is a selected test sample, not a full-history coverage claim |
| SickB to Ethereum bridge | [Matched transfers](bridge-matched-transfers-2026-11-25.md) | Exact withdrawal IDs, release calldata matches, ERC-20 transfer logs and successful Ethereum receipts | Full-history release matching and all-route outstanding reconciliation remain pending |
| Post-workaround mobile tests | [MetaMask case study](../docs/metamask-mobile-relay-recovery.md), [two further matches](bridge-matched-transfers-2026-11-25.md#post-workaround-physical-device-follow-up-two-additional-transfers) | Founder-identified mobile journeys with 22-second deposit and 59-second withdrawal inclusion-to-inclusion times | Does not show wallet tap-to-completion or causal improvement in chain latency |
| Collateral and wrapped supply | [Read-only reconciliation method](reconciliation-method.md) | Contract/asset references and a repeatable measurement procedure | No independently completed dated three-asset numerical reconciliation is published |
| Parent-chain batch-posting recovery | [Recovery evidence requirements](verification-gaps.md) | Founder records of a 55-day posting backlog, rehearsal and restoration | Arbitrum One posting transactions, timeline and full reconciliation not yet packaged |
| Vault contracts and tests | [Contract address list](../docs/developer-start.md), [product boundaries](../docs/architecture-products.md) | Three public contract addresses; founder records of 195 passing fork checks and deployed-code matching | Publish safe test-run provenance, deployment transactions and independent review scope; no full third-party audit |
| Android Product Zero | [Current product status](../docs/architecture-products.md) | Founder-operated Google Play internal testing and mainnet user journeys | Redacted Play internal release evidence and broader device QA not yet included |
| ChadBot V3 | [Current product status](../docs/architecture-products.md) | Historical memory, web research and read-only blockchain capabilities documented in project records | Deployed integrations and scheduled/proactive services should be validated separately |
| Early migration, presales, burns | [Historical account](../docs/history.md) | Dated contemporaneous community records and founder reports | Publish per-chain token burn transactions, refunded-sale receipts and migration distribution ledger before claiming complete independent reconciliation |

## Known onchain references

The reference addresses below are chain-specific; verify contract code, transaction receipts and state with a fresh read-only RPC before drawing conclusions.

| Chain | Contract or record | Reference |
| --- | --- | --- |
| SickB 5016 | Genesis dedication | Block 10, tx 0xaf525995884b1c6f0b0086ff5554ec952523d095ce2dbc3f66d213954da99ab8 |
| SickB 5016 | SickBGenesis | 0x86734D2fc365231b8502254e08aE635Ae949DA0A |
| Ethereum 1 | Baht Bus lockbox | [0x86734D2fc365231b8502254e08aE635Ae949DA0A](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A) |
| SickB 5016 | V2 deposit minter | 0xb8a3f62407df7d605915ff7dbd2301cf0bdf557d |
| SickB 5016 | V2 withdrawal bridge | 0xd5583d37a84fB3ffDa3395334F3E5c714Ffb64f7 |
| SickB 5016 | Vault Devices | 0x483D8267cd21c3733d21e27be063163B2fA7beDD |
| SickB 5016 | Vault Executor | 0xfE329B2Fe4a5b1cCb945abb965a538E19590d2a9 |
| SickB 5016 | Vault Factory | 0x443f069f778F0080Bd704aD9212D9232441A2818 |

The same hexadecimal contract address occurs as SickBGenesis on SickB Chain and as the lockbox on Ethereum. An address alone is insufficient to identify a contract.

See [developer start](../docs/developer-start.md) for the supported asset tokens and additional onchain references.

## What the matched samples establish

The [November 25 sample](bridge-matched-transfers-2026-11-25.md) contains five latest indexed L3 deposit mints and five latest L3 withdrawal initiations selected at the time of inspection, all matched to Ethereum by exact bridge IDs. Across that selected sample, the median source-inclusion to destination-inclusion time was 45 seconds and 7 of 10 completed in under 60 seconds. These are not representative of all mainnet traffic and do not establish Ethereum consensus finality.

Two later user-identified post-workaround mobile tests also have cross-chain matches: 9,351.5625 SICKB Ethereum to SickB in 22 seconds and 997,500 SICKB net SickB to Ethereum in 59 seconds. The bridge worked as designed when the Android wallet communication obstacle was removed; the evidence does not show the workaround reduced underlying bridge settlement latency.

The L1 matches were checked for successful receipts and matching canonical block hashes. The L3 side of those matching runs used a confirmed activity indexer; fresh independent receipt checks for each L3 event were not included in the same script. These are verifiable proof references, not audit certification.

## Accounting and operating claims

Token market capitalization, if referenced in older community posts, is not the same as money invested, protocol revenue, locked collateral, corporate spending, net asset value or bridge economic activity. No market-cap figure is used in this portfolio as a proxy for financial resources committed to the ecosystem.

A backing assertion requires a dated Ethereum lockbox balance and SickB wrapped supply for each asset, plus in-flight transfers, fee reserves, contract-era coverage and a common time cutoff. See [reconciliation method](reconciliation-method.md).

The parent-chain posting incident also requires evidence for the exact batches involved, the stop and recovery windows, and subsequent publication on Arbitrum One. Until then it is a founder-reported operations case, not an externally certified availability statistic.

## Source quality and contribution

Evidence is labeled as one of the following: a public onchain artifact, an owner-operated read-only measurement, an internal engineering result, or a historical founder/community report. Do not silently promote the latter categories into independent audit findings.

Missing evidence, correction requests and reproducible read-only checks can be proposed through the public repository review process. Read [verification gaps](verification-gaps.md) before proposing a new performance, collateral or security claim.
