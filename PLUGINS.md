# Official Claude Code Plugins Guide

> **For InsightureAI team members** — How to install and use official Anthropic plugins alongside our custom commands.

---

## Quick Start

```bash
# Step 1: Add the official Anthropic marketplace (run once)
/plugin marketplace add anthropics/claude-code

# Step 2: Install plugins via interactive UI
/plugin
# → Select "Install Plugins" → Select all desired plugins → Enter

# Step 3: Restart Claude Code
/exit
claude
```

---

## Recommended Plugins for Our Team

| Priority | Plugin | Why We Recommend |
|----------|--------|------------------|
| ⭐ Must Have | `feature-dev` | 7-phase structured development — prevents cowboy coding |
| ⭐ Must Have | `code-review` | Automated PR review with confidence scoring |
| ⭐ Must Have | `security-guidance` | Catches OWASP issues before commit |
| ✓ Recommended | `commit-commands` | `/commit`, `/commit-push-pr` workflow |
| ✓ Recommended | `hookify` | Create custom safety hooks easily |
| ○ Optional | `frontend-design` | Better UI generation (auto-activates) |
| ○ Optional | `pr-review-toolkit` | 6 specialized PR review agents |

---

## All 13 Official Plugins

All plugins are developed by **Anthropic engineers** and maintained in `anthropics/claude-code`.

---

### Development Workflow

#### 1. feature-dev ⭐
**Structured 7-phase feature development**

```bash
/feature-dev Add OAuth authentication with Google
```

**The 7 Phases:**

| Phase | Purpose | What Happens |
|-------|---------|--------------|
| 1. Discovery | Understand requirements | Clarifies feature request, asks constraints |
| 2. Codebase Exploration | Learn existing patterns | Launches 2-3 `code-explorer` agents in parallel |
| 3. Clarifying Questions | Resolve ambiguities | Identifies edge cases, waits for your answers |
| 4. Architecture Design | Design approaches | Launches 2-3 `code-architect` agents with different philosophies |
| 5. Implementation | Build it | Waits for approval, then implements |
| 6. Quality Review | Ensure quality | Launches 3 `code-reviewer` agents |
| 7. Summary | Document work | Lists files modified, decisions made, next steps |

**Agents:** `code-explorer`, `code-architect`, `code-reviewer`

**Manual agent invocation:**
```bash
"Launch code-explorer to trace how authentication works"
"Launch code-architect to design the caching layer"
"Launch code-reviewer to check my recent changes"
```

---

#### 2. code-review ⭐
**Automated PR review with confidence scoring**

```bash
/code-review
```

**How it works:**
- Launches 5 parallel review agents
- Scores each issue 0-100 for confidence
- Only posts issues ≥80 confidence (filters false positives)
- Checks CLAUDE.md compliance, bugs, historical context

**Review agents:**
1. CLAUDE.md compliance audit (x2 for redundancy)
2. Bug detection (changed code only)
3. Historical context analysis (git blame)

**Confidence scoring:**
| Score | Meaning |
|-------|---------|
| 0 | Not confident, false positive |
| 25 | Somewhat confident |
| 50 | Moderately confident |
| 75 | Highly confident |
| 100 | Absolutely certain |

---

#### 3. commit-commands
**Git workflow automation**

| Command | What it does |
|---------|--------------|
| `/commit` | Analyze changes, match repo commit style, create commit |
| `/commit-push-pr` | Branch + commit + push + PR in one command |
| `/clean_gone` | Remove local branches deleted from remote |

**Example workflow:**
```bash
# Develop feature
/commit              # First commit
# More changes
/commit              # Second commit
/commit-push-pr      # Create PR when ready
```

---

#### 4. pr-review-toolkit
**6 specialized PR review agents**

```bash
/pr-review-toolkit:review-pr [aspects]
```

**Aspects:** `comments`, `tests`, `errors`, `types`, `code`, `simplify`, `all`

**Agents:**
| Agent | Focus |
|-------|-------|
| `comment-analyzer` | PR comment analysis |
| `pr-test-analyzer` | Test coverage and quality |
| `silent-failure-hunter` | Swallowed errors, missing error handling |
| `type-design-analyzer` | TypeScript type design |
| `code-reviewer` | General code quality |
| `code-simplifier` | Complexity reduction |

---

### Security & Safety

#### 5. security-guidance ⭐
**Pre-tool hook that warns about security patterns**

**No command needed** — runs automatically on file edits.

**Detects 9+ patterns:**
- Command injection
- XSS vulnerabilities
- `eval()` / `exec()` usage
- Dangerous HTML injection
- Pickle deserialization
- `os.system()` calls
- Hardcoded credentials
- And more...

---

#### 6. hookify
**Create custom hooks via natural language**

```bash
# From explicit instruction
/hookify Don't use console.log in TypeScript files
/hookify Warn me when using rm -rf

# Analyze conversation for patterns to hook
/hookify
```

**Other commands:**
| Command | Purpose |
|---------|---------|
| `/hookify:list` | List all active rules |
| `/hookify:configure` | Enable/disable rules |
| `/hookify:help` | Get help |

**Example rule created:**
```markdown
---
name: block-dangerous-rm
enabled: true
event: bash
pattern: rm\s+-rf
action: block
---

⚠️ **Dangerous rm command detected!**
This command could delete important files.
```

---

### Frontend

#### 7. frontend-design
**Distinctive, non-generic UI generation**

