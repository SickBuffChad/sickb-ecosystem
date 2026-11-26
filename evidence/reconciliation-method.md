# Read-only collateral and wrapped-supply reconciliation

This page describes how to gather and check backing evidence for the supported Baht Bus assets. It does not contain a completed three-asset audit or a claim of independently certified reserves.

## Why a dated calculation matters

The Ethereum lockbox holds canonical tokens, while SickB Chain contains corresponding wrapped tokens. Deposits and withdrawals are completed through different chain transactions. A reading taken at one Ethereum block and another taken at an unrelated SickB timestamp may disagree even when the bridge is operating correctly.

A useful backing test must include the chain, contract version, exact block numbers and hashes, a common UTC cutoff, pending cross-chain movements and any fee-bearing wrapped tokens retained by the protocol.

Supply held in a protocol-owned wallet is still part of an ERC-20 total supply unless actually burned. Do not subtract it from supply merely because the project controls it.

## Known public contract references

| Asset | Ethereum canonical ERC-20 | SickB wrapped ERC-20 | Decimals |
| --- | --- | --- | ---: |
| SICKB | 0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3 | 0x9b4d4f0ce03CB60De813c13EfBcA153F1418ac24 | 18 |
| WETH | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2 | 0xdf482f642630aed49fa339fce8a83a019dd3fc7c | 18 |
| USDC | 0xA0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 | 0x810D12ada35e961a5249da163af299374c2e772f | 6 |

Ethereum lockbox: 0x86734D2fc365231b8502254e08aE635Ae949DA0A (chain 1). These are the current V2 configuration references documented in the portfolio; account for historical deployments or alternate custody paths separately when making full-period claims.

## Suggested measurement procedure

1. Choose a UTC cutoff and find the last confirmed Ethereum block and SickB block at or before that cutoff. Record both block numbers, hashes and timestamps.
2. Read the balance of each canonical ERC-20 held by the Ethereum lockbox using balanceOf(lockbox) at the selected Ethereum block.
3. Read totalSupply() of each corresponding wrapped ERC-20 on SickB at the selected SickB block. Include wrapped balances in the protocol fee reserve in total supply.
4. Index the Ethereum Deposit events and SickB finalizeDeposit transactions by their exact deposit IDs up to the cutoff. Identify locks not yet minted and any unmatched mints.
5. Index SickB WithdrawInitiated events and Ethereum release transactions by exact withdrawal ID. Identify burned but not yet released net amounts, and distinguish gross input from the withdrawal fee.
6. Check onchain processed/released flags where available, validate successful receipts and block hashes, and account for each contract epoch, upgrade or migration.
7. Reconcile any difference and retain the transaction-level ledger. A nonzero difference is a finding to investigate, not proof of either solvency or insolvency without its component accounting.

## Read-only example with Foundry cast

Use a trusted Ethereum RPC of your choice for the first command. Do not commit its API key. The second command uses the published SickB mainnet read-only RPC. Supply historical block numbers aligned to a common UTC cutoff.

~~~bash
# On Ethereum chain 1: canonical SICKB held by the lockbox.
cast call 0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3 \
  'balanceOf(address)(uint256)' \
  0x86734D2fc365231b8502254e08aE635Ae949DA0A \
  --rpc-url "$ETHEREUM_RPC" \
  --block "$L1_BLOCK"

# On SickB chain 5016: total minted wrapped SICKB.
cast call 0x9b4d4f0ce03CB60De813c13EfBcA153F1418ac24 \
  'totalSupply()(uint256)' \
  --rpc-url https://rpc-mainnet.sickb.io \
  --block "$L3_BLOCK"

# Query the actual bridge registry's getToken(address) ABI for the
# SICKB route. This reports the registry's bpsFee field, not necessarily
# a separate V2 withdrawal-contract fee or the user's realized fee.
cast call 0xBde1C3EB2711dB702c9E30504f16fBb95C3962Db \
  'getToken(address)((address,address,string,uint8,bool,bool,bool,uint256,uint256,address,uint256,uint256,uint256,uint256,uint256,bool,bool,bool,bool,uint256))' \
  0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3 \
  --rpc-url https://rpc-mainnet.sickb.io
~~~

Run the corresponding balance/supply commands for WETH and USDC, observing their decimals. This example prints raw integer units and does not by itself generate an audited reconciliation.

The mainnet website configuration specifies **25 basis points (0.25%)** for withdrawals. The function `withdrawFeeBps()` previously suggested in this document was not supported by the V2 ABI available for this review and has been removed. The bridge registry's actual `getToken(address)` ABI includes a `bpsFee` route field, but that field must not be conflated with the V2 withdrawal contract's effective fee without reviewing its own implementation or an exact gross/net onchain receipt. A live, contract-level 25 bps reading has **not** been independently reproduced in this documentation update. The transaction evidence and website configuration support the stated product setting, not an independently measured live getter.

The historical 0.00375 ETH deposit surcharge appearing in some older configurations was an unimplemented placeholder, not a realized Ethereum lockbox charge. Do not include it in bridge revenue.

## How to publish a usable result

A reproducible snapshot should include:

| Required field | Description |
| --- | --- |
| Sample cutoff UTC | Common comparison time |
| L1 / L3 blocks | Number, hash, timestamp and confirmation basis for each chain |
| Contract version | Lockbox, minter, withdrawal contract and supported route addresses |
| Canonical lock | Exact raw token balance held on L1 |
| Wrapped supply | Exact raw totalSupply on SickB including protocol-held tokens |
| In-flight liabilities | Unfinalized deposits and initiated but unreleased withdrawals |
| Fee treatment | Gross withdrawal amount, net burn/release, protocol-held fee asset |
| Reconciliation residual | Exact raw amount, unit decimals and any unresolved differences |
| Receipts | Full source and destination transaction hashes, IDs and status |

The sample [bridge receipt evidence](bridge-matched-transfers-2026-11-25.md) demonstrates transaction matching. It is not a substitute for a full collateral and circulating-supply ledger. No unsupported numerical collateral or bridge volume claims should be published.
