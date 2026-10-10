# DAML authorization and privacy

Use for contract design, review and tests. Sources D1/D2/U1 in [sources](sources-and-versions.md) anchor historical 3.4 semantics; check the selected compiler/LF and participant before applying version-sensitive details.

| Contract/choice item | Specify |
| --- | --- |
| Creation | Fields, invariants, signatories and how creation authority is obtained |
| Reading | Stakeholders, observers, disclosure recipients and transaction consequences |
| Exercise | Controllers, required authorization, preconditions and necessary visibility |
| Lifecycle | Consuming/nonconsuming, archived inputs, created outputs, terminal states |
| Interface | Installed package identity, implementing templates, view and choice semantics |

Signatories authorize creation; observers do not gain choice authority merely by observing. Choice controllers are not automatically observers. Visibility is affected by transaction structure and disclosure, not just the template's observer list. Analyze nested exercises and transitive consequences; disclosure provides information, not blanket authority. Do not claim privacy merely because a party's name is absent from a template.

Default choices consume their contract unless declared nonconsuming. Make that intent explicit: a consumed proposal cannot be accepted twice; a nonconsuming approval path needs another enforceable replay/state invariant. Validate values on direct creation as well as choice paths. Avoid trusting only frontend validation or backend admission checks for ledger invariants.

For multi-party approval, collect each party's actual authority through proposals, acceptances or other verified authorization patterns. A list of approver names or a UI checkbox does not authorize them. Define whether approvals are sequential, unanimous or threshold-based, how expiry/revocation works, and whether distinct parties are required. Preserve partial approval state atomically and prevent premature finalization.

Test valid creation/exercise, missing signatory, wrong controller, invalid amounts/dates, duplicate/replayed actions, premature finalization and consumed contract reuse. Assert visibility for each actor and unrelated tenants. Script tests establish model behavior; separate Ledger API tests must cover authenticated readAs/actAs rights and actual participant visibility/disclosure. An all-party administrative test client does not establish tenant isolation.

Check the selected release's interface support, contract keys, disclosure mechanisms and upgrade rules rather than copying old examples. Changes to module/template identity, signatories, choice bodies or data representations need compatibility and semantic review; see [deployment/upgrades](deployment-upgrades.md).
