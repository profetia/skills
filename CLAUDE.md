# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Structure

Registry for my Claude Code skills. Each skill is a directory containing `.claude/` configuration — SKILL.md, agents, hooks, commands, settings, etc. — exactly as it would appear in a target repo's own `.claude/` directory.

The `by-name/` directory contains skills for other repositories, inspired by nixpkgs.

```
by-name/
  rust-clippy/
    .claude/
      SKILL.md
```

To use a skill in another repo, symlink or copy its `.claude/` contents into that repo's own `.claude/` directory. No build step, no package manager — just files.

## Adding a Skill

1. Create a directory with a `.claude/` subdirectory, e.g. `by-name/<skill-name>/.claude/`
2. Add the skill's contents — SKILL.md, agents, hooks, commands, settings, etc.
3. The skill is ready to use — no registration or indexing needed
