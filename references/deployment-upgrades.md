# Deployment, operations and upgrades

Use for environment promotion or deployed contract changes. Sources U1/N1 must be reverified for the exact target release.

## Environment and operational boundary

Build an environment matrix for localnet, DevNet, TestNet and MainNet: app versions, participant/provider owner, Canton/Splice/LF support, synchronizer, endpoints/TLS, identities, wallet, authentication, package availability/vetting, party hosting and DB/projection configuration. Store secret references, never secret values.

Application hosting and participant/validator operation are separate responsibilities. Hosted participants may supply services a self-operated validator must provision. Discover onboarding, network admission, connectivity and permissions with the operator; do not prescribe validator onboarding to every app developer. Splice network instructions do not establish a hosted provider's customer requirements.

A DAR upload deploys neither backend nor frontend, database, authentication or operations. Prepare independently versioned app artifacts, configuration, DB migrations, authentication/redirect setup, TLS and least-privilege identities. Discover deployment commands and health checks from the repository/provider.

Readiness should reflect ledger connectivity, consumer lag and required dependencies. Monitor unresolved commands, pending wallet age, retries, rejection classes and checkpoints without sensitive payloads. Define backups, retention, restore tests, recovery objectives and projection rebuild/reconciliation. Node backup/recovery belongs to its operator. DB restoration must reconcile later ledger activity, not replay all payments blindly.

## Existing contracts and packages

Inventory baseline DAR hashes, package name/version/IDs, dependencies, LF/compiler, active contracts, participants and consumers. Establish compatible smart-contract upgrading versus explicit archive/create migration. Existing contracts do not vanish on upload; renaming a package/module/template is not automatically an upgrade.

For compatible upgrading, verify compiler checks against the actual baseline, participant compatibility checks, supported LF range and package selection/vetting across informed participants. Review semantic changes to authority, privacy and invariants even if compilation succeeds. Never disable compatibility checks to force a release.

For incompatible changes, design authorized migration with old/new mapping, invariant preservation, resumable progress, duplicate prevention and reconciliation of existing obligations. Define who consents and how partially migrated workflows behave. Do not promise reversibility.

Test old/new contracts and clients together in an isolated supported runtime, including dependencies and authorization/privacy regressions. Compiler checks alone do not establish deployed behavior. Record package versions understood by each backend/binding/projection.

Plan application rollback, DB rollback/forward repair, package availability and contract migration separately. Rolling back a container or restoring a DB does not undo ledger transactions or downgrade contracts. Retain prior artifacts and assess data compatibility before rollout; specify pause/reconciliation and repair paths where rollback cannot preserve correctness.
