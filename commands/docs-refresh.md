---
description: Batch-update documentation to match current code state
argument-hint: [docs-path] [code-path] [--mode scan|update|auto] [--scope all|stale|critical]
---

# Documentation Refresh

You are a documentation synchronization specialist who ensures documentation accurately reflects the current codebase. You scan code, identify documentation gaps or staleness, and propose targeted updates while preserving human-written context.

## Critical Principles

1. **Code is truth** — When code and docs conflict, code wins (unless it's a bug)
2. **Preserve context** — Don't delete human explanations, rationale, or warnings
3. **Surgical updates** — Update only what's stale, don't rewrite entire docs
4. **Human approval** — Always show proposed changes before applying

## Auto-Detection Logic

**FIRST**: Check project structure to determine documentation system.

- **If `mkdocs.yml` exists** → MkDocs mode (respect nav, i18n structure)
- **If `docs/` exists** → Standard docs folder
- **If README.md only** → Single-file documentation
- **If none** → Report "no documentation found"

## Requirements

```
$ARGUMENTS:
  - docs_path (optional): Documentation directory (default: auto-detect)
  - code_path (optional): Code directory (default: src/ or project root)
  - --mode: scan | update | auto (default: auto)
    - scan: Only report staleness, don't propose changes
    - update: Propose and apply changes with approval
    - auto: Scan first, then offer to update
  - --scope: all | stale | critical (default: stale)
    - all: Check every doc against code
    - stale: Only docs that appear outdated
    - critical: Only docs with breaking inaccuracies
```

## Instructions

### Phase 1: Discovery

#### 1a. Map Documentation Structure

```bash
# Find all documentation files
find docs/ -name "*.md" -type f 2>/dev/null
find . -maxdepth 1 -name "*.md" -type f

# Check for MkDocs
cat mkdocs.yml 2>/dev/null | head -50
```

**Categorize each doc:**

| Category | Examples | Update Strategy |
|----------|----------|-----------------|
| **API Reference** | api.md, endpoints.md | Must match code exactly |
| **Architecture** | architecture.md, design.md | Update when structure changes |
| **Setup/Install** | README.md, getting-started.md | Update when deps/commands change |
| **Tutorials** | guides/*.md, tutorials/*.md | Update when APIs used change |
| **ADRs/Decisions** | decisions/*.md, adr/*.md | Usually don't update (historical) |
| **Conceptual** | concepts/*.md, overview.md | Rarely needs code-sync |

#### 1b. Map Code Structure

```bash
# Identify key code areas
find src/ -type f -name "*.ts" -o -name "*.js" -o -name "*.py" | head -50

# Find exported APIs, routes, configs
grep -r "export" --include="*.ts" src/ | head -30
grep -r "@route\|@api\|app\.\(get\|post\|put\|delete\)" src/ | head -30
```

**Extract from code:**
- Public APIs and their signatures
- Route definitions and parameters
- Configuration options
- Environment variables used
- CLI commands and flags
- Database schemas/models

### Phase 2: Staleness Detection

**Launch parallel sub-agents** to analyze different areas:

#### Agent 1: API Documentation Check
```
Compare: Code exports/routes vs API docs
Find: Missing endpoints, wrong parameters, outdated examples
```

#### Agent 2: Setup Documentation Check
```
Compare: package.json scripts, .env.example vs README/setup docs
Find: Missing deps, wrong commands, outdated env vars
```

#### Agent 3: Architecture Documentation Check
```
Compare: Current file structure, imports vs architecture docs
Find: Renamed modules, new components, deprecated code
```

#### Agent 4: Example/Tutorial Check
```
Compare: Code APIs vs examples in docs
Find: Examples using old APIs, deprecated patterns
```

### Phase 3: Staleness Report

Present findings in this format:

```markdown
## Documentation Freshness Report

**Scanned**: [X] docs, [Y] code files
**Documentation System**: MkDocs / Standard / Single-file

### Summary

| Status | Count | Action Needed |
|--------|-------|---------------|
| 🟢 Fresh | X | None |
| 🟡 Stale | X | Update recommended |
| 🔴 Critical | X | Must update (breaking inaccuracies) |
| ⚪ Skipped | X | Historical/conceptual (not code-synced) |

---

### 🔴 Critical Issues (Breaking Inaccuracies)

#### 1. `docs/api/users.md` — Wrong endpoint documented

**Doc says:**
```
POST /api/users/create
```

**Code actually has:**
```typescript
// src/routes/users.ts:45
router.post('/api/v2/users', createUser)
```

**Impact**: Users following docs will hit 404
**Proposed fix**: Update endpoint path, add v2 note

---

#### 2. `README.md` — Missing required env var

**Doc says:**
```
Required: DATABASE_URL, API_KEY
```

**Code requires:**
```typescript
// src/config.ts:12
const required = ['DATABASE_URL', 'API_KEY', 'JWT_SECRET']
```

**Impact**: App crashes without JWT_SECRET
**Proposed fix**: Add JWT_SECRET to required list

---

### 🟡 Stale (Should Update)

#### 3. `docs/setup.md` — Outdated install command

**Doc says:** `npm install`
**Code uses:** `pnpm install` (per package.json)
**Proposed fix**: Update to pnpm

#### 4. `docs/architecture.md` — Missing new module

**Doc doesn't mention:** `src/services/notifications/`
**Added in code:** 2 weeks ago (15 files)
**Proposed fix**: Add notifications module section

---

### 🟢 Fresh (No Changes Needed)

- `docs/decisions/001-database-choice.md` — ADR, historical
- `docs/concepts/authentication.md` — Conceptual, still accurate
- `docs/api/health.md` — Matches code

---

## Proposed Changes Preview

| # | File | Change Type | Lines Affected |
|---|------|-------------|----------------|
| 1 | docs/api/users.md | Update endpoint | ~5 lines |
| 2 | README.md | Add env var | ~2 lines |
| 3 | docs/setup.md | Update command | ~1 line |
| 4 | docs/architecture.md | Add section | ~20 lines |

**Total**: 4 files, ~28 lines

---

**Apply these changes?**

Options:
- `all` — Apply all proposed changes
- `critical` — Apply only critical fixes (1, 2)
- `1,2,3` — Apply specific changes by number
- `none` — Exit without changes
- `show 1` — Preview exact diff for change #1
```

### Phase 4: Apply Updates (with approval)

For each approved change:

1. **Read the current doc file**
2. **Make surgical edits** — only change what's stale
3. **Preserve**:
   - Human-written explanations
   - Warnings and caveats
   - Historical context
   - Formatting and style
4. **Show diff before saving**
5. **Save with backup** (optional)

### Phase 5: Summary

```markdown
## Refresh Complete

**Updated**: X files
**Skipped**: Y files (user chose not to update)
**Errors**: Z files (couldn't update)

### Changes Applied

| File | Changes |
|------|---------|
| docs/api/users.md | Updated endpoint /api/users/create → /api/v2/users |
| README.md | Added JWT_SECRET to required env vars |

### Recommended Follow-up

- [ ] Review `docs/architecture.md` — new module needs more detail
- [ ] Run docs build to verify no broken links
- [ ] Commit changes: `git add docs/ && git commit -m "docs: refresh to match current code"`
```

## Edge Cases

### No Documentation Found
```
No documentation detected in this project.

Would you like to:
1. Generate initial docs with /easydev:onboard
2. Specify custom docs path: /easydev:docs-refresh ./my-docs
```

### Documentation More Recent Than Code
```
Note: docs/api/users.md was modified MORE recently than src/routes/users.ts

This might mean:
- Docs were updated manually (verify accuracy)
- Code needs to catch up to spec (use /easydev:design-sync)

Skipping this file. Use --force to include anyway.
```

### Large Codebase
```
Large codebase detected (500+ files).

Options:
1. Focused scan: /easydev:docs-refresh --scope critical
2. Specific area: /easydev:docs-refresh docs/api src/routes
3. Full scan (slower): /easydev:docs-refresh --scope all
```

## MkDocs-Specific Behavior

When MkDocs detected:

1. **Respect nav structure** — Don't create orphan files
2. **Check i18n** — Flag if primary lang updated but translations stale
3. **Suggest nav entry** — If new doc created, show where to add in mkdocs.yml
4. **Validate links** — Check internal links still work after updates
