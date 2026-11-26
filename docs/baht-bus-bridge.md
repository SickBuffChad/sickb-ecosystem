# Baht Bus Bridge: SickB's native asset bridge

**Status:** Mainnet bridge in operation · **Network:** SickB Chain (Arbitrum Orbit AnyTrust L3, chain ID `5016`) · **Parent:** Arbitrum One · **Canonical asset origin:** Ethereum mainnet

## Why we built it

SickB is a blockchain ecosystem, not a general-purpose cross-chain messaging protocol. Once we built our own Arbitrum Orbit L3, we needed a way to bring Ethereum assets into that environment and return them to Ethereum without making users assemble a separate set of infrastructure services.

**Baht Bus is the bridge built specifically for that need.** It is a SickB-operated system rather than an integration of a third-party messaging or bridge provider. Its role is to connect Ethereum liquidity to SickB's onchain products: trading, smart-contract Vaults, Social payments, and future applications.

The objective was practical: **move supported assets between Ethereum and SickB, make the user experience straightforward, and give the destination wallet native SickB gas where the bridge design requires it.**

The system was developed and exercised through multiple iterations on an Ethereum Sepolia / Arbitrum Sepolia / SickB L3 test environment before the June 2026 mainnet launch. The original bidirectional testnet bridge was documented as working in February 2026. The design subsequently evolved to support multiple assets and additional operational checks.

## What it connects

**Two distinct relationships, not an Ethereum → Arbitrum One → SickB asset-bridge route:**

```text
ASSET BRIDGE (Baht Bus)                     ROLLUP / SETTLEMENT PARENT
----------------------------------          --------------------------------
Ethereum mainnet (L1)                      Ethereum mainnet (L1)
  canonical assets and lockbox                 │
            ⇅                                  ▼
  bridge events, verification,              Arbitrum One (L2 parent)
  signed attestations and relayers               │
            ⇅                                     ▼
SickB Chain (L3, id 5016)                 SickB Chain (Orbit AnyTrust L3)
  wrapped assets + native gSICKB                 │
  DEX / Vaults / Social                          └─ sequencer batches / DA
```

**Asset movement is directly between the Ethereum lockbox and SickB's L3 contracts.** Arbitrum One underpins SickB's Orbit parent-chain architecture; it is **not** an intermediate asset-bridge custody or release step in the current mainnet Baht Bus routes.

**Operator-owned infrastructure:** SickB runs its own Ethereum execution client (**Reth**) and consensus client (**Lighthouse**), an **Arbitrum One Nitro node**, its **SickB L3 sequencer**, and an **AnyTrust data-availability committee**. These operate alongside chain-specific bridge processing, auditing and separately operated verification/attestation services. Running these nodes reduces reliance on third-party RPC providers; it does not imply independence from Ethereum or Arbitrum consensus, or that the network is fully decentralized.

The currently supported principal routes are **SICKB, WETH and USDC**. A registry associates their canonical L1 tokens with L3 wrapped assets and governs whether each direction is enabled and within configured limits. Bridge capacity is ultimately constrained by available collateral, enabled routes and operational safeguards, not an advertised unlimited-liquidity guarantee.

**Native gas is a separate asset from bridged wSICKB:** SickB uses **gSICKB** for L3 transaction fees. The Baht Bus gas-sponsorship system is designed to make supported bridge operations and subsequent L3 interactions usable without an additional manual gas-funding journey.

## Ethereum → SickB: deposit and onboarding

At the architectural level:

1. The user submits the supported canonical asset to the Ethereum-side lockbox using the **mainnet nonpayable, three-argument deposit function**; the normal deposit does **not** attach an ETH bridge surcharge or a paid retryable ticket. The wallet still pays Ethereum transaction gas.
2. Cross-chain processing identifies the deposit and performs route and transaction checks before authorizing minting on SickB.
3. The L3 finalization operation delivers the corresponding wrapped asset and, for the gas-sponsored design, delivers a native gas ticket to the SickB wallet.

**The wrapped-asset mint and native-gas sponsorship are atomic within the L3 finalization transaction.** If the required combined L3 operation reverts, neither of those L3 effects is committed. Deposit IDs and processing status are used to prevent duplicate finalization.

That guarantee is **local to the destination-chain transaction**. It does not mean that a prior Ethereum lock is automatically rolled back by a later L3 failure; cross-chain delivery, reconciliation and recovery remain separate concerns.

## SickB → Ethereum: withdrawal and release

The mainnet V2 design uses a similarly coordinated L3 operation:

