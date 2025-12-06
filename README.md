---
disable-model-invocation: true
---

# InsightureAI Claude Commands

> **Design-doc-driven development toolkit for tech leads**

A curated set of Claude Code commands focused on what tech leads actually need: planning, reviewing against specs, documentation hygiene, and team workflows.

## Philosophy

- **Design doc compliance** — Bidirectional sync between code and specs
- **Documentation hygiene** — Find duplicates, capture ideas, keep docs clean
- **Framework-agnostic** — Works with any stack, not opinionated about Rails/React/etc
- **Focused, not exhaustive** — Commands that matter, not 57 you'll never use

## Installation

```bash
# Clone to Claude's commands directory
git clone https://github.com/insightureAI/claude-commands.git ~/.claude/commands

# Restart Claude Code to pick up new commands
```

### Update

```bash
cd ~/.claude/commands && git pull
```

## Workflow: Idea → Design → Code → Ship

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           IDEATION PHASE                                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  1. QUICK IDEA                        2. DEEP DISCUSSION                    │
│     ↓                                    ↓                                  │
│  /docs-capture-mkdocs                 [Have conversation with AI]           │
│  "Use ONNX for edge inference"           ↓                                  │
│     ↓                                 /docs-synthesize-mkdocs               │
│  Creates: docs/zh/decisions/0007-*       ↓                                  │
│                                       Creates: structured design doc         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                           DESIGN PHASE                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  3. REFINE DESIGN DOC                                                       │
│     - Review generated doc                                                  │
│     - Add details, constraints, requirements                                │
│     - Get team feedback                                                     │
│     ↓                                                                       │
│  Design doc ready: docs/zh/architecture/feature-x.md                        │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                         IMPLEMENTATION PHASE                                 │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  4. IMPLEMENT CODE                                                          │
│     "Implement the feature described in docs/zh/architecture/feature-x.md"  │
│     ↓                                                                       │
│  AI writes code based on design doc                                         │
│                                                                             │
│  5. SYNC CHECK                                                              │
│     ↓                                                                       │
│  /design-sync docs/zh/architecture/feature-x.md                             │
│     ↓                                                                       │
│  Reports misalignments, asks: "Which is correct? Code or Doc?"              │
│     ↓                                                                       │
│  You answer → AI fixes the appropriate side                                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                           REVIEW PHASE                                       │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  6. CODE QUALITY REVIEW                                                     │
│     ↓                                                                       │
│  /review                                                                    │
│     ↓                                                                       │
│  Security, Performance, Architecture, Code Quality checks                   │
│     ↓                                                                       │
│  Fix any issues found                                                       │
│                                                                             │
│  7. PR & SHIP                                                               │
│     ↓                                                                       │
│  /pr-enhance                                                                │
│     ↓                                                                       │
│  Auto-generate PR description → Merge                                       │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
                                    ↓
┌─────────────────────────────────────────────────────────────────────────────┐
│                          MAINTENANCE PHASE                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  8. PERIODIC AUDIT                                                          │
│     ↓                                                                       │
│  /docs-audit-mkdocs                                                         │
│     ↓                                                                       │
│  Find orphan docs, outdated content, missing translations                   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

## Commands

### Core Workflow

| Command | Purpose | Example |
|---------|---------|---------|
| `/plan <feature>` | Idea → actionable implementation plan | `/plan Add OAuth2 with JWT tokens` |
| `/review` | 4-perspective code quality review | `/review` |
| `/design-sync <doc>` | Bidirectional code ↔ design doc alignment | `/design-sync docs/specs/auth.md` |
| `/standup [days]` | Git activity → standup notes | `/standup` or `/standup 3` |
| `/subagents <tasks>` | Execute multiple tasks in parallel | `/subagents "Fix auth" "Add tests"` |

### Documentation (Generic)

| Command | Purpose | Example |
|---------|---------|---------|
| `/docs-audit` | Find duplicates, orphans, broken links | `/docs-audit docs/` |
| `/docs-capture <idea>` | Quick capture idea → structured doc | `/docs-capture Use Kalman filter` |
| `/docs-synthesize` | Distill conversation → structured doc | `/docs-synthesize` |

### Documentation (MkDocs)

For MkDocs-based documentation sites with i18n support:

| Command | Purpose | Example |
|---------|---------|---------|
| `/docs-audit-mkdocs` | Audit with translation coverage, nav awareness | `/docs-audit-mkdocs` |
| `/docs-capture-mkdocs <idea>` | Quick capture with ADR numbering, zh default | `/docs-capture-mkdocs Use ONNX` |
| `/docs-synthesize-mkdocs` | Conversation → doc with ADR format, Mermaid | `/docs-synthesize-mkdocs` |

### Code Quality

| Command | Purpose | Example |
|---------|---------|---------|
| `/tech-debt [path]` | Find and prioritize technical debt | `/tech-debt src/` |
| `/pr-enhance` | Auto-generate PR description | `/pr-enhance` |

### Team

| Command | Purpose | Example |
|---------|---------|---------|
| `/onboard [focus]` | Generate new developer onboarding guide | `/onboard backend` |

## What Makes This Different

### Bidirectional Design Sync

Code and docs drift apart. Traditional tools assume the doc is always right. We ask:

```bash
/design-sync docs/specs/auth.md
```

Output:
```markdown
| # | Design Doc Says | Code Does | Which is Correct? |
|---|-----------------|-----------|-------------------|
| 1 | Password reset required | Not implemented | ? |
| 2 | localStorage tokens | httpOnly cookies | ? |

Respond: "1: doc, 2: code" → I'll fix the appropriate side
```

### Conversation Synthesis

Had a long discussion? Don't lose the insights:

```bash
/docs-synthesize-mkdocs
```

- Prioritizes **later conclusions** over early exploratory thoughts
- Auto-numbers ADRs (0007, 0008, ...)
- Generates Mermaid diagrams from architecture discussions

### MkDocs-Aware Auditing

```bash
/docs-audit-mkdocs
```

- Recognizes `en/` ↔ `zh/` as translation pairs, not duplicates
- Reads `mkdocs.yml` nav for orphan detection
- Reports translation coverage gaps

## Agents

These agents are invoked by commands or can be used directly:

| Agent | Expertise | Invoked By |
|-------|-----------|------------|
| `code-reviewer` | Clean code, patterns, testability | `/review` |
| `security-auditor` | OWASP, auth, secrets, injection | `/review` |
| `design-compliance` | Requirements tracing, spec coverage | `/design-sync` |

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add or modify commands.

## Attribution

Built by [InsightureAI](https://github.com/insightureAI).

Inspired by patterns from:
- [wshobson/commands](https://github.com/wshobson/commands) (MIT License)
- [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)

## License

MIT License - see [LICENSE](LICENSE)
