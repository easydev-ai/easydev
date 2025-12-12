---
description: Comprehensive documentation audit and cleanup using docs skills (duplicate checker, placement advisor, health checker, content writer)
---

# Documentation Cleanup Workflow

## Pre-Flight

```bash
pwd && date
```

Confirm you're in the correct repository and note the timestamp.

## Core Principles

- **Don't assume** - Read files as source of truth
- **Code > Docs** - When conflict exists, code is correct
- **Single source of truth** - Every piece of info lives in ONE place only

## Phase 1: Health Check

Use `docs-health-checker` skill:

- Check nav vs filesystem (find broken nav entries)
- Find orphan files (exist but not in nav)
- Validate internal links
- Check index completeness (each index links to its section files)

**Output**: List all issues found before proceeding.

## Phase 2: Duplication Audit

Use `docs-duplicate-checker` skill:

- Search for repeated H2/H3 headings across files
- Find similar content blocks
- Identify glossary term re-definitions
- Check reference/ for content (should be URLs only)

**Output**: List all duplicates with file locations.

## Phase 3: Placement Review

Use `docs-placement-advisor` skill for any misplaced content:

- Analyze content type and audience
- Recommend correct location per section purpose:
  - `product/` → business, market, MVP
  - `design/` → architecture, algorithms
  - `design/research/` → background research
  - `design/decisions/` → ADRs only
  - `components/` → hardware specs
  - `platform/` → software implementation
  - `reference/` → URLs ONLY

**Output**: List files needing move/merge with recommendations.

## Phase 4: Create Fix Plan

Based on findings, create prioritized fix plan:

```markdown
| Priority | Issue | File | Action |
|----------|-------|------|--------|
| 🔴 Critical | {issue} | {file} | {action} |
| 🟠 Warning | {issue} | {file} | {action} |
| 🟢 Minor | {issue} | {file} | {action} |
```

**Present plan to user for approval before proceeding.**

## Phase 5: Execute Fixes

Use `docs-content-writer` skill for each approved fix:

- **Ask approval before each file change**
- Update mkdocs.yml nav if needed
- Add cross-references to related docs
- Verify no new duplicates introduced

## Subagent Strategy (for large repos)

For repos with 10+ files or multiple sections, spawn parallel subagents:

```text
Main Agent
├── Subagent: product/ audit
├── Subagent: design/ audit
├── Subagent: components/ audit
└── Subagent: platform/ audit

Each subagent runs Phase 1-3 for its section.
Main agent consolidates and executes Phase 4-5.
```

## Post-Cleanup Verification

```bash
npm run lint:md      # Markdown linting
npm run lint:links   # Link validation
npm run test:build   # Build test
```

All checks must pass before considering cleanup complete.
