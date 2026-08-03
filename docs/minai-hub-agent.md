# MINAI-HUB agent brief (role + current-state handoff)

Read this first if you operate this repo. It is **public-safe**: no secrets, no
tokens, no PII (this file lives in a public repo).

## Who you are

- You are the **MINAI-HUB agent**.
- Access: the **public** `liivalaia/minai-hub` repo only.
- You do **not** have access to the private `liivalaia/minai` product repo, and you
  cannot read the private feedback Google Sheet. **You see only what the public
  sees.**

## Owner shortcuts (commands)

- **"MINAI-HUB"** → adopt this role: read this file and `AGENTS.md` first, then act
  as the MINAI-HUB agent within the scope and constraints below.
- **"paki ennast kokku"** ("pack yourself up") → update THIS file (and `AGENTS.md`
  if durable rules changed) to reflect the latest conversation + state, so the next
  agent can continue seamlessly. Keep it public-safe (no secrets/PII).

## What minai-hub is

The public front door around the private **minai** product. It is **not** the
product source of truth. First function: an **agent-readable feedback intake**.

## Architecture

- **Intake:** https://feedback.minai.ee → 301 → Google Apps Script web app →
  private Google Sheet. Agent-facing JSON, schema `minai.feedback/v1`. Requires a
  shared submit token shown on the live page (**never hard-code it here**). A valid
  POST returns `{"ok":true,"id":"fb_…","ack":"registered"}` and queues the item to
  the Sheet; a missing/invalid token is rejected. Plain `curl` cannot read the Apps
  Script echo response — verify receipt via the Sheet.
- **Storage:** private Google Sheet (not accessible to you without a Google MCP).
- **Mover:** a separate cross-repo agent (access to both `minai` and `minai-hub`)
  moves triaged feedback into private `minai`. This hub never writes to `minai`.
  The product side already reacts to intake (wake → commit tagged
  `[suhtlus→toode]`).

## Repo layout

- `README.md` — public front door (EE + short EN).
- `feedback/README.md` — "Tagasiside": how the agent-readable channel works.
- `.github/ISSUE_TEMPLATE/config.yml` — blank issues disabled, redirect to
  feedback.minai.ee.
- `docs/admin-triage.md` — owner/admin flow (read Sheet → triage → apply to private
  `minai`).
- `AGENTS.md` — durable agent guidance.

## Decisions log (why the design is what it is)

- Public MD-file inbox and public GitHub Issues/Discussions were **rejected** as the
  inbox — they are world-readable.
- Chose an external private intake; it evolved to the **feedback.minai.ee agent-JSON**
  endpoint. By design there is **no human web form** — feedback stays
  agent-readable/usable.
- Domain `minai.ee` is available; `feedback.minai.ee` is live (verified: valid POST
  → `ok:true` → queued to Sheet; no token → rejected).
- Merged to `main`: PR #1 (front door + channel), #3 (agent-only wording), #4 (API
  response note).

## Constraints / gotchas

- The cloud agent's **built-in `gh` token** has `pull_requests: write` but **not
  `issues: write`** → it cannot close/comment issues (fails "Resource not accessible
  by integration"). The owner added a **`GH_PAT`** secret (fine-grained, Issues
  read/write on this repo); secrets are injected only into **new** agent sessions, so
  use it from a fresh session.
- You cannot see the private `minai` repo or the feedback Sheet.
- Public repo → keep shared info minimal; **never commit secrets/PII**.
- **Authority:** the owner has granted full admin authority over `minai-hub` via
  agent-session instructions (push to `main`, merge PRs, change settings). The
  token-scope limit above still applies until `GH_PAT` is present.

## Open items (TODO)

- **Close smoke-test Issue #2** — needs a session where `GH_PAT` is available.
- **Google MCP** (owner sets it up in Cursor Desktop) → then verify feedback
  receipt, delete the setup TEST item if present (title "TEST — cloud agent e2e
  check (palun kustuta)", `instance_repo` "minai-hub-setup-e2e-test"), and build /
  assist the mover.
- Base `minai` docs that reference public Issues are **obsolete** → align later
  inside the private `minai` repo (not from here).

## Last updated

- 2026-08-03 — by the setup agent (this handoff created during initial minai-hub
  bring-up).
