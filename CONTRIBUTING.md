# Contributing to easydev

## Project Structure

```
easydev/
├── .claude-plugin/
│   ├── plugin.json           # Plugin manifest
│   └── marketplace.json      # Marketplace configuration
├── commands/                  # Slash commands (6 total)
│   ├── research.md
│   ├── design-sync.md
│   ├── docs-audit.md
│   ├── synthesize.md
│   ├── standup.md
│   └── onboard.md
├── agents/                    # Sub-agents (3 total)
│   ├── code-reviewer.md
│   ├── security-auditor.md
│   └── design-compliance.md
├── README.md
├── CONTRIBUTING.md
├── CHANGELOG.md
└── LICENSE
```

## Adding a New Command

### 1. Before Adding: Check Philosophy

We intentionally keep commands minimal. Before adding:

1. **Does an official plugin do this?** → Don't add, recommend the official one
2. **Does an existing command cover this?** → Extend that command instead
3. **Is this unique value we provide?** → Proceed with adding

### 2. Create the Command File

```bash
touch commands/your-command.md
```

### 3. Use This Template

```markdown
---
description: One-line description (shown in /easydev:help)
argument-hint: [required-arg] [--optional-flag]
---

# Command Name

You are [role description]. Your expertise includes [capabilities].

## Context

[When this command is useful]

## Auto-Detection Logic (if applicable)

**FIRST**: Check if [condition].

- **If detected**: [behavior]
- **If not detected**: [alternative behavior]

## Requirements

$ARGUMENTS

## Instructions

### 1. [First Phase]
[What to do]

### 2. [Second Phase]
[What to do]

## Output Format

[Markdown template for output]
```

### 4. Test Your Command

```bash
# In Claude Code with the plugin installed
/easydev:your-command test-input
```

### 5. Submit PR

- Update CHANGELOG.md with the new command
- Explain the unique value in PR description
- Include example usage

## Modifying Existing Commands

1. Read the current command file thoroughly
2. Make your changes
3. Test with real scenarios
4. Submit PR with before/after examples

## Adding an Agent

Agents live in `agents/` and are invoked by commands or directly.

### Template

```markdown
# Agent Name

You are [expertise description].

## Context

[When this agent is invoked]

## Instructions

### 1. [Category of Checks]
[Specific checks to perform]

### 2. [Category of Checks]
[Specific checks to perform]

## Output Format

[Severity-rated findings template]
```

## Naming Conventions

- **Commands**: kebab-case in filename: `docs-audit.md` → `/easydev:docs-audit`
- **Agents**: kebab-case in filename: `code-reviewer.md`
- **Descriptions**: Start with verb, be concise

## Code Style

- Keep frontmatter minimal
- Use `$ARGUMENTS` to reference command arguments
- Include clear output format templates
- Add auto-detection logic when behavior differs by context

## Questions?

Open an issue at [github.com/easydev-ai/easydev/issues](https://github.com/easydev-ai/easydev/issues)
