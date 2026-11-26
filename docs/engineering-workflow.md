# Engineering process and AI-assisted development

SickB was founded, architected, developed and is operated by **Joshua Spoehr, Founder, Systems Architect, Developer and Infrastructure Operator**. The project was developed while the founder continued full-time work and personally funded infrastructure and development.

As reported from Joshua Spoehr's GitHub activity display on **November 25, 2026**, the preceding one-year period recorded **2,561 GitHub contributions**. This is a dated activity metric, **not 2,561 commits**, merged pull requests, deployed features or a measurement of code quality. The contribution count has not been independently reproduced from a dated GitHub export in this portfolio.

## AI as a development tool

AI assistance has been part of SickB's engineering process beginning with GPT-4 and continuing with later coding and research models. The workflow uses AI to explore documentation, generate and compare implementation options, assist with debugging, create tests, review changes and prepare technical writing.

That does not transfer production authority or technical accountability to an AI system. The founder owns design decisions, decides what is deployed, operates the infrastructure and tests the actual user experience. Tool output is reviewed against contracts, source, chain state and runtime behavior, rather than accepted because it sounds confident.

Review work is separated from changes to production. A documentation investigation should not silently become a deployment, contract modification, wallet action, database edit or server restart. Sensitive configuration and private production source are not copied into public technical examples.

## Evidence-first engineering

A useful engineering record identifies the observed fault, environment, reproduction method, hypothesis, intervention, test result and remaining uncertainty. Where feasible, results are linked to independent public artifacts.

The [MetaMask Mobile case study](metamask-mobile-relay-recovery.md) is an example. It distinguishes Android background network policy observations from a separate controlled relay-channel recovery reproduction. The battery-setting workaround was verified on one physical Android device without changes to SickB production code. A wallet-side repair hypothesis remains an upstream candidate, not a completed patch.

The [Baht Bus transaction evidence](../evidence/bridge-matched-transfers-2026-11-25.md) uses unique transfer IDs and both chain receipts, rather than matching transfers by visual similarity or relying on UI times. It explicitly distinguishes blockchain inclusion from user signing and Ethereum finality.

## Engineering responsibilities

- Design and implementation: founder-directed architecture and changes, assisted by AI tools where useful.
- Verification: chain-specific IDs, receipts, block hashes, reproducible scripts, manual device testing and documented constraints.
- Review: inspect assumptions, test failure modes and label the boundaries of internal and independent checks.
- Publication: remove secrets and personal details; publish the result with enough provenance for a reviewer to reproduce the non-sensitive portion.
- Operations: monitor, reconcile and recover the running chain and applications. Operation is ongoing work, not proof of infallibility.

Independent technical scrutiny and collaboration are welcome, particularly where they can detect mistakes or turn operational experience into knowledge useful to other EVM developers.

No statement in this workflow should be read as a claim that generated code is automatically safe, that all code has been audited, or that private production repositories are available to the public.
