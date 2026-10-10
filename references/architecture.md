# Architecture and state ownership

Use when defining a vertical slice or separating an application from Quickstart. These are engineering recommendations, not platform guarantees; versioned platform sources are in [sources](sources-and-versions.md).

Write a compact workflow record in the target project's existing documentation: trigger, actors, authorization, input units/precision, invariant, transition, resulting evidence, rejection behavior and recovery. Specify tenant, party and network identity independently; never trust a party supplied by the browser as permission to act for it.

| State | Typical owner | Required decision |
| --- | --- | --- |
| Agreements, obligations, asset rights, approvals | Ledger contracts | Which parties must authorize and see each transition? |
| Preferences, sessions, documents, operation intents, retry state | Application store | Retention, access controls and durable transaction boundaries |
| Search views, balances, activity lists, contract indexes | Projection | Source, offset, scope, lag, rebuild and pruning behavior |
| External payment/signing outcome | Provider plus confirmed evidence | What proves completion, and how is it reconciled? |

PostgreSQL may host application state, a PQS projection, or operational node data. Determine the actual role and keep ownership/schema boundaries explicit. A mirror can lag and is not authoritative proof of current ledger state. Do not write application changes directly into participant or PQS-managed tables. See source P1.

Use exact decimal/fixed-point money, explicit instrument and scale, and business-defined rounding. For lending/credit, define exposure limits, collateral valuation source and timestamp, accrual/repayment ordering, liquidation authority and currency conversion before implementing affected behavior. Do not equate approval of credit with disbursement or a bookkeeping receipt with asset delivery.

For the UI, preserve the existing stack and authentication flow. Implement validated forms, role-aware actions, operation progress, recoverable errors and scoped activity history. Present stale/offline data and unknown outcomes honestly. Correlate operation, command, update/transaction and contract identifiers server-side. Permit refresh/reconnect without losing in-flight operations. Avoid optimistic financial success.

For repository structure, consider contracts/, backend/, frontend/, infra/ and docs/ only when it fits existing ownership. Separate repositories are equally valid. Record the canonical location, upstream Quickstart commit/tag, owned overlays and artifact handoffs. Plan relocation independently from behavior changes; do not reorganize without task scope and evidence.
