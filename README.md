# .specify/ — Speckit Framework

This directory contains the Speckit spec-driven development framework: extensions, templates, scripts, and workflows for building features through specification → plan → tasks → implementation.

## Directory Structure

```
.specify/
├── extensions.yml              # Hook definitions (before/after lifecycle events)
├── init-options.json           # AI integration, branch numbering, script preference
├── integration.json            # Integration state for OpenCode
├── extensions/
│   ├── .registry               # Registered extensions (git, agents)
│   ├── git/                    # Git extension (branching, auto-commit)
│   │   ├── config-template.yml # Default git config
│   │   ├── extension.yml       # Extension metadata
│   │   ├── git-config.yml      # Active config
│   │   ├── README.md           # Git extension docs
│   │   └── scripts/            # Bash + PowerShell scripts
│   └── agents/
│       ├── agents-config.yml   # Tech stack → engineer/skill mapping
│       └── extension.yml       # Extension metadata
├── integrations/
│   ├── opencode.manifest.json  # File hashes for OpenCode commands
│   └── speckit.manifest.json   # File hashes for Speckit files
├── memory/
│   └── constitution.md         # Project principles and governance (filled)
├── scripts/
│   ├── bash/                   # Bash scripts (check-prerequisites, create-feature, etc.)
│   └── powershell/             # PowerShell equivalents
├── templates/
│   ├── spec-template.md        # Feature specification template
│   ├── plan-template.md        # Implementation plan template (pre-filled for this stack)
│   ├── tasks-template.md       # Task list template (lean structure)
│   ├── tasks-guide.md          # Detailed guide for task usage
│   ├── checklist-template.md   # Quality checklist template
│   └── constitution-template.md# Project constitution template (reference)
└── workflows/
    ├── workflow-registry.json  # Registered workflows
    └── speckit/
        └── workflow.yml        # Full SDD cycle: specify → plan → tasks → implement
```

## How Speckit Works

### The Workflow

```
/specify "description"  →  specs/NNN-feature/spec.md
/plan                   →  specs/NNN-feature/plan.md
/tasks                  →  specs/NNN-feature/tasks.md
/implement              →  Code generated from tasks
```

Each step produces an artifact that feeds into the next:
1. **Spec**: User-focused requirements (no tech details)
2. **Plan**: Technical architecture, API contracts, data models
3. **Tasks**: Ordered, actionable tasks with file paths
4. **Implement**: Code generation following tasks

### Extension Hooks

Hooks run automatically before/after core commands. Defined in `extensions.yml`:

| Event | Extension | Command | When |
|-------|-----------|---------|------|
| `before_specify` | git | `speckit.git.feature` | Create feature branch |
| `before_constitution` | git | `speckit.git.initialize` | Initialize git repo |
| `before_plan` | agents | `speckit.agent.select` | Select engineer agent |
| `before_plan` | git | `speckit.git.commit` | Auto-commit |
| `after_*` | git | `speckit.git.commit` | Auto-commit after each step |

Configure hook behavior in `.specify/extensions/git/git-config.yml`.

### Agent Selection

When `/speckit.plan` runs, the `speckit.agent.select` command:
1. Reads `spec.md`/`plan.md` for tech stack keywords
2. Matches patterns in `extensions/agents/agents-config.yml`
3. Loads the matched engineer's `SYSTEM.md` from `.agents/system/engineers/`
4. Loads matching skill `SKILL.md` files from `.agents/skills/system_skills/`

See `agents-config.yml` for the full pattern → agent/skill mapping.

## Customizing Templates

### For Your Project Stack

The templates in this directory are pre-configured for:
- **Backend**: NestJS + TypeScript + Prisma + PostgreSQL
- **Admin**: React + TypeScript + Vite + Ant Design + TanStack Query
- **Mobile**: Flutter + Clean Architecture + BLoC + GoRouter + GetIt

To customize for a different stack:
1. Edit `plan-template.md` → Update Technical Context and Project Structure sections
2. Edit `tasks-template.md` → Update default task paths and phase structure
3. Edit `agents-config.yml` → Update tech stack patterns and engineer mappings

### Adding New Templates

1. Create file in `templates/` with `.md` extension
2. Use placeholders like `[FEATURE_NAME]`, `[DATE]` for dynamic content
3. Reference from commands or workflows as needed

## Adding Extensions

1. Create directory under `extensions/<name>/`
2. Add `extension.yml` with metadata, commands, hooks
3. Register in `extensions.yml` under `installed:`
4. Add to `.registry` with version and command list
5. Add hooks to `extensions.yml` under appropriate event keys

## Key Files

| File | Purpose |
|------|---------|
| `extensions.yml` | Hook lifecycle — what runs before/after each Speckit command |
| `init-options.json` | AI integration choice, branch numbering mode, script language |
| `memory/constitution.md` | Project principles — non-negotiable rules for all development |
| `extensions/agents/agents-config.yml` | Tech stack detection → engineer/skill selection |
| `extensions/git/git-config.yml` | Auto-commit settings, branch numbering |
| `workflows/speckit/workflow.yml` | Full SDD cycle definition with review gates |
