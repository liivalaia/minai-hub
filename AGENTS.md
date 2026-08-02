# AGENTS.md

## Cursor Cloud specific instructions

`minai-hub` is the public side of the **minai** product. Right now it is a
documentation / Markdown repository, **not an application**: there are no
dependencies to install, and nothing to build, lint, or test. No update script
is needed for the environment.

Its first purpose is to be an **agent-readable feedback inbox**:

- Feedback lives as one Markdown file per item under `feedback/`.
- Each file uses light YAML frontmatter (`type: bug|feature`, `date:`) followed
  by a `## Summary` and optional `## Details`. See `feedback/README.md` for the
  format.
- To read the inbox, list `feedback/*.md` (ignore `feedback/README.md`, which is
  the format doc, not feedback) and parse the frontmatter + sections.

Keep the public surface minimal — avoid revealing more about minai than needed.
