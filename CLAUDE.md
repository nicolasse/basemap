# Workspace

This is a multi-repo workspace.

## Structure

- `repositories/` — All repos live here. Each subdirectory is a repo.
- `features/` — Product, engineering, and implementation context for each feature. See `features/CLAUDE.md`.
- `.claude/skills/` — User-invocable workflows
- `.claude/agents/` — Reusable worker agents

## Repos

The repos are all directories inside `repositories/`. To discover available repos, list that directory. Do not hardcode repo names — they may change.

## Features Context

The `features/` directory contains the source of truth for understanding, implementing, and validating changes across repos.

When working on a feature, always check `features/` for existing context before exploring repos from scratch.
