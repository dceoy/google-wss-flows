---
name: github-projects-manager
description: Manage GitHub Projects v2 via GitHub CLI and GraphQL, including project discovery, issue/PR triage, field updates (status, date, iteration, single-select), and backlog reporting. Use when asked to organize, prioritize, or automate GitHub Project boards.
---

# GitHub Projects Manager

Use this skill to execute reliable, repeatable GitHub Projects v2 operations.

## Required setup

1. Confirm auth and scopes.
2. Resolve owner/repo/project before mutations.
3. Discover field and option IDs dynamically.

```bash
gh auth status
gh auth refresh -s read:project,project,repo
```

## Core workflow

1. **Resolve project**: find project number, project ID, and URL.
2. **Inspect schema**: list fields and options (especially status/iteration/select).
3. **Resolve content**: locate issue/PR IDs and existing project items.
4. **Mutate safely**: only create/update when target state differs.
5. **Report**: output performed commands and resulting IDs/URLs.

Prefer command helpers from `scripts/project_queries.sh` and references from `references/graphql-snippets.md`.

## Guardrails

- Always check for existing item before adding an issue/PR to a project.
- Always fetch select/iteration options before updating those field values.
- For batch updates, dry-run by printing planned mutations first.
- Treat missing permissions as recoverable: report exact scope requirements.

## Common tasks

- Add issue/PR to project.
- Set status, priority, estimate, due date.
- Move items through workflow stages.
- Generate backlog views (e.g., "Ready", "Blocked", "This Sprint").

## Deliverable format

- Project: `title (#number)`, `projectId`, URL.
- Item-level results: content URL, item ID, changed fields.
- Explicit no-op notes for already-correct state.
