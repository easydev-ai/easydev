# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

easydev is a **Claude Code plugin** that provides developer productivity commands. It complements (not duplicates) official Anthropic plugins by focusing on research, design-code sync, documentation workflows, and standup automation.

**Plugin Type**: Declarative markdown-based commands and agents (no build process)

## Project Structure

```
easydev/
├── .claude-plugin/
│   └── plugin.json           # Plugin manifest (name, version, metadata)
├── commands/                  # Slash commands (6 total)
│   ├── research.md           # Deep research + codebase investigation
│   ├── design-sync.md        # Bidirectional code ↔ design doc alignment
│   ├── docs-audit.md         # Documentation auditing (auto-detects MkDocs)
│   ├── synthesize.md         # Conversation → structured documentation
│   ├── standup.md            # Standup notes from git activity
│   └── onboard.md            # Generate onboarding documentation
├── agents/                    # Sub-agents invoked by commands
│   ├── code-reviewer.md      # Code quality expertise
│   ├── security-auditor.md   # OWASP/security expertise
│   └── design-compliance.md  # Requirements tracing
└── README.md, CONTRIBUTING.md, CHANGELOG.md
```

## Architecture

### Command File Format

Each command is a markdown file with YAML frontmatter:

```markdown
---
description: Short description (shown in /easydev:help)
argument-hint: <required> [optional] [--flag value]
---

# Command Title

You are [role]. Your expertise includes [capabilities].

## Instructions
[Detailed prompt for Claude to follow when command is invoked]

## Output Format
[Template for expected output]
```

**Key conventions**:
- `$ARGUMENTS` placeholder references user-provided arguments
- Auto-detection logic (e.g., checking for `mkdocs.yml`) adapts behavior
- Output templates use markdown with severity indicators (🔴🟡🟢)

### Agent File Format

Agents are simpler — just role definition and instructions without frontmatter:

```markdown
# Agent Name

You are [expertise description].

## Instructions
[What checks/analysis to perform]

## Output Format
[How to structure findings]
```

### Naming Conventions

- Commands: `kebab-case.md` → invoked as `/easydev:kebab-case`
- Agents: `kebab-case.md` → referenced by commands via Task tool

## Design Philosophy

1. **Complement, don't compete** — Use official plugins for code review (`/code-review:*`), feature development (`/feature-dev:*`), commits (`/commit-commands:*`). This plugin fills gaps.

2. **Code is truth** — Commands like `/easydev:research` and `/easydev:design-sync` verify against actual code, not assumptions.

3. **Smart auto-detection** — Commands detect MkDocs, i18n, project structure and adapt behavior automatically.

4. **Parallel by default** — `/easydev:research` spawns multiple sub-agents for parallel investigation.

## Testing Commands

Since this is a plugin, "testing" means invoking commands in Claude Code:

```bash
# In Claude Code with plugin installed:
/easydev:research Is X applicable to our codebase?
/easydev:design-sync docs/spec.md src/feature/
/easydev:docs-audit docs/ --focus duplicates
/easydev:synthesize --category decision
/easydev:standup 3
/easydev:onboard --focus setup
```

## Modifying Commands

1. Read existing command file thoroughly
2. Preserve frontmatter format (`description`, `argument-hint`)
3. Keep `$ARGUMENTS` placeholder for user input
4. Include clear output format templates
5. Add auto-detection logic when behavior differs by context (MkDocs vs generic)

## Adding New Commands

Before adding, check:
1. Does an official plugin do this? → Don't add
2. Does an existing command cover this? → Extend instead
3. Is this unique value? → Proceed

Create `commands/your-command.md` following the template in CONTRIBUTING.md.

## Key Files to Understand

- `commands/research.md` — Most complex command; demonstrates parallel sub-agent spawning, multi-phase analysis, output templates
- `commands/design-sync.md` — Shows bidirectional sync pattern (code→doc or doc→code)
- `commands/docs-audit.md` — Shows MkDocs auto-detection and mode switching
