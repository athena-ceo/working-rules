# working-rules

<!-- Copyright (c) 2025–2026 Athena Decision Systems SAS. All rights reserved. -->

The one place where Harley's general way of working is written down for the coding
agents (Claude Code, Codex) that work in the Athena projects: golden-path, xcape, hearts
and unweaver.

## What is here

| File | What it is |
|---|---|
| `general.md` | The rules. The only file to edit when a general rule changes. |
| `sync.py` | Writes a generated copy of the rules, and the check below, into a project. |
| `check.py` | Installed in each project as `scripts/lint-working-rules.py`. Fails when a project's copy was edited in place; warns when it is behind `general.md`. |

## Why each project carries a copy

A cloud session, another computer or a collaborator's machine sees one project
repository and nothing beside it. The rules therefore have to be inside every project.
Each project holds a generated copy at `.claude/rules/general.md`, which Claude Code
loads together with the project's own `CLAUDE.md`; the project's `AGENTS.md` points
Codex at the same two files.

The copies are generated and checked, never maintained by hand. What is specific to one
project stays in that project's `CLAUDE.md`.

## Changing a rule

1. Edit `general.md` here and commit it.
2. Roll it out — with the projects checked out beside this repository:

   ```bash
   python3 sync.py
   ```

   or, from inside one project:

   ```bash
   python3 ../working-rules/sync.py .
   ```

3. Review and commit the changed copy in each project.

`sync.py` commits nothing. With no arguments it updates every sibling folder that
already has a copy; name a project to install into it for the first time.

## Setting up another computer

Clone this repository beside the projects (for example `~/Development/working-rules`).
Nothing else is needed: the projects already contain their copy, and the clone is only
used to change a rule or to be told a copy is behind.