1. The user initiates a withdrawal against the enabled registry route.
2. In **one SickB L3 transaction**, the contract receives the wrapped tokens, burns the net withdrawal amount, and requests a native gSICKB gas ticket for the originating wallet.
3. **If the gas sponsorship step fails, the entire L3 withdrawal transaction reverts.** The transfer, burn and withdrawal record do not partially commit.
4. A successful L3 transaction emits a withdrawal record indicating gas delivery.
5. A **separate read-only verification and attestation path** checks that the L3 withdrawal exists, the token route is valid and enabled, the required gas-delivery flag is present, and the Ethereum withdrawal has not already been released.
6. A transaction-submitting relayer presents the signed authorization to the Ethereum lockbox, which processes the release subject to its onchain rules.

The design intentionally separates **verification / attestation** from **transaction submission**. The relayer cannot treat an arbitrary L3 event as sufficient authorization to release Ethereum collateral.

## The meaning of “atomic”

**The term is important, and we use it precisely.**

- **Inbound:** asset minting and the associated native-gas gift execute together or revert together **on SickB L3**.
- **Outbound:** wrapped-token withdrawal/burn and the associated native-gas gift execute together or revert together **on SickB L3**.
- **Cross-chain:** Ethereum settlement and SickB settlement happen in **different transactions on different chains**. The entire end-to-end movement is **not** a single atomic Ethereum-plus-L3 transaction.

This distinction is why the architecture also includes route validation, unique event identifiers, processed/released checks, independent attestation, reconciliation and operational recovery procedures.

A cross-chain operation can remain **pending** when a subsequent step is delayed, even if an individual onchain step has succeeded. Atomic L3 operations reduce partial-state risks **inside those L3 transactions**; they do not remove every possible delay, failure mode or recovery obligation across networks.

## Practical security and operating properties

| Property | How the architecture addresses it |
| --- | --- |
| Canonical-asset backing | Ethereum-side locked assets back the corresponding wrapped assets on SickB |
| Token identification | Registry links permitted L1 assets to their L3 representations and route controls |
| Replay / double-release controls | Deposit and withdrawal IDs, processed-state and released-state checks |
| L3 onboarding | Native gSICKB sponsorship incorporated into supported bridge actions |
| Withdrawal release authorization | Read-only verification, a separate signed attestation and Ethereum contract validation |
| Operational resilience | Dedicated relay, verifier and auditor functions; monitored processing and reconciliation |
| Fees and reserves | Mainnet V2 withdrawal fee configured at **25 basis points (0.25%)** in the product configuration; wrapped-token fee reserves are designed to remain backed by Ethereum collateral |

**Fee settings are governed by live contract configuration**, so current onchain parameters, not this document, are authoritative at transaction time. The potential transfer of protocol-owned reserves to future DAO/multisig stewardship is a **roadmap objective**, not a claim of current DAO custody.

## Experience and evidence

**Fee clarification:** The historical `0.00375 ETH` deposit-fee setting was an **unimplemented placeholder**, not an Ethereum deposit charge. It must not be counted as realized revenue or included in historical bridge-performance costs.

**Evidence status:** The November 7, 2026 archived activity-feed probe inspected SickB blocks 201,011–300,991 and observed seven L3 withdrawal initiations, with zero deposit mints in that bounded window. These observations are not a full-history inventory and do not independently establish Ethereum releases. The existing activity feed is a useful starting point for a separate read-only, bridge-ID-matched historical dataset.

The founder has operated the bridge for approximately five months since mainnet deployment in June 2026 and reports successful real-asset transfers in both directions without an observed failed settlement in that period. This is **operational experience**, not a claim that all conceivable failures have been excluded or that transfers have a guaranteed completion time.

Representative transfers have completed in tens of seconds, but timing depends on the underlying chains, confirmations, transaction inclusion and processing conditions.

Public reviewers can inspect the Ethereum-side [lockbox on Etherscan](https://etherscan.io/address/0x86734D2fc365231b8502254e08aE635Ae949DA0A), the [matched cross-chain transaction receipts](../evidence/bridge-matched-transfers-2026-11-25.md), and the [read-only collateral reconciliation method](../evidence/reconciliation-method.md). The ten selected November 25 transfer pairs, plus two later mobile follow-ups, are documented with exact bridge IDs and chain-specific transactions. A complete historical reconciliation and independent security audit have not been published. The [evidence index](../evidence/INDEX.md) identifies those gaps.

## How this differs from a general-purpose interoperability protocol

LayerZero and similar frameworks provide interoperability tooling that applications and chains can integrate. **Baht Bus was not designed as a universal substitute for those systems.** SickB is itself the operating blockchain; Baht Bus is the ecosystem-specific bridge we engineered to serve it.

We are not claiming that gas delivery, cross-chain messaging or bridge safety mechanisms are unique inventions. The achievement is **building, integrating and operating these components as a coherent bridge for an independently run Orbit L3**.

Its architecture may inform future collaborations or integrations with other chains, but that is a **possible future direction**, not a product offered today.

---

*Public architecture overview · November 25, 2026. Intentionally excludes private operational configuration, signing infrastructure, security-sensitive implementation details and proprietary source. This document is technical context, not a formal audit.*
