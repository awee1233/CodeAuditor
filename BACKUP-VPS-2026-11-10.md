# VPS Backup Snapshot — 2026-11-10

Snapshot of the CodeAuditor tree as it existed on the UpCloud VPS
(`95.111.194.228`, host `kazu`) at `/opt/tools/CodeAuditor`.

## Provenance

- Source host: `95.111.194.228` (UpCloud), user `root`
- Source path: `/opt/tools/CodeAuditor`
- Source git HEAD: `a7aca02` — `fix: specify reproduction disclosure manifest roles`
  (clone of upstream `COCOP1l0t/CodeAuditor`, history depth = 1, not shared with this
  repository's history)
- Owner on VPS: `codeauditor:codeauditor`
- Snapshot date: 2026-11-10

## Why this branch exists

The VPS tree descends from the upstream `COCOP1l0t/CodeAuditor` repository and shares
**no common ancestor** with this repository's `main` (261 commits, started 2026-03-14).
Force-overwriting `main` would have destroyed that history, so the VPS tree is recorded
here on its own branch instead. `main` is untouched.

## What was excluded

- `.venv/` (729 MB virtualenv, reproducible from `uv.lock`)
- `__pycache__/`
- `node_modules/`
- `.git/` of the source clone
- Runtime data under `/home/codeauditor/.code_auditor/` (`audits.db`, `audits.db.secret-key`,
  `results/`, `repo/`) — deliberately not committed: it holds audit data and an
  encryption key that must not enter version control.

## Local uncommitted change on the source host

`code_auditor/agent.py` carried one uncommitted modification relative to `a7aca02`: the
Codex provider `wire_api` value is now read from the `CODE_AUDITOR_CODEX_WIRE_API`
environment variable instead of being hardcoded to `"responses"`. That change is included
in this snapshot.

## Divergence summary vs `main`

- 97 paths differ overall (15 present only on `main`, 17 present only on the VPS tree,
  65 modified in both).
- Present on the VPS tree but not on `main`: `contracts.py`, `semantic_dedupe.py`,
  `stage_runtime.py`, `stage_state.py`, `submission_policy.py`, `layout.py`,
  `db_constants.py`, `agent_runtime.py`, `web/history.py`, plus matching tests.
- Present on `main` but not on the VPS tree: `code_auditor/bench/`, `web/auth.py`,
  `scripts/reset_password.py`, and the benchmark integration docs.

This branch is a point-in-time record, not a forward development line. Do not merge it
into `main` blindly; it will revert the benchmark subsystem.
