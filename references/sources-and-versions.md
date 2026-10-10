# Sources and version applicability

Verification date: **2026-10-09**. These are research anchors, not default dependency versions. No service compatibility is inferred from a documentation page. Re-open the matching official release documentation and inspect installed schemas/DARs before implementation.

## Opened official sources

| ID | Source | Verified scope and applicability |
| --- | --- | --- |
| D1 | [Digital Asset: Compose choices](https://archived.docs.digitalasset.com/build/3.4/tutorials/smart-contracts/compose.html) | 3.4 documentation: observers, controllers, transaction consequences and privacy. Not a proof of isolation in a particular deployment. |
| D2 | [Digital Asset: Choices](https://archived.docs.digitalasset.com/build/3.4/reference/daml/choices.html) | 3.4 language reference: controllers and consuming/nonconsuming choices. Recheck against selected SDK/LF. |
| L1 | [Digital Asset: Ledger API services](https://archived.docs.digitalasset.com/build/3.4/explanations/ledger-api-services.html) | 3.4 submission versus completion, command services and participant-scoped deduplication. |
| L2 | [Digital Asset: Command deduplication](https://archived.docs.digitalasset.com/build/3.4/sdlc-howtos/applications/develop/command-deduplication.html) | 3.4 command/change identity, attempt submission IDs, effective dedup periods and recovery. Page contains both user-ID and application-ID terminology in different sections: resolve exact fields from the deployed proto/schema rather than assuming interchangeability. |
| J1 | [Digital Asset: JSON Ledger API OpenAPI](https://archived.docs.digitalasset.com/build/3.4/reference/json-api/openapi.html) | Opened 3.4 schema reference. Does not validate 3.5 request shapes or legacy v1 compatibility. Prefer the actual participant's matching schema. |
| P1 | [Digital Asset: PQS architecture](https://archived.docs.digitalasset.com/build/3.4/component-howtos/pqs/references/architecture.html) | 3.4 event ingestion into a query datastore; applications submit commands to participant. Use supported SQL interfaces, not internal tables. |
| U1 | [Digital Asset: Smart Contract Upgrade](https://archived.docs.digitalasset.com/build/3.4/sdlc-howtos/smart-contracts/upgrade/smart-contract-upgrades.html) | 3.4 compatibility checking and package vetting, including source/target packages on informed participants. No guarantee for other releases or arbitrary semantic changes. |
| T1 | [Splice: Token Standard APIs](https://docs.sync.global/app_dev/token_standard/index.html) | Rolling main documentation: holdings, interfaces, transfer integration, context/disclosures and versioned history handling. Release not pinned by URL; inspect installed packages before using any identifiers. |
| T2 | [CIP-0056](https://github.com/canton-foundation/cips/blob/main/cip-0056/cip-0056.md) | Rolling proposal/specification source, reached through Splice documentation. A standard is not evidence every deployed asset/provider implements it. |
| W1 | [Splice.Wallet.TransferOffer](https://docs.sync.global/app_dev/api/splice-wallet/Splice-Wallet-TransferOffer.html) | Rolling generated contract reference; accepted offers have a separate completion choice. Applies to this wallet contract family, not every token transfer. |
| N1 | [Splice: Validator onboarding](https://docs.sync.global/validator_operator/validator_onboarding.html) | Rolling network/operator prerequisites; separate DevNet/TestNet/MainNet. Reconfirm requirements with operator and network before acting. |
| C1 | [OpenAI: Build skills](https://learn.chatgpt.com/docs/build-skills) | Current official page, redirected from developers.openai.com/codex/skills. Documents local .agents/skills discovery and agents/openai.yaml metadata. Environment installation notes belong in the delivery report. |

## Unresolved boundaries

- The original docs.digitalasset.com 3.4 URLs returned 404; the archived official 3.4 pages above opened successfully. Attempts to open the 3.5 JSON Ledger API page on docs/get-docs/archived hosts failed. Search snippets are not sufficient to certify that schema; fetch the deployed schema or matching official release before 3.5 integration.
- The rolling Splice Validator API index at https://docs.sync.global/app_dev/validator_api/index.html repeatedly timed out. W1 verifies the contract lifecycle, not every HTTP route or provider response shape.
- No wallet provider is a universal default. Where provider-specific documentation cannot be obtained, record provider/version/auth/custody/schema as unresolved and proceed only with independent work or explicitly labeled local fixtures. Never substitute unrelated blockchain wallet documentation.

## Evidence discipline

Maintain a project-local matrix: component, configured version, installed version, running version, package/hash or schema, source URL/path, verification date, status and unresolved compatibility question. Use **verified** for directly inspected artifacts or executed evidence (name its limits), **project convention** for repository-specific choices, and **unresolved** for absent/conflicting information. Keep infrastructure/runtime, SDK, LF, token package and wallet versions distinct.

The reference guidance about outboxes, idempotency records, state/checkpoint transactions, exact amounts and environment separation is engineering advice to evaluate against the repository. It is not a Canton promise of exactly-once processing, universal wallet behavior or reversible upgrades. No project party IDs, credentials, provider URLs or deployment choices should be promoted into this reusable skill.
