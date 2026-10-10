# Local development and ownership

Use for discovery, Quickstart work and reproducible local tests. These are project practices; verify commands against actual manifests, wrappers and installed help.

- Find Git roots, applicable instructions, canonical paths, worktree changes and upstream Quickstart pin. Multiple app copies are not permission to edit all of them.
- Inspect daml.yaml, lockfiles, wrappers, source mappings, test scripts, CI, Compose services, image pins and deployment examples. Record configured versus installed versus running versions separately. An SDK listing does not prove project selection; an image tag does not prove a running service.
- Inspect only necessary nonsecret configuration. Never dump .env files, credentials, private keys, process environments, Docker inspect output or expanded Compose configuration. Use sanitized examples or narrowly allowlisted nonsecret version fields. Even manifests/source can contain credentials; avoid broad unfiltered content output.
- Check executable availability and safe version/help output before commands. On Windows preserve PowerShell/native wrappers; do not assume bash, make, WSL, GNU tools or a Java distribution. A runtime may exist only in containers. Explain missing tools without installing a new stack by default.
- Reuse pinned dependency managers and builds. Separate component tests from Docker/participant/wallet integration. Use disposable DBs, distinct ports and named test resources; inspect lifecycle scripts before executing them. Never reset volumes or stop shared infrastructure as a routine test step.

Keep owned source in canonical directories. If extraction is requested, establish source/artifact boundaries and preserve history; verify a clean checkout can build and connect using pinned Quickstart plus owned overlays. Record upstream URL/tag/commit, modifications, profiles, startup order, health signals and teardown scope. A surrounding workspace commit is not necessarily the upstream Quickstart commit.

Normally exclude secrets, runtime DBs/WAL files, logs, caches, node_modules, virtual environments and generated output from source control. Managed release DARs, hashes/manifests or generated bindings may be explicit exceptions with provenance and reproducible generation. Never blanket-ignore all DARs when releases are intentionally tracked. Do not overwrite ignore rules or delete files during inspection.
