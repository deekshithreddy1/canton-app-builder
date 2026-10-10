# Ledger-backed operations and recovery

Use for APIs, event consumers and workers. Preserve the existing language/framework. Sources L1/L2 establish versioned Ledger API concepts; the transaction design below is an engineering recommendation.

Discover the actual gRPC protos or JSON Ledger API schema and authentication configuration. Verify issuer, audience, expiry, user-to-party rights and supported signing model. Keep authenticated identity separate from request parameters. Generate/reuse bindings from matching definitions when supported; do not infer endpoints from a legacy JSON API tutorial.

Define separate states for durable request acceptance, command submission, confirmed ledger result and downstream completion. A submit-and-wait response can provide command outcome according to its verified schema; it does not prove a separate wallet or business process finished. Persist uncertainty on timeouts, including failures after the ledger may have committed.

## Durable boundaries

1. In one application DB transaction, scope an idempotency key to tenant/network/operation, compare a canonical payload hash and persist an intent with stable command/tracking identity. Same key with different payload is a conflict; concurrent duplicates return the same operation.
2. Submit outside the DB transaction with worker leases/fencing or equivalent concurrency control. Persist enough before the external call to recover after a crash. Reuse the business identity on uncertain retry, including all fields forming the deployed API's deduplication identity, not only the command ID. Distinguish attempt/submission identifiers if the API requires them.
3. On restart, reconcile unresolved intents using supported completion/update/provider evidence. Separate authorization/business rejection from transient transport failure. Back off retries and cap/escalate unresolved attempts; never blindly resubmit beyond a verified deduplication boundary.
4. Apply each ledger update's projection changes, event deduplication marker and stream checkpoint in the same DB transaction. Scope identifiers to ledger/network/stream. Never advance a checkpoint before applying state. For separate stores, use a durable handoff/outbox and explain recovery rather than claiming a cross-store atomic commit.
5. Deliver downstream effects through durable outbox work with recipient idempotency where available. Reconcile effects without it. Handle duplicate/delayed delivery, concurrent workers, poison events and terminal-state regression.

The 3.4 documentation scopes ledger command deduplication to a change identity, a time/offset window and the same participant. Verify exact identity fields, retention and behavior for the deployed release. DB uniqueness, ledger deduplication and provider deduplication cover different boundaries. Avoid unqualified exactly-once claims.

## Projections and tests

Establish snapshot/stream offset consistency, filter/party coverage, lag monitoring and safe rebuild if history is pruned. PQS is a query projection, not a transaction coordinator. A projection cannot prove an unseen contract does not exist for other parties.

Inject crashes before submission, after submission but before response persistence, and between state/checkpoint writes. Test duplicate requests/events, payload conflicts, worker races, retries past dedup windows, expired credentials, stale contracts and restart recovery. Verify one business effect and consistent state/checkpoint after replay, not just an HTTP status. Report local DB/mock results separately from participant integration.
