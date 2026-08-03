# AGENTS.md

## Cursor Cloud specific instructions

`minai-hub` is the **public front door** around the private **minai** project. It
is a documentation / Markdown repo, **not an application**: there are no
dependencies to install and nothing to build, lint, or test, so no environment
update script is needed.

### Scope

- This repo is **public**. Keep shared info minimal; **never commit secrets or PII**.
- Agents operating here see only what the public sees. Private `liivalaia/minai`
  and the feedback Google Sheet are out of scope unless the session has separate
  access (not via this repo's contents).
- **Never store received feedback in this public repo.** Submissions must not be
  committed here.

### Feedback (public facts)

- Intake: **https://feedback.minai.ee** — agent-facing, machine-readable JSON
  (`minai.feedback/v1`). By design there is **no human web form**.
- Submit token is shown on the live page — **do not hard-code it** in this repo.
- Blank GitHub Issues are disabled; see `.github/ISSUE_TEMPLATE/config.yml`.

### Layout

- `README.md` — public front door (EE + short EN).
- `feedback/` — how the Feedback channel works (**no submissions live here**).
- `.github/ISSUE_TEMPLATE/config.yml` — blank issues disabled, redirect to Feedback.
- `docs/admin-triage.md` — high-level maintainer triage flow (no secrets).

### Out of scope here

Do **not** modify the private `liivalaia/minai` repo from this hub. Product-side
doc alignment belongs in that private repo with explicit permission.
