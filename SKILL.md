---
name: skills
description: Set up Claude Code on a new machine with the right plugins and skills for the machine type — general (every machine), desktop (GUI environment with browser and local apps), or dev (headless development machine accessed via SSH). Use this whenever setting up Claude Code for the first time, reinstalling, or asked to install recommended plugins.
---

# Claude Code Setup

## Machine Types

| Type | Environment | What happens there |
|---|---|---|
| **Desktop** | GUI, browser, local apps | Browse, open documents, run browsers |
| **Dev** | Headless, accessed via SSH + VS Code | Code, builds, git |

A machine can be both — install both sets.

## Marketplace Setup

Before installing, add these marketplaces:

```
/plugin marketplace add anthropics/skills
/plugin marketplace add forrestchang/andrej-karpathy-skills
```

## Plugins

### General — every machine

```bash
claude plugins install superpowers@claude-plugins-official
claude plugins install remember@claude-plugins-official
claude plugins install skill-creator@claude-plugins-official
claude plugins install claude-md-management@claude-plugins-official
claude plugins install claude-code-setup@claude-plugins-official
claude plugins install security-guidance@claude-plugins-official
claude plugins install context7@claude-plugins-official
claude plugins install hookify@claude-plugins-official
claude plugins install andrej-karpathy-skills@karpathy-skills
```

- **superpowers**: brainstorming, debugging, TDD, plan execution — foundational workflow skills.
- **remember**: persistent memory across sessions and machines.
- **skill-creator**: create and iterate on skills.
- **claude-md-management**: keep CLAUDE.md files healthy.
- **claude-code-setup**: configure hooks, settings, automations.
- **security-guidance**: lightweight security awareness.
- **context7**: real-time library and docs context.
- **hookify**: generate hooks from natural language.
- **andrej-karpathy-skills**: coding discipline — think before coding, simplicity first, surgical changes, goal-driven execution.

### Desktop — GUI environment

```bash
claude plugins install playwright@claude-plugins-official
claude plugins install document-skills@anthropic-agent-skills
```

- **playwright**: drives a real browser. Needs a local browser runtime — a headless dev machine can't run one.
- **document-skills**: creates `.docx` `.pptx` `.xlsx` `.pdf` files. These need native apps (Office, PDF reader) to open and review. Install on the desktop where you can double-click to view the output.

### Dev — headless, where the code lives

```bash
claude plugins install commit-commands@claude-plugins-official
claude plugins install code-review@claude-plugins-official
claude plugins install code-simplifier@claude-plugins-official
```

- **commit-commands**: structured commit workflows. The repo is on dev.
- **code-review**: systematic code review. Code lives here.
- **code-simplifier**: simplification and reuse improvements.

### LSPs — per project

Don't globally install LSP plugins. They're language-specific and project-dependent. When setting up a project on a dev machine, ask which languages are used, then install only the matching LSPs.

---

## Procedure

1. **Add marketplaces**: `anthropics/skills` and `forrestchang/andrej-karpathy-skills`
2. **Detect** machine type — ask if not obvious.
3. **Install General plugins**.
4. **Install machine-specific plugins**:
   - Desktop: `playwright`, `document-skills`
   - Dev: `commit-commands`, `code-review`, `code-simplifier`
5. **For dev projects**: ask which languages, install matching LSPs.
6. **Verify**: `claude plugins list`.
