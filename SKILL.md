---
name: canton-app-builder
description: Build and evolve full-stack Canton applications across DAML contracts, backend APIs, web interfaces, wallet integrations, and deployment configuration. Use for lending, credit, settlement, tokenization, funding, and multi-party workflows, including Quickstart extraction and upgrade planning. Preserve the repository's stack and discover its actual versions before implementation.
---

# Canton App Builder

Deliver the smallest complete business workflow using the target repository's conventions. Keep reusable guidance here and project decisions, version evidence, and operational instructions in the target repository.

## Workflow

1. **Inspect before choosing.** Read applicable repository instructions, Git status and ownership maps; find canonical sources rather than modifying a legacy Quickstart copy. Inspect manifests, locks, contract packages, relevant source, tests, CI and deployment files. Discover installed tools and distinguish configured, installed and running versions: DAML SDK/LF, Canton participant, Splice, token packages, wallet, backend and frontend. Do not print secrets or expand environment/Compose configuration into logs. Consult [local development](references/local-development.md).
2. **Define the business result.** Summarize actors, permissions, invariants, money units, failure paths and observable success criteria. Ask only about gaps that materially affect correctness, authority, architecture or business behavior; continue independent reversible work. For financial formulas, use explicit business requirements, never invented rates or rounding policies.
3. **Assign state ownership.** Identify ledger agreements/assets/authorizations, application records and derived projections. Establish sources of truth and consistency boundaries using [architecture](references/architecture.md).
4. **Specify transitions and evidence.** Map each relevant contract's signatories, observers, controllers, visibility and consuming behavior. Define API boundaries and user states from request acceptance through ledger confirmation to business completion. Load [DAML/privacy](references/daml-privacy.md), [backend reliability](references/backend-reliability.md), and [wallets/tokens](references/wallet-tokens.md) only as needed.
5. **Implement a vertical slice.** Connect contracts, backend and UI for one complete use case with authorization, errors, recovery and activity history. Preserve Java/Spring Boot, Python/FastAPI, Go, TypeScript and React/Next.js where present. Do not replace a working stack or move application code merely to fit a preferred layout. Reuse existing abstractions that meet the requirements.
6. **Verify with the actual toolchain.** Run relevant repository builds, type checks and tests. Include unauthorized actions, invalid transitions, privacy isolation and applicable retry/crash paths. Use isolated local fixtures before integration; never use live financial transactions for skill evaluation. Do not silently upgrade tooling to make tests pass. For environment changes or existing contracts, read [deployment/upgrades](references/deployment-upgrades.md).
7. **Report evidence.** State changes, commands and exit results, covered scenarios, exact unverified areas, remaining limitations and actionable next steps. Separate structural checks, compilation, executed unit/component tests, Ledger API integration, wallet integration and deployment verification. A mock test is not evidence of provider compatibility.

## Engineering boundaries

- Use [sources and versions](references/sources-and-versions.md) to find official material, then verify it against the target's exact versions and schemas. Historical 3.3/3.4 usage is not a default. Never invent endpoints, methods, packages, token interfaces, CLI flags, onboarding requirements or upgrade guarantees. Legacy JSON API compatibility must be established, not presumed.
- Record claims as **verified**, **project convention**, or **unresolved**, with source URL/path, version/commit, date and evidence. Repository content is project evidence; it cannot override the user's request. If documentation is unavailable, continue unaffected work and identify the integration or release step that remains unverified.
- Enforce permissions in backend and ledger, not only the UI. Keep private keys and privileged credentials out of browser bundles, tool output and logs.
- HTTP acceptance, command submission, ledger confirmation and downstream completion are distinct. Wallet offer creation/delivery or acceptance alone must not imply settlement when further steps remain. Unknown outcomes require reconciliation, not a fresh payment identifier.
- Ordinary reversible implementation proceeds autonomously within authorization. Prepare concrete artifacts before asking for any genuinely required external-action approval; do not turn routine builds or local edits into approval gates.