**Auto-activates** when doing frontend work. No command needed.

**Emphasizes:**
- Bold aesthetic choices (not template-like)
- Distinctive typography and color palettes
- High-impact animations
- Production-ready code

**Just ask:**
```
"Create a dashboard for a music streaming app"
"Build a landing page for an AI startup"
```

---

### Plugin & Agent Development

#### 8. plugin-dev
**Toolkit for creating your own Claude Code plugins**

```bash
/plugin-dev:create-plugin
```

**8-phase guided workflow** for creating plugins, with agents:
- `agent-creator`
- `plugin-validator`
- `skill-reviewer`

---

#### 9. agent-sdk-dev
**Claude Agent SDK development kit**

```bash
/new-sdk-app
```

**For:** Building custom AI agents with the Claude Agent SDK.

**Agents:**
- `agent-sdk-verifier-py` — Validate Python SDK apps
- `agent-sdk-verifier-ts` — Validate TypeScript SDK apps

---

### Specialized

#### 10. claude-opus-4-5-migration
**Migrate prompts/code to Opus 4.5**

One-time migration helper for updating:
- Model strings
- Beta headers
- Prompt adjustments

---

#### 11. ralph-wiggum
**Autonomous iteration loops**

```bash
/ralph-loop "Build REST API with tests" --completion-promise "COMPLETE" --max-iterations 50
```

**How it works:**
1. Claude works on task
2. Tries to exit
3. Stop hook blocks exit
4. Same prompt fed back
5. Repeat until completion promise found or max iterations

**Commands:**
| Command | Purpose |
|---------|---------|
| `/ralph-loop "<prompt>" --max-iterations N --completion-promise "TEXT"` | Start loop |
| `/cancel-ralph` | Cancel active loop |

**⚠️ Always use `--max-iterations`** as a safety mechanism.

**Good for:**
- Well-defined tasks with clear success criteria
- Tasks requiring iteration (getting tests to pass)
- Greenfield projects

**Not good for:**
- Tasks requiring human judgment
- Unclear success criteria
- Production debugging

---

### Learning Modes

#### 12. explanatory-output-style
**Educational insights about implementation choices**

SessionStart hook that explains *why* code choices are made. Mimics deprecated "Explanatory" output style.

---

#### 13. learning-output-style
**Interactive learning mode**

SessionStart hook that asks you to write code (5-10 lines) at decision points. For active learning.

---

## Plugin + Custom Command Synergy

Our custom commands complement these official plugins:

| Our Command | Plugin Complement | How They Work Together |
|-------------|-------------------|------------------------|
| `/review` | `code-review` | Our 4-perspective review + their automated PR review |
| `/pr-enhance` | `commit-commands` | Our PR description + their `/commit-push-pr` |
| `/research-evaluate` | `feature-dev` | Our research + their structured implementation |
| `/design-sync` | `feature-dev` | Our spec compliance + their architecture design |
| `/tech-debt` | `code-review` | Our debt identification + their issue detection |

---

## Potential Conflicts

| Combination | Issue | Solution |
|-------------|-------|----------|
| `explanatory-output-style` + `learning-output-style` | Both inject SessionStart hooks | Enable only one |
| `code-review` + `pr-review-toolkit` | Overlapping PR review | Use one per PR |
| `ralph-wiggum` | Stop hook intercepts exits | Always use `--max-iterations` |
| `security-guidance` | May slow edits slightly | Worth it for safety |

---

## Installation Commands

### Option 1: Interactive UI (Recommended)

```bash
/plugin
```
Then select "Install Plugins" → Select desired plugins → Enter.

### Option 2: Individual Commands

Run each command one at a time in Claude Code:

```bash
/plugin install agent-sdk-dev@anthropics-claude-code
/plugin install claude-opus-4-5-migration@anthropics-claude-code
/plugin install code-review@anthropics-claude-code
/plugin install commit-commands@anthropics-claude-code
/plugin install explanatory-output-style@anthropics-claude-code
/plugin install feature-dev@anthropics-claude-code
/plugin install frontend-design@anthropics-claude-code
/plugin install hookify@anthropics-claude-code
/plugin install learning-output-style@anthropics-claude-code
/plugin install plugin-dev@anthropics-claude-code
/plugin install pr-review-toolkit@anthropics-claude-code
/plugin install ralph-wiggum@anthropics-claude-code
/plugin install security-guidance@anthropics-claude-code
```

### Option 3: Recommended Only

```bash
/plugin install feature-dev@anthropics-claude-code
/plugin install code-review@anthropics-claude-code
/plugin install security-guidance@anthropics-claude-code
/plugin install commit-commands@anthropics-claude-code
/plugin install hookify@anthropics-claude-code
```

### After Installation

**Restart Claude Code:**
```bash
/exit
claude
```

**Verify installation:**
```bash
/plugin
# → Select "Manage Plugins" to see installed plugins
```

---

## Resources

- [Official Plugins Repo](https://github.com/anthropics/claude-code/tree/main/plugins)
- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Plugin System Docs](https://docs.anthropic.com/en/docs/claude-code/plugins)
- [Frontend Aesthetics Cookbook](https://github.com/anthropics/claude-cookbooks/blob/main/coding/prompting_for_frontend_aesthetics.ipynb)

---

## Changelog

| Date | Change |
|------|--------|
| 2025-12-15 | Initial documentation of all 13 official Anthropic plugins |
