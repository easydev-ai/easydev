# easydev

> Developer productivity toolkit for Claude Code — research, design-sync, documentation, and workflow automation.

A focused plugin with 6 essential commands that complement (not duplicate) official Anthropic plugins.

## Philosophy

- **Complement, don't compete** — Use official plugins for code review, feature development, commits. This plugin fills the gaps.
- **Smart auto-detection** — Commands detect MkDocs, i18n, and project structure automatically.
- **Code is truth** — Every command treats code as the source of truth, not assumptions.
- **Parallel by default** — Research and auditing spawn multiple sub-agents for speed.

## Installation

### From Marketplace

```bash
# Add the easydev-ai marketplace
/plugin marketplace add easydev-ai/easydev

# Install the plugin
/plugin install easydev@easydev-ai
```

### Manual Installation

```bash
# Clone to your plugins directory
git clone https://github.com/easydev-ai/easydev ~/.claude/plugins/easydev
```

Restart Claude Code after installation.

## Commands

| Command | Description | Use When |
|---------|-------------|----------|
| `/easydev:research` | Deep research + codebase investigation with parallel sub-agents | "Is X applicable to us?" "Why is Y breaking?" |
| `/easydev:design-sync` | Bidirectional code ↔ design doc alignment | Code and spec have drifted apart |
| `/easydev:docs-audit` | Audit docs for duplicates, orphans, broken links (auto-detects MkDocs) | Documentation cleanup needed |
| `/easydev:synthesize` | Distill conversation into structured documentation | Long discussion needs to become permanent docs |
| `/easydev:standup` | Generate standup notes from git activity | Daily standup prep |
| `/easydev:onboard` | Generate comprehensive onboarding documentation | New team member joining |

## Command Details

### `/easydev:research <question> [code-paths...]`

Your most powerful research tool. Spawns parallel sub-agents to investigate:

```bash
# Research a technology
/easydev:research Is API Gateway HTTP API applicable to our lambda/processor?

# Investigate a bug
/easydev:research Why are transcriptions failing for large files? src/services/audio/ --mode investigate

# Compare options
/easydev:research Should we switch from REST to GraphQL?
```

**Modes:**
- `research` — External research, technology evaluation
- `investigate` — Deep codebase analysis, dependency mapping
- `auto` (default) — Intelligently combines both

**Features:**
- Parallel sub-agent execution (4+ agents at once)
- Blast radius analysis for code changes
- Evidence-based recommendations with sources

---

### `/easydev:design-sync <design-doc-path> [code-path]`

Identifies mismatches between design documents and code, then asks YOU which direction to fix:

```bash
/easydev:design-sync docs/specs/auth.md src/auth/
```

**Output:**
```markdown
| # | Design Doc Says | Code Does | Which is Correct? |
|---|-----------------|-----------|-------------------|
| 1 | Password reset required | Not implemented | ? |
| 2 | localStorage tokens | httpOnly cookies | ? |

Respond: "1: doc, 2: code" to specify fix direction
```

**Why this is unique:** Most tools assume the spec is always right. This command recognizes that sometimes code evolved past the spec.

---

### `/easydev:docs-audit [target-path]`

Smart documentation auditing that auto-detects your documentation system:

```bash
# Audit all docs
/easydev:docs-audit docs/

# Focus on specific issues
/easydev:docs-audit --focus duplicates
/easydev:docs-audit --focus translations --lang zh
```

**Auto-detects:**
- MkDocs (checks for `mkdocs.yml`) → i18n-aware, nav validation
- Generic → File-based auditing, duplicate detection

**Finds:**
- Duplicate content (exact and semantic)
- Orphan files (not linked anywhere)
- Broken internal links
- Translation gaps (MkDocs mode)
- Nav mismatches (MkDocs mode)

---

### `/easydev:synthesize`

Distills a conversation into permanent, structured documentation:

```bash
# After a long discussion
/easydev:synthesize

# With specific options
/easydev:synthesize --category decision --title "Authentication Strategy"
```

**Key feature:** Prioritizes later conclusions over earlier exploration. If you discussed Redis, then MySQL, then decided PostgreSQL — the doc reflects PostgreSQL as the decision.

**Auto-detects:**
- MkDocs → ADR numbering, i18n folders, nav suggestions
- Generic → Standard markdown output

---

### `/easydev:standup [days]`

Generates standup notes from git activity:

```bash
/easydev:standup      # Yesterday's activity
/easydev:standup 3    # Last 3 days
```

**Output:**
```markdown
*Standup 2025-12-15*

✅ *Done:* Merged OAuth PR #123, fixed token refresh bug
🔄 *Today:* Password reset flow, integration tests
🚧 *Blocked:* PR #126 awaiting review (2d)
```

---

### `/easydev:onboard [--focus setup|architecture|workflows]`

Generates comprehensive onboarding documentation by analyzing your codebase:

```bash
/easydev:onboard
/easydev:onboard --focus backend
```

**Generates:**
- Tech stack overview
- Prerequisites and setup instructions
- Project structure guide
- Available commands
- Development workflow
- Troubleshooting guide

## Agents

These agents are invoked by commands or can be used directly:

| Agent | Expertise | Invoked By |
|-------|-----------|------------|
| `code-reviewer` | Clean code, patterns, testability | Review workflows |
| `security-auditor` | OWASP, auth, secrets, injection | Security checks |
| `design-compliance` | Requirements tracing, spec coverage | `/easydev:design-sync` |

## Using with Official Plugins

This plugin is designed to work alongside official Anthropic plugins:

| Task | Use Official Plugin | Use easydev |
|------|---------------------|-------------|
| Code review | `/code-review:code-review` | — |
| Feature development | `/feature-dev:feature-dev` | — |
| Commits & PRs | `/commit-commands:*` | — |
| **Research & evaluation** | — | `/easydev:research` |
| **Design-code sync** | — | `/easydev:design-sync` |
| **Documentation audit** | — | `/easydev:docs-audit` |
| **Conversation → docs** | — | `/easydev:synthesize` |
| **Standup notes** | — | `/easydev:standup` |
| **Onboarding docs** | — | `/easydev:onboard` |

**Recommended plugin setup:**
```bash
# Official plugins
/plugin install feature-dev@anthropics-claude-code
/plugin install code-review@anthropics-claude-code
/plugin install commit-commands@anthropics-claude-code

# This plugin
/plugin install easydev@easydev-ai
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add or modify commands.

## License

MIT License - see [LICENSE](LICENSE)

---

Built by [EasyDev AI](https://github.com/easydev-ai)
