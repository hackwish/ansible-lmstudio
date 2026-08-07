# AGENTS.md

Ansible Galaxy role (not a playbook) that installs LM Studio on Debian-based Linux (`.deb` via `apt`) and macOS Silicon (`.dmg` mounted/copied with relative `./tmp/` paths run on the control node). Entrypoint is `tasks/main.yml`.

## Version/build must match real installer URLs

`defaults/main.yml` holds `version` + `build`, interpolated into:
`https://installers.lmstudio.ai/{linux/x64|darwin/arm64}/{version}-{build}/LM-Studio-{version}-{build}-x64.deb` (or `-arm64.dmg`).

Wrong combos silently 404 (e.g. `4.0.0-6`). To find the latest, resolve the redirect:
`curl -sIL https://lmstudio.ai/download/latest/linux/x64 | grep -i location` → yields `<version>-<build>` (e.g. `0.4.20-1`). Then verify BOTH the `.deb` and the `.dmg` return HTTP 200 before committing a bump. Update `defaults/main.yml` and the README "Role Variables" section together.

## Verify

`ansible-playbook tests/test.yml -i tests/inventory --syntax-check`

`ansible.cfg` sets `roles_path=../`; `tests/test.yml` runs against `localhost` with `become: true`, so running it (not just syntax-check) installs LM Studio on the current machine. Use syntax-check for CI-style verification.

## Other notes

- Tasks deliberately use `ignore_errors: true` throughout; keep that pattern.
- All tasks are tagged `lmstudio`; filter with `--tags lmstudio`.
- CI is semantic-release on push to `master`/`main` (`.github/workflows/actions.yml`). Commit messages must follow conventional-commit format — commit type/scope drives versioning.
- `meta/main.yml` is the untouched Galaxy template; leave it unless publishing to Galaxy.
