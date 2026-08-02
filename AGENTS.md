# AGENTS.md

## Cursor Cloud specific instructions

`minai-hub` is the **public front door** around the private **minai** project. It
is a documentation / Markdown repo, **not an application**: there are no
dependencies to install and nothing to build, lint, or test, so no environment
update script is needed.

### Feedback model (important)

Feedback is collected through an **external private form** (Option A: hosted form
such as Tally, with CAPTCHA / rate limit / honeypot). Submissions are visible
**only to admins** on the form dashboard.

- **Never store received feedback in this public repo.** By design, submissions
  are not committed here — the public must not be able to read others' feedback.
- Do **not** use public GitHub Issues/Discussions as the inbox (world-readable).
  Blank issues are disabled and redirected via `.github/ISSUE_TEMPLATE/config.yml`.

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
