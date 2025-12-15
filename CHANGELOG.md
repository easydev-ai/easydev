# Changelog

All notable changes to easydev will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [2.1.0] - 2025-12-15

### Added
- **`/easydev:docs-refresh`** — Batch-update documentation to match current code state
  - Parallel sub-agents for API docs, setup docs, architecture, tutorials
  - Staleness detection with severity levels (Critical, Stale, Fresh)
  - Surgical updates that preserve human-written context
  - Auto-detects MkDocs for i18n-aware updates

---

## [2.0.0] - 2025-12-15 — Major Restructuring

### Breaking Changes
- **Renamed from `insightureAI-claude-commands` to `easydev`**
- **Reduced from 16 commands to 6 focused commands**
- **Converted from user commands to Claude Code plugin**
- **Moved repository from `insightureAI` to `easydev-ai` org**

### Removed Commands (Deprecated in Favor of Official Plugins)
| Removed | Use Instead |
|---------|-------------|
| `/commands:review` | `/code-review:code-review` (official) |
| `/commands:plan` | `/feature-dev:feature-dev` (official) |
| `/commands:pr-enhance` | `/commit-commands:commit-push-pr` (official) |
| `/commands:tech-debt` | `/code-review:code-review` (official) |
| `/commands:subagents` | Built-in Task tool parallelization |
| `/commands:docs-capture` | Merged into `/easydev:docs-audit` |
| `/commands:docs-capture-mkdocs` | Merged into `/easydev:docs-audit` |
| `/commands:docs-cleanup` | Merged into `/easydev:docs-audit` |
| `/commands:docs-audit` (generic) | Merged with MkDocs version |
| `/commands:docs-synthesize` (generic) | Merged with MkDocs version |

### New Command Names
| Old Name | New Name |
|----------|----------|
| `/commands:research-evaluate` | `/easydev:research` |
| `/commands:design-sync` | `/easydev:design-sync` |
| `/commands:docs-audit-mkdocs` | `/easydev:docs-audit` |
| `/commands:docs-synthesize-mkdocs` | `/easydev:synthesize` |
| `/commands:standup` | `/easydev:standup` |
| `/commands:onboard` | `/easydev:onboard` |

### Added
- **Plugin structure** with `.claude-plugin/plugin.json` manifest
- **Marketplace support** for installation via `/plugin install easydev@easydev-ai`
- **Auto-detection logic** in `docs-audit` and `synthesize` (detects MkDocs automatically)
- **Comprehensive README** with usage examples and comparison to official plugins

### Changed
- Commands now use `easydev:` prefix instead of `commands:`
- All commands enhanced with smart auto-detection where applicable
- Philosophy: "Complement official plugins, don't compete"

---

## [1.1.0] - 2025-12-10

### Added
- `/subagents` - Execute multiple tasks in parallel using subagents via the Task tool
- `/docs-audit-mkdocs` - MkDocs-aware documentation auditing with i18n support
- `/docs-synthesize-mkdocs` - MkDocs-aware conversation synthesis with ADR numbering
- `/docs-capture-mkdocs` - MkDocs-aware idea capture
- `/research-evaluate` - Unified research and codebase investigation

### Changed
- `/review` now includes design doc compliance as optional focus area

---

## [1.0.0] - 2025-12-05

### Added

#### Commands
- `/plan` - Transform feature ideas into actionable implementation plans
- `/review` - Multi-perspective code review with design doc compliance
- `/standup` - Generate standup notes from git activity
- `/tech-debt` - Assess technical debt with severity scoring
- `/pr-enhance` - Auto-generate comprehensive PR descriptions
- `/onboard` - Generate new developer onboarding guides
- `/docs-audit` - Find duplicate/messy docs and propose consolidation
- `/docs-capture` - Capture ideas into clean, organized documentation
- `/design-sync` - Bidirectional code ↔ design doc alignment

#### Agents
- `code-reviewer` - Comprehensive code quality review
- `security-auditor` - Security vulnerability assessment (OWASP Top 10)
- `design-compliance` - Verify code matches design specifications

---

## Version History

| Version | Date | Highlights |
|---------|------|------------|
| 2.1.0 | 2025-12-15 | Added `/easydev:docs-refresh` for batch documentation updates |
| 2.0.0 | 2025-12-15 | Major restructuring: 16→6 commands, plugin format, easydev branding |
| 1.1.0 | 2025-12-10 | Added MkDocs variants, research-evaluate, subagents |
| 1.0.0 | 2025-12-05 | Initial release with 8 commands, 3 agents |
