# Offline behavioral evaluation

Date: 2026-10-09. Method: author-applied tabletop evaluation using the five isolated fixtures in fixtures.json and the completed skill. These are concrete design responses and review judgments, not an independent agent benchmark or executed application tests. No application repository was modified and no live service was called. Platform code was not generated merely to simulate validation.

## 1. Multi-party approval

Selected workflow and DAML/privacy, architecture and backend references. Preserve Java/Spring Boot and React. The borrower creates a request under borrower authority; use verified proposal/acceptance authority flow for lender and risk. Finalization must obtain all necessary authority, not create a three-signatory agreement from the borrower's submission alone. Consuming approval transitions track the set of distinct approvals and prevent reuse of a previous state. Rejection/cancellation terminate the pending workflow according to the fixture; concurrent accept/cancel must resolve through ledger contention rather than two successful business outcomes.

The borrower, lender and risk party can see the request by the chosen stakeholder design; outsider cannot. Only the designated party exercises each approval; observers gain no generic approval right. Review consequences/disclosures before promising the intended privacy. Backend maps sessions to scoped rights, stores operation intent/projection, and UI shows pending partial approval until confirmed finalization. Test missing signatory, outsider approval/query, duplicate approval, early finalize, cancelled request and successful unanimous approval.

Assessment: guidance rejects the authorization shortcut and covers a complete slice. Approval proposal details must be compiled with actual SDK and integration-tested for privacy. No such compilation/integration ran in this evaluation.

## 2. Ledger operation and crash recovery

Preserve FastAPI/PostgreSQL. Return the persisted operation for retry K; compare payload and scope before accepting it. Keep command C and reconcile its outcome after the response-loss crash. Do not create a fresh command/payment identity, including after expiry of the deduplication window. If evidence is pruned/unavailable, keep unresolved state and request the necessary recovery evidence rather than claiming failure and resubmitting.

Process E through one DB transaction containing projection changes, unique event marker and checkpoint. A crash before commit rolls all three back; replay then commits once. A crash after commit observes the marker. If current code splits these writes, repair that boundary. Use a durable outbox and provider idempotency for downstream effects; no global exactly-once claim. Verify worker concurrency, differing payload for K, duplicates and both crash points with fixtures, then verify participant schema/auth separately.

Assessment: recovery guidance handles the two crash windows and limits retries beyond deduplication. No FastAPI/PostgreSQL or participant test was executed; the fixture is a design trace, not crash-injection evidence.

## 3. Funding and wallet UI

Preserve Next.js. Keep request approval separate from delivery. Trace maps to approved -> offer pending -> awaiting recipient -> accepted/settlement pending -> reconciling -> delivered. A delayed created event must not regress confirmed delivery. Only the matching evidence permits delivery status; full business completion may require a separate ledger bookkeeping step. Persist operation identity across refresh and show history with safe errors.

Rejected and expired branches render supported failure states. Confirm expiry against provider/ledger evidence. For a preapproved asset, use its verified direct-delivery lifecycle without inventing recipient acceptance. Hide unavailable actions in UI and enforce rights server-side and on ledger.

Assessment: guidance avoids premature success at creation, delivery and acceptance, and handles reordered updates. No browser, wallet or frontend component test ran.

## 4. Separate deployment

Preserve Go and existing owned paths while preparing an ownership/extraction plan. Identify/pin actual Quickstart upstream, retain overlays and a clean-checkout local procedure. Do not delete the development volume. Keep managed release DARs with hashes/provenance; exclude runtime DBs, secrets and generated caches.

Prepare app artifacts, TestNet configuration placeholders, auth/TLS, database migration/backup/recovery and monitoring separately from DAR deployment. Hosted participant operator must supply supported versions, hosting/rights, package vetting, connectivity and wallet capabilities. Do not start validator onboarding merely because the application changes environment. PQS remains a scoped projection and needs rebuild/lag procedures. Produce a runbook and unresolved environment matrix without deploying.

Assessment: rejects DAR-only deployment and destructive reset; honors prepare-only scope. No container or deployment verification ran. Upstream pin/provider details remain prerequisites, not fabricated values.

## 5. Existing contract upgrade

Inventory the actual baseline/hash, LF/dependencies and active obligations, plus versions for both participants and older consumer. The module rename and required-field change are not assumed compatible. Run supported baseline compatibility checks without disabling them. Preserve old contracts/packages while assessing a compatible redesign or an explicitly authorized migration; plan mapping, consent, resumability and reconciliation if migration is needed.

Reverify target 3.5.x support and vetting of required source/target packages across informed participants. Test old/new clients and contracts in an isolated matching runtime. Database rollback cannot undo ledger effects. Do not promise participant compatibility from a 3.4.11 compiler result.

Assessment: guidance rejects bypassing compatibility checks and separates application rollback from ledger migration. No upgrade compilation or deployed old/new interoperability test ran.

## Review limits

All five scenarios are covered at the design-guidance level. This establishes traceable coverage, not measured independent model performance or correct generated code. Structural validation is summarized in the repository README. The skill contains no executable inspection helper or speculative application scaffold, so there are no bundled helper scripts to test. Future changes should rerun these cases and record actual implementation/test results when suitable isolated runtimes and task scope are available.
