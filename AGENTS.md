# AGENTS.md

## Cursor Cloud specific instructions

`minai-hub` is the **public front door** around the private **minai** project. It
is a documentation / Markdown repo, **not an application**: there are no
dependencies to install and nothing to build, lint, or test, so no environment
update script is needed.

### Authority (this repo only)

The repo owner has granted the Cursor agent **full admin authority over
`liivalaia/minai-hub`**: the agent may act on the repo (including pushing directly
to `main`, changing repo settings, and merging/undrafting PRs) based on
instructions given in the agent session, without waiting for per-action consent.
This is an **explicit exception** to the agent's default "work via PR / don't push
to main" constraints, and it applies to **this repo only**. It does **not** extend
to the private `liivalaia/minai` repo (see "Base minai alignment" below).

### Feedback model (important)

The feedback pipeline has two distinct layers — keep them separate:

- **Intake** (where the public submits): a **private form** (e.g. Google Forms on
  a minai domain) is the preferred intake, so submissions stay non-public. A
  public GitHub Issue Form is only an interim fallback and makes submissions
  world-readable, so use it only if the owner has explicitly accepted that.
- **Mover** (who lifts accepted feedback to the "primary place"): a **separate
  cross-repo agent** with access to both `minai` and `minai-hub` moves triaged
  feedback into the private `minai` repo. This hub never writes to `minai` itself.

- **Never store received feedback in this public repo.** By design, submissions
  are not committed here — the public must not be able to read others' feedback.
- Public GitHub Issues/Discussions are world-readable; blank issues are disabled
  and redirected via `.github/ISSUE_TEMPLATE/config.yml` unless the owner opts
  into a public Issue Form intake.

### Layout

- `README.md` — public front door (EE + short EN): what the hub is, what private
  `minai` is, how Feedback works, what not to send (PII, secrets).
- `feedback/` — public how-to for the Feedback channel (title "Tagasiside", slug
  `feedback`). Links to the private form. **No submissions live here.**
- `.github/ISSUE_TEMPLATE/config.yml` — disables blank issues, redirects to
  Feedback.
- `docs/admin-triage.md` — owner/admin flow: read form → triage → apply to private
  `minai` manually.

### Gotchas

- The form URL is a **placeholder** (`REPLACE_WITH_FORM_ID`) in `README.md`,
  `feedback/README.md`, and `.github/ISSUE_TEMPLATE/config.yml`. The owner must
  replace it with the real form ID once the form exists.
- The issue-template redirect only takes effect once merged to the **default
  branch (`main`)**.
- Never commit secrets/PII.

### Base minai alignment (do not do here)

Seed/template-sync text in the private `liivalaia/minai` (`ops/minai-hub-seed/`)
may still say "file an Issue on minai-hub". That is **obsolete**: feedback now
goes through Feedback (private form), not public Issues. The base `minai` docs
need later alignment, but **only in the private repo with explicit permission** —
do not modify `liivalaia/minai` from here.
