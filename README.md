# basemap

A context layer for multi-repo workspaces. Maps features across repositories with product definitions, engineering contracts, and implementation docs — designed for AI-assisted development with Claude Code.

## What it does

basemap sits on top of your repos and gives AI agents (and humans) a structured way to understand features that span multiple services. Each feature gets three files:

- **product.md** — what the feature does, use cases, business rules
- **engineering.md** — technical contracts, key interfaces, constraints
- **implementation.md** — how it's actually built today, key files, flows

Commands and agents use these files to implement new use cases, review contracts, and map existing code — all without losing context across repos.

## Getting started

```bash
# 1. Clone basemap as your workspace
git clone git@github.com:nicolasse/basemap.git my-workspace
cd my-workspace

# 2. Set up your project context
cd features
git init  # or clone an existing features repo
cd ..

# 3. Clone your repos
cd repositories
git clone git@github.com:your-org/repo-a.git
git clone git@github.com:your-org/repo-b.git
cd ..

# 4. Open Claude Code
claude
```

## Three layers of git

basemap separates the framework from the project context from the code:

```
my-workspace/                ← basemap git (the framework)
  .claude/
    commands/                ← bm- prefixed commands
    agents/                  ← worker agents
  features/                  ← project context git (your team's knowledge)
    CLAUDE.md                ← part of basemap
    _template/               ← part of basemap
    follow-up/               ← your project context
    payments/                ← your project context
  repositories/              ← each repo has its own git
    repo-a/
    repo-b/
```

| Layer | What it is | Who shares it |
|---|---|---|
| **basemap** (root git) | Framework: commands, agents, templates | Everyone using basemap |
| **features/** (its own git) | Project context: product, engineering, implementation docs | Your team working on this project |
| **repositories/** (each its own git) | The actual code | Depends on the repo |

This means you can:
- Update basemap independently (pull new commands/agents)
- Share project context with your team without coupling it to basemap
- Use the same basemap setup for completely different projects

## Commands

| Command | What it does |
|---|---|
| `/bm-add-feature` | Design and implement a new feature from scratch |
| `/bm-add-use-case` | Add a use case to an existing feature with contract validation |
| `/bm-map-feature-product` | Explores repos + talks to you → generates `product.md` |
| `/bm-map-feature-engineering` | Explores repos → extracts technical contracts into `engineering.md` |
| `/bm-map-feature-implementation` | Explores repos → maps current implementation into `implementation.md` |

## Agents

| Agent | Color | What it does |
|---|---|---|
| `feature-implementer` | 🔵 blue | Writes code scoped to a feature, respecting its contracts |
| `contract-reviewer` | 🟡 yellow | Validates code against product and engineering contracts (read-only) |

## Workflow

**New feature (doesn't exist in code):**
1. `/bm-add-feature` — designs product + engineering, implements, validates, documents

**Existing feature (already in code, needs context files):**
1. `/bm-map-feature-product` → generates `product.md`
2. `/bm-map-feature-engineering` → generates `engineering.md`
3. `/bm-map-feature-implementation` → generates `implementation.md`

**Adding behavior to an existing feature:**
1. `/bm-add-use-case` — implements, validates contracts, updates context files
