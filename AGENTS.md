# AGENTS.md

This repository maintains `degitag.database` with mariadb, postgresql, redis, memcached, patroni and etcd roles. Use vim in instructions. Write documentation from the DevOps/system architecture perspective.

Support Debian 13, Ubuntu 22.04/24.04/26.04 and Rocky/RHEL 9. All four sibling collections use the same generated role scaffold, fact-aware preflight, layered platform variables, typed public API, service guards and check commands. Preserve existing uncommitted work.

Host networking and additive firewall rules belong to `degitag.infrastructure`. Patroni is the sole PostgreSQL service owner in HA mode; etcd owns consensus. Never delete a data directory, reset DCS, rotate encryption keys, bootstrap a cluster, migrate data or change cluster membership implicitly. Database initialization and external binary installation require explicit switches. Existing topology requires a reviewed operator procedure.

Use tools/generate_role_scaffold.py and tools/role_scaffold_config.yml for generated content. Implementation belongs in tasks/configuration.yml. Defaults must validate before facts are loaded. Secrets must remain in Vault and secret tasks use no_log. Native EL9 SELinux enforcement stays enabled.

Run scaffold --check, pytest tests/unit, YAML lint, production Ansible lint, all role syntax checks, artifact build/install and compile/import sanity. Container smoke must converge on five free target images; real service, SELinux, reboot, replication, Patroni failover, backup and restore need disposable VMs. Document actual evidence and gaps in docs/validation; a refactor does not authorize production deployment or a collection release; repository integration follows the authorized implementation scope and global completion standard.

The GitHub repository owner and Ansible namespace are degitag. Run the shared local entry point bash tests/run_checks.sh. Local toolchain uses Homebrew Python 3.12 and .venv. No credentials in logs, defaults or repository files.

## Change contract and acceptance

- Maintain reusable roles and modules. Customer-specific host values, endpoints and secrets belong in consuming inventories and their secret stores.
- Document public variables, provide meaningful safe defaults and validate typed inputs before changes. Preserve existing consumers and variable contracts for compatible changes; document breaking changes and their migration path explicitly.
- Verify changes against the declared distribution and Ansible support matrix in README, metadata and preflight, including role-specific limits. Syntax success does not prove platform support.
- Prove idempotence on suitable test systems with an unchanged second run reporting `changed=0`. Exercise check mode where supported and document its limits. Verify real service behavior, including systemd/journald, on suitable systems; containers alone do not prove that behavior.
- Use `bash tests/run_checks.sh` for implementation changes plus applicable functional tests. For changes limited to working instructions, check Markdown, diff and consistency and await all triggered required CI; do not invent implementation or host tests for prose changes.
- Update changelog and version as appropriate to functional changes and compatibility. Build and inspect the collection artifact; follow actual release checks through successful completion. Working-instruction changes alone do not justify a release tag. Publishing a collection does not authorize deployment to consuming systems.

## Completion and documentation

The global completion standard applies: commit and push your changes, integrate through a pull request after required checks succeed, await relevant post-merge checks, then clean up only your integrated working branches. Preserve independent changes, branches and worktrees. Respect protection rules and required reviews; report concrete blockers and outstanding steps.

Repository integration, publication and production operation are separate outcomes. Successful checks or a merge do not grant additional production approval. Existing specific approval rules remain binding; this file introduces no blanket automatic production approval.

Use `vim` in instructions and write from the DevOps/system architecture perspective. Preserve repository validation evidence and existing Outline operations documentation; edit Outline only within the requested scope. Obtain secrets from protected variable sources; never print them or commit them.
