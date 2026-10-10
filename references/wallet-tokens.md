# Wallet, token and funding lifecycles

Use before token transfers, funding UI or wallet integration. Sources T1/T2/W1 in [sources](sources-and-versions.md) do not establish a provider's deployed version.

Identify the actual provider and release, network/synchronizer, issuer/instrument, token package IDs/interfaces, party hosting, custody, signing authority and recipient workflow. Determine whether signing is participant-managed or external, who holds keys, what consent is needed, and whether wallet onboarding, party allocation and funded holdings are separate steps. Do not infer a wallet from a party ID or Ledger API URL.

Match official provider API/schema and installed DARs to the integration. Distinguish Splice wallet-specific offers, token-standard transfer instructions, direct/preapproved transfers and allocations used for settlement. Do not assume all assets implement identical choices or that V1/V2 interfaces are interchangeable. Obtain verified context/disclosures where required; handle stale context through supported refresh/reconciliation. Never fabricate package IDs or copy release-floating examples into production configuration.

Model both application funding requests and asset movements. Approval may authorize initiating a transfer but does not deliver funds. These are conceptual labels, not promised provider status strings:

| Evidence | UI meaning |
| --- | --- |
| Durable request accepted | Request recorded |
| Authorized initiation pending/submitted | Preparing/submitting transfer |
| Offer created or delivered | Awaiting recipient action if required |
| Recipient acceptance confirmed | Accepted; settlement may remain pending |
| Rejection/withdrawal/expiry confirmed | Relevant terminal failure, when supported |
| Verified asset delivery/settlement | Funds delivered; complete the matching business step |
| Timeout, stale projection, missing evidence | Outcome unknown/reconciling |

Map actual responses/transitions to these meanings with tests. Where acceptance is unnecessary, use the verified direct/preapproval path instead of inventing an offer phase. Never auto-accept for a recipient without their authority. Wall-clock expiry alone may not establish final ledger outcome; reconcile races with acceptance/completion.

Bind settlement evidence to the persisted operation, network, sender, recipient, issuer/instrument, exact amount/fee semantics and update/contract references. Offer IDs, balance differences or an application receipt alone are insufficient. Providers may expose authoritative completion differently; document and verify that trust boundary rather than requiring an unavailable event shape.

Keep privileged credentials/keys server-side or in the verified custody signer, scoped to the actor. Redact upstream errors and request/response logs. Enforce authority in backend and ledger even when UI actions are hidden.

Test delivered-but-unaccepted, accepted-but-unsettled, rejected, expired, unknown, duplicate/reordered updates and confirmed delivery. Include refresh/reconnect and cross-tenant access. Do not create real financial transactions for evaluation.
