# AGENTS.md

## Project purpose
Older standalone repo of reusable GitHub Actions workflows for VyOS. Largely **superseded by `vyos/.github`** (the canonical org-wide reusable-workflow library, default branch `production`). Some the private side-side and legacy repos still consume workflows from here; new work should target `vyos/.github`.

## Tech stack
- GitHub Actions YAML reusable workflows under `.github/workflows/`.
- Python helper scripts under `scripts/` (`check-pr-title-and-commit-messages.py`, `override-default`, `transclude-template`).

## Build / test / run
N/A — consumed by other repos via:
```
uses: vyos/vyos-github-actions/.github/workflows/<name>.yml@<ref>
```
The Python helper scripts are invoked from the workflows.

## Repository layout
- `.github/workflows/` — reusable workflows: `codeql-analysis.yml`, `mergifyio_backport.yml`, `pr-conflicts.yml`, `pull-request-labels.yml`, `pull-request-management.yml`, `pull-request-message-check.yml`, `stale.yml`, `unused-imports.yml`, `cla-check.yml`, `auto-author-assign.yml`.
- `scripts/`
  - `check-pr-title-and-commit-messages.py` — PR-title/commit-message linter (`component: T12345: description`).
  - `override-default` — XML preprocessor (also vendored in `vyos/.github/scripts/`, used by `vyos-1x`/`vyos-build`).
  - `transclude-template` — XML `#include` preprocessor (same vendoring).
- `README.md` — workflow inventory + usage snippets.

## Cross-repo context
- **Superseded by `vyos/.github@production`.** That canonical repo carries 19 workflow files and the modern mirror pipeline (`pr-mirror-repo-sync.yml`). Most active VyOS repos pin `vyos/.github`, not this repo.
- The `override-default` and `transclude-template` scripts here are duplicated into `vyos/.github/scripts/` — they are runtime build-time helpers used by `vyos-1x` (XML interface-definition processing) and `vyos-build`.
## Conventions
- Commit/PR title: `component: T12345: description` (Phorge task ID at https://vyos.dev).
- Reusable-workflow pin model: callers reference these workflows with floating refs (no semver tags); changes ship to consumers immediately.
- Default branch is the legacy default (typically `master`/`main`); confirm via `git ls-remote --symref` before pinning.

## Notes for future contributors
- **New reusable workflows belong in `vyos/.github`, not here.** Add them at `vyos/.github/.github/workflows/<name>.yml` on `production`.
- Before deleting a workflow from this repo, grep `vyos/*` and an internal repository consumers for `uses: vyos/vyos-github-actions/...` — some legacy repos may still be pinned here.
- The `scripts/override-default` and `scripts/transclude-template` are kept in sync with the copies in `vyos/.github/scripts/`. If you change one, change the other (or migrate fully to `vyos/.github`).
