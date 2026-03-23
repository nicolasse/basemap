# basemap

A context layer for multi-repo workspaces. Maps features across repositories with product definitions, engineering contracts, and implementation docs — designed for AI-assisted development with Claude Code.

## What it does

basemap sits on top of your repos and gives AI agents (and humans) a structured way to understand features that span multiple services. Each feature gets three files:

- **product.md** — what the feature does, use cases, business rules
- **engineering.md** — technical contracts, key interfaces, constraints
- **implementation.md** — how it's actually built today, key files, flows

Skills and agents use these files to implement new use cases, review contracts, and map existing code — all without losing context across repos.

## Structure

```
basemap/
  CLAUDE.md                              # workspace context
  repositories/                          # your repos go here
  features/
    CLAUDE.md                            # agent instructions
    _template/                           # templates for new features
    {feature-name}/                      # one dir per feature
      product.md
      engineering.md
      implementation.md
  .claude/
    skills/                              # user-invocable workflows
      add-use-case.md                    # implement a new use case
      map-feature-product.md             # generate product.md from code + conversation
      map-feature-engineering.md         # generate engineering.md from code
      map-feature-implementation.md      # generate implementation.md from code
    agents/                              # reusable worker agents
      feature-implementer.md             # writes code with feature context
      contract-reviewer.md               # validates contracts, read-only
```

## Getting started

1. Clone this repo (or copy the structure into your workspace)
2. Put your repos inside `repositories/`
3. Open the workspace in Claude Code
4. Run a skill: "map the product for follow-ups"

## Skills

| Skill | What it does |
|---|---|
| `map-feature-product` | Explores repos + talks to you to generate `product.md` |
| `map-feature-engineering` | Explores repos to extract technical contracts into `engineering.md` |
| `map-feature-implementation` | Explores repos to map current implementation into `implementation.md` |
| `add-use-case` | Implements a new use case end-to-end with contract validation |

## Agents

| Agent | What it does |
|---|---|
| `feature-implementer` | Writes code scoped to a feature, respecting its contracts |
| `contract-reviewer` | Validates code against product and engineering contracts (read-only) |
