# Canton App Builder

A reusable **Codex skill for building full-stack applications on Canton** with DAML contracts, backend APIs, and web interfaces.

It gives Codex a repeatable engineering workflow: understand the repository and business rules, design ledger and application state, implement a complete vertical slice, and verify the result with the project's actual toolchain.

Use it for pooled lending, collateralized credit lines, settlement financing, tokenization, funding requests, and other multi-party workflows. It also covers separating an application from Canton Quickstart and planning changes to deployed DAML contracts.

## What this repository provides

This is an instruction package for Codex. It contains the skill and focused engineering references; it does not contain a runnable Canton application, wallet SDK, or preconfigured infrastructure.

The skill helps Codex:

- Discover the repository's DAML, Canton, Splice, wallet, and application versions before choosing APIs or dependencies.
- Define actors, permissions, contract transitions, and business success criteria.
- Explain who can see each contract and who can exercise its choices.
- Build backend operations with durable idempotency, crash recovery, and reconciliation.
- Show honest transaction progress in the UI, including recipient acceptance and settlement when required.
- Preserve the existing stack, whether Java/Spring Boot, Python/FastAPI, Go, TypeScript, React, or Next.js.
- Keep application ownership separate from upstream Quickstart infrastructure.
- Prepare environment-specific deployment and upgrade plans with explicit verification limits.

## Install

You need Codex with local skill support. Installing this skill does not require a DAML SDK or Docker; those may be needed for the application tasks you ask it to perform.

The [official Codex skill documentation](https://learn.chatgpt.com/docs/build-skills) describes personal skills in `~/.agents/skills` and repository-scoped skills in `.agents/skills`.

### Windows / PowerShell

```powershell
$skillDirectory = Join-Path $HOME '.agents\skills\canton-app-builder'
if (Test-Path -LiteralPath $skillDirectory) {
    throw 'canton-app-builder already exists. Review the existing installation before replacing it.'
}
New-Item -ItemType Directory -Path (Split-Path $skillDirectory -Parent) -Force | Out-Null
git clone https://github.com/deekshithreddy1/canton-app-builder.git $skillDirectory
```

### macOS / Linux

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/deekshithreddy1/canton-app-builder.git \
  "$HOME/.agents/skills/canton-app-builder"
```

If you already have this skill installed, inspect that copy before updating it. Do not create duplicate installations in multiple discovery directories.

For a repository-scoped installation, copy `SKILL.md`, `agents/`, and `references/` into your application's `.agents/skills/canton-app-builder/` directory. Keep the same relative layout. Downloading this repository as a ZIP and copying those files also works; Git is not required for that method.

Codex should discover the skill automatically. If it is missing, restart Codex and start a new session in your application repository.

## Use it

Open the application repository you want to work on, then explicitly invoke the skill:

```text
Use $canton-app-builder to add a multi-party approval workflow.
The borrower submits a request, and both the lender and risk reviewer must
approve it. An unrelated tenant must not see or approve the request.
Preserve the current stack and implement the contracts, API, and UI.
```

Give Codex the business behavior you want, the repository to change, and any deployment or authorization constraints. The skill directs it to inspect the project before selecting versions or implementation details.

### More examples

**Reliable backend operation**

```text
Use $canton-app-builder to add durable idempotency and crash recovery to this
ledger-backed API operation. Handle a crash after the ledger commits but
before the backend saves the response. Keep our existing FastAPI stack.
```

**Funding request and wallet progress**

```text
Use $canton-app-builder to display funding-request and wallet-transfer
progress in our existing UI. Determine our actual wallet flow first.
Do not show funds delivered while recipient acceptance or settlement
is still pending.
```

**Separate deployment environment**

```text
Use $canton-app-builder to prepare our application inside Canton Quickstart
for a separate deployment environment. Preserve local reproducibility,
identify app-owned files and upstream infrastructure, and prepare the
configuration and runbook. Do not deploy yet.
```

**DAML upgrade planning**

```text
Use $canton-app-builder to plan a DAML upgrade with existing active contracts.
Inspect the baseline DAR, compiler, participant versions, dependencies,
and consumers. Explain compatibility checks, package vetting, migration
options, and rollback limits before implementation.
```

## How the workflow works

1. **Inspect:** identify versions, architecture, services, instructions, tests, and deployment environment.
2. **Clarify the business workflow:** summarize actors, authority, invariants, and success criteria.
3. **Assign state ownership:** separate authoritative ledger state, application records, and projections.
4. **Define transitions:** specify contract choices, API boundaries, and evidence for user-visible states.
5. **Implement:** build the smallest complete slice across contracts, backend, and frontend.
6. **Verify:** run the relevant builds and tests using the actual installed toolchain.
7. **Report:** explain changes, executed checks, limitations, and precise next steps.

Ordinary reversible work proceeds within the requested scope. Missing information should trigger questions when it materially changes correctness, authority, architecture, or business behavior.

## Important engineering distinctions

**Versions are discovered, not assumed.** Historical DAML/Canton 3.3 or 3.4 usage does not make those releases a default. SDK, LF, participant, Splice, token packages, and wallet versions are separate compatibility questions.

**Submission is not completion.** HTTP acceptance, command submission, ledger confirmation, and downstream business completion can be different events. Creating or delivering a wallet offer does not prove funds were transferred.

**A database projection is not the ledger.** PostgreSQL and PQS can serve different roles. The skill requires explicit consistency boundaries, durable checkpoints, and recovery behavior rather than unqualified exactly-once claims.

**Permissions belong in every relevant layer.** UI visibility alone is insufficient. Backend identity checks and ledger authorization must enforce the intended permissions, with privacy tests for unrelated parties.

**Uploading a DAR is only part of deployment.** Backend, frontend, database, authentication, connectivity, and operations need their own deployment work. Application rollback does not undo ledger transactions or automatically migrate contracts.

## Repository map

```text
.
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── architecture.md
│   ├── daml-privacy.md
│   ├── backend-reliability.md
│   ├── wallet-tokens.md
│   ├── local-development.md
│   ├── deployment-upgrades.md
│   └── sources-and-versions.md
└── evaluation/
    ├── fixtures.json
    └── results.md
```

Start with [SKILL.md](SKILL.md). Codex loads the deeper references when they are relevant to the task. The [source/version record](references/sources-and-versions.md) distinguishes official evidence, version applicability, and unresolved documentation gaps.

## Validation and limits

The initial skill passed the installed skill-creator structural validator, YAML and relative-link checks, an isolated installation-layout copy check, and package-integrity checks.

Five synthetic offline scenarios received author-applied tabletop evaluation: multi-party approval, idempotency/crash recovery, funding/offer lifecycle, separate deployment, and existing-contract upgrades. Read the [fixtures](evaluation/fixtures.json) and [evaluation results](evaluation/results.md) for the concrete cases and limitations. These are design reviews, not an independent model benchmark or executed application tests.

No application compilation, Ledger API integration, wallet integration, or deployment is certified by installing the skill. Those checks belong to each target project. Documentation research includes official Digital Asset 3.4 material and rolling Splice/token-standard references; it does not certify a particular provider or a newer deployed API version. Verify the current matching sources before implementation.

## Improving the skill

When proposing a change, describe the application scenario it improves, include version-specific source evidence where needed, and update the relevant evaluation case. Keep project party IDs, secrets, customer information, and deployment-specific configuration out of this repository. Put project decisions in the application repository.
