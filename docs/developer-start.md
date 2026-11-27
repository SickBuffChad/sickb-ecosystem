# Developer start: SickB mainnet

This is part of SickB Digital LLC's current official engineering documentation and public technical reference. It is for developers evaluating SickB Chain or planning a documented integration. No private repository, infrastructure access, paid RPC key or operator credentials are required to inspect public blockchain state.

## Network configuration

| Setting | Value |
| --- | --- |
| Network | SickB Chain mainnet |
| Chain ID (decimal) | 5016 |
| Chain ID (hexadecimal) | 0x1398 |
| Technology | Arbitrum Orbit AnyTrust L3 |
| Parent | Arbitrum One (chain 42161) |
| Native gas currency | gSICKB |
| Public read-only RPC | https://rpc-mainnet.sickb.io |
| Mainnet explorer | [SickB Scan](https://sickb.io/explorer), identified as chain 5016 |
| Ethereum canonical asset chain | Ethereum mainnet (chain 1) |

These are the production SickB L3 settings. SickB testnet uses a different chain ID and must not be confused with mainnet. Check RPC responses and the exact chain ID before signing a transaction. The explorer interface is project-operated; use blockchain RPC and the chain-specific transaction hashes to cross-check important results.

### Minimal read-only verification

The examples below use curl and do not require a wallet.

~~~bash
# Confirm the RPC is reporting SickB mainnet, chain 5016 (0x1398).
curl -sS https://rpc-mainnet.sickb.io \
  -H 'content-type: application/json' \
  --data '{"jsonrpc":"2.0","id":1,"method":"eth_chainId","params":[]}'

# Read the documented genesis dedication block.
curl -sS https://rpc-mainnet.sickb.io \
  -H 'content-type: application/json' \
  --data '{"jsonrpc":"2.0","id":2,"method":"eth_getBlockByNumber","params":["0xa",false]}'
~~~

The reported chain ID must be 0x1398. For block 10, compare the returned hash with [the canonical founding receipt](../evidence/genesis-block-10.md). Do not assume a response from a website or RPC is an independent security audit.

Foundry users can also use:

~~~bash
cast chain-id --rpc-url https://rpc-mainnet.sickb.io
cast block 10 --rpc-url https://rpc-mainnet.sickb.io
~~~

## Contracts and supported assets

All addresses must be interpreted together with their chain. This portfolio reports the following public contract references from the project's V2 mainnet configuration and historical receipt work; developers should verify code and contract state against the applicable chain before integration.

### Ethereum mainnet, chain 1

| Reference | Address |
| --- | --- |
| UniversalLockBoxL1 | 0x86734D2fc365231b8502254e08aE635Ae949DA0A |
| Canonical SICKB | 0x8172e2Ff7009483ff98c24Bd639C8078caCED9a3 |
| Canonical WETH | 0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2 |
| Canonical USDC | 0xA0b86991c6218b36c1d19d4a2e9eb0ce3606eb48 |

The lockbox can be inspected at [Etherscan](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A).

### SickB Chain, chain 5016

| Reference | Address |
| --- | --- |
| V2 deposit minter | 0xb8a3f62407df7d605915ff7dbd2301cf0bdf557d |
| V2 withdrawal bridge | 0xd5583d37a84fB3ffDa3395334F3E5c714Ffb64f7 |
| Wrapped SICKB | 0x9b4d4f0ce03CB60De813c13EfBcA153F1418ac24 |
| Wrapped WETH | 0xdf482f642630aed49fa339fce8a83a019dd3fc7c |
| Wrapped USDC | 0x810D12ada35e961a5249da163af299374c2e772f |
| SickbVaultDevices | 0x483D8267cd21c3733d21e27be063163B2fA7beDD |
| SickbVaultExecutor | 0xfE329B2Fe4a5b1cCb945abb965a538E19590d2a9 |
| BotVaultFactory | 0x443f069f778F0080Bd704aD9212D9232441A2818 |
| SickBGenesis (block 10) | 0x86734D2fc365231b8502254e08aE635Ae949DA0A |

The genesis contract and Ethereum lockbox have the same hexadecimal address on different chains. They are different contracts. Never use a contract address without its chain ID.

### Code presence check

~~~bash
cast code 0xb8a3f62407df7d605915ff7dbd2301cf0bdf557d \
  --rpc-url https://rpc-mainnet.sickb.io

cast code 0xd5583d37a84fB3ffDa3395334F3E5c714Ffb64f7 \
  --rpc-url https://rpc-mainnet.sickb.io
~~~

A nonempty code response only establishes contract code exists at the queried address. It does not establish current roles, route controls, safety or audited provenance. For version-sensitive integration, retrieve ABI and live registry parameters from verified source or the relevant public contracts.

## What to expect from Baht Bus

Baht Bus supports SICKB, WETH and USDC between the Ethereum lockbox and SickB L3 wrapped tokens. The design includes native gas sponsorship in the supported bridge workflows. Sponsorship is subject to route and ticket conditions, not a guarantee of arbitrary free transactions.

The asset bridge is Ethereum to SickB directly at the asset-service level. Arbitrum One provides the Orbit parent relationship, not an intermediate Baht Bus asset hop.

Read [Baht Bus architecture](baht-bus-bridge.md), then inspect [matched transaction pairs](../evidence/bridge-matched-transfers-2026-11-25.md). Each published pair includes a source and destination transaction reference. Ethereum-to-SickB inclusion-to-inclusion timing is not the same thing as wallet approval latency or Ethereum consensus finality.

## Available integration work

Developers can evaluate standard EVM interactions, read-only RPC indexing, contract/event decoding, supported DEX integrations and consumer wallet experiences. The published material is intended to let collaborators assess compatibility and propose specific work. It is not a promise of a public API with a stability SLA.

When testing a transaction:

1. Confirm the target chain and token contract address.
2. Read the contract ABI and current route or permission status rather than relying on an old screenshot.
3. Start with a small self-controlled test amount and record its transaction hashes.
4. Match each cross-chain transfer by its unique bridge ID, not by amount and timestamp proximity.
5. Reconcile pending or failed wallet interactions before submitting again.

## Public versus private

This repository contains documentation, published transaction references, high-level architecture and selected engineering evidence. It does not include the production application source tree, contract deployment keys, private server files, signing infrastructure, internal database contents, privileged API tokens or unreviewed customer data.

There is currently no explicit license granting reuse of private SickB production code. Do not assume that public documentation makes those systems open source. Proposed public contributions should concern documentation improvements, reproducible non-sensitive test cases, compatibility reports and vetted integration proposals.

Continue to [evidence and verification](../evidence/INDEX.md), [engineering workflow](engineering-workflow.md) and [collaboration](collaboration.md).
