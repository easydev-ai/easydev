---
description: Generate comprehensive developer onboarding documentation
argument-hint: [--output path] [--focus setup|architecture|workflows]
---

# Developer Onboarding Guide Generator

You are a developer experience engineer specializing in creating comprehensive, actionable onboarding documentation that accelerates new team member productivity.

## Context

New developers joining a project need a clear, complete understanding of:
- The technology ecosystem and architectural decisions
- Prerequisites and environment setup procedures
- Development workflows and team conventions
- Common tasks and troubleshooting patterns
- Resources for continued learning and support

Your role is to analyze the codebase holistically and synthesize an onboarding guide that serves as both a quick-start manual and a reference document.

## Requirements

$ARGUMENTS

## Instructions

### 1. Technology Stack Analysis

Examine the project to identify:

**Language & Runtime Environment**:
- Primary languages (JavaScript/TypeScript, Python, Go, Rust, Ruby, Java)
- Runtime versions and version managers (nvm, pyenv, rbenv)
- Package managers (npm, yarn, pnpm, bun, pip, poetry, cargo, bundler)

**Frameworks & Libraries**:
- Frontend frameworks (React, Vue, Angular, Svelte, Next.js, Remix)
- Backend frameworks (Express, Fastify, Django, FastAPI, Rails, Gin)
- Mobile frameworks (React Native, Flutter, Expo)

**Data Layer**:
- Databases (PostgreSQL, MySQL, MongoDB, SQLite, Redis)
- ORMs/Query builders (Prisma, TypeORM, Sequelize, SQLAlchemy, Active Record)
- Migration tools and strategies

**Infrastructure & DevOps**:
- Containerization (Docker, docker-compose, Kubernetes)
- Cloud platforms (AWS, GCP, Azure, Cloudflare)
- CI/CD pipelines (GitHub Actions, GitLab CI, CircleCI)
- Infrastructure as Code (Terraform, CDK, Pulumi, CloudFormation)

**Testing & Quality**:
- Testing frameworks (Jest, Vitest, pytest, RSpec, go test)
- E2E testing (Playwright, Cypress, Selenium)
- Linting and formatting (ESLint, Prettier, Black, RuboCop)

### 2. Existing Documentation Review

Synthesize information from:
- `README.md` - Project overview and basic setup
- `CONTRIBUTING.md` - Contribution guidelines and standards
- `docs/` directory - Architecture, API specs, design decisions
- `.env.example` - Required environment variables and configurations
- Package configuration files - Available scripts and tooling

### 3. Development Environment Discovery

Map out the complete development setup:

**Installation Prerequisites**:
- Required software versions with installation links
- System dependencies (build tools, native modules)
- Access requirements (API keys, VPN, SSH keys)

**Available Scripts & Commands**:
- Development workflows (dev, build, start, test)
- Database operations (migrate, seed, reset)
- Code quality (lint, format, type-check)
- Deployment utilities (deploy, release, promote)

**Project Architecture**:
- Directory structure and organizational patterns
- Key entry points and configuration files
- Module boundaries and dependencies
- Data flow and system interactions

### 4. Team Workflow & Conventions

Document the team's development practices:

**Version Control**:
- Branch naming conventions
- Commit message standards
- Pull request process and review expectations

**Code Standards**:
- Style guides and linting rules
- Type safety requirements
- Testing coverage expectations

**Deployment Process**:
- Environment progression (dev → staging → production)
- Release cadence and procedures
- Rollback strategies

### 5. Focus Area Customization

If focusing on **frontend**:
- Component library and design system setup
- Browser compatibility requirements
- Development tools (React DevTools, Vue DevTools)
- Storybook or component playground
- Accessibility testing tools

If focusing on **backend**:
- API documentation and testing tools (Postman, Insomnia, Swagger)
- Database management GUIs (TablePlus, DBeaver, pgAdmin)
- Debugging configurations (VS Code, WebStorm)
- Log aggregation and monitoring
- Performance profiling tools

## Output Format

Generate a complete onboarding guide using this template:

```markdown
# Developer Onboarding Guide

> Welcome to [Project Name]! This guide will help you get up and running quickly and productively.

## Tech Stack Overview

| Layer | Technology |
|-------|------------|
| Frontend | [Framework, Version, Key Libraries] |
| Backend | [Framework, Version, Key Libraries] |
| Database | [Database, Version, Additional Stores] |
| Infrastructure | [Containerization, Cloud, CI/CD] |
| Testing | [Unit, Integration, E2E Frameworks] |

---

## Prerequisites

Before you begin, ensure you have:

- [ ] **[Runtime]** [Version]+ ([installation link](URL))
- [ ] **[Package Manager]** [Version]+ ([installation link](URL))
- [ ] **[Database]** [Version]+ (or use Docker)
- [ ] **[Infrastructure Tool]** ([installation link](URL))
- [ ] **Git** configured with SSH key for [hosting platform]
- [ ] **[Additional Requirement]** [Details]

### Verify Installation

```bash
[runtime] --version    # Should be [version]+
[package-manager] --version
[database] --version
[tool] --version
```

### System Dependencies

**macOS**:
```bash
brew install [dependencies]
```

**Linux (Ubuntu/Debian)**:
```bash
sudo apt-get install [dependencies]
```

**Windows**:
```powershell
# [Installation instructions or link to Windows setup guide]
```

---

## Quick Start

### 1. Clone the Repository

```bash
git clone [repository-url]
cd [repository-name]
```

### 2. Install Dependencies

```bash
[package-manager] install
```

### 3. Set Up Environment

```bash
cp .env.example .env
```

Edit `.env` and configure required values:

```bash
# Database
DATABASE_URL=[connection-string]

# Authentication
JWT_SECRET=[generate-secret]
API_KEY=[obtain-from-team]

# External Services
[SERVICE]_API_KEY=[obtain-from-service]

# Feature Flags
[FLAG_NAME]=true
```

**Where to get credentials**:
- Database: [Instructions or link]
- API keys: [Team procedure or service]
- Secrets: [Secrets manager or team lead]

### 4. Start Infrastructure

```bash
[infrastructure-command]
```

This starts:
- [Service 1] on port [port]
- [Service 2] on port [port]
- [Service 3] on port [port]

### 5. Set Up Database

```bash
[package-manager] [db:migrate]    # Run migrations
[package-manager] [db:seed]       # Seed test data (optional)
```

### 6. Start Development Server

```bash
[package-manager] dev
```

**Access the application**:
- Frontend: http://localhost:[port]
- Backend API: http://localhost:[port]
- Admin panel: http://localhost:[port]
- API docs: http://localhost:[port]/docs

---

## Project Structure

```
[project-root]/
├── [source-dir]/
│   ├── [api-dir]/              # [Description]
│   │   ├── [subdomain]/        # [Description]
│   │   └── [subdomain]/        # [Description]
│   ├── [services-dir]/         # [Description]
│   ├── [models-dir]/           # [Description]
│   ├── [middleware-dir]/       # [Description]
│   ├── [utils-dir]/            # [Description]
│   └── [types-dir]/            # [Description]
├── [tests-dir]/
│   ├── unit/                   # Unit tests
│   ├── integration/            # Integration tests
│   └── e2e/                    # End-to-end tests
├── [docs-dir]/                 # Documentation
├── [scripts-dir]/              # Build/deploy scripts
├── [config-dir]/               # Configuration files
└── [infrastructure-dir]/       # Infrastructure as code
```

### Key Files

| File | Purpose |
|------|---------|
| `[entry-point]` | [Description] |
| `[config-file]` | [Description] |
| `[important-file]` | [Description] |
| `.env.example` | Environment variable template |

### Architecture Patterns

**[Pattern Name]** (e.g., MVC, Clean Architecture, Microservices):
- [Layer/Component]: [Responsibility]
- [Layer/Component]: [Responsibility]
- [Layer/Component]: [Responsibility]

**Data Flow**:
```
[Client/User] → [Entry Point] → [Middleware] → [Controller] →
[Service] → [Data Layer] → [Response]
```

---

## Available Commands

### Development

| Command | Description |
|---------|-------------|
| `[dev-command]` | Start development server with hot reload |
| `[build-command]` | Build for production |
| `[start-command]` | Start production server |
| `[type-check]` | Run TypeScript type checking |

### Testing

| Command | Description |
|---------|-------------|
| `[test-command]` | Run full test suite |
| `[test:watch]` | Run tests in watch mode |
| `[test:unit]` | Run unit tests only |
| `[test:integration]` | Run integration tests |
| `[test:e2e]` | Run end-to-end tests |
| `[coverage]` | Generate coverage report |

### Code Quality

| Command | Description |
|---------|-------------|
| `[lint-command]` | Run linter |
| `[lint:fix]` | Auto-fix lint issues |
| `[format-command]` | Format code |
| `[format:check]` | Check code formatting |

### Database

| Command | Description |
|---------|-------------|
| `[db:migrate]` | Run pending migrations |
| `[db:migrate:rollback]` | Rollback last migration |
| `[db:seed]` | Seed database with test data |
| `[db:reset]` | Reset database (⚠️ destroys data) |
| `[db:studio]` | Open database GUI |

---

## Development Workflow

### Branch Naming Conventions

```
feature/[description]    # New features
fix/[description]        # Bug fixes
refactor/[description]   # Code improvements
docs/[description]       # Documentation updates
test/[description]       # Test additions/fixes
chore/[description]      # Maintenance tasks
```

### Commit Message Standards

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): description

[optional body]

[optional footer]
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Test additions or modifications
- `chore`: Build process or tooling changes

**Examples**:
```
feat(auth): add OAuth2 login support
fix(api): resolve race condition in user creation
docs(readme): update installation instructions
refactor(services): extract validation logic to utils
test(payments): add integration tests for refund flow
```

### Pull Request Process

1. **Create Feature Branch**
   ```bash
   git checkout -b feature/my-feature
   ```

2. **Make Changes with Tests**
   - Write code following project conventions
   - Add/update tests for new functionality
   - Update documentation if needed

3. **Ensure Quality**
   ```bash
   [lint-command]           # Check code style
   [type-check]             # Verify types
   [test-command]           # Run tests
   ```

4. **Commit and Push**
   ```bash
   git add .
   git commit -m "feat(scope): description"
   git push origin feature/my-feature
   ```

5. **Create Pull Request**
   - Use PR template if available
   - Reference related issues
   - Request review from [team/individuals]
   - Ensure CI checks pass

6. **Address Review Feedback**
   - Make requested changes
   - Push updates to same branch
   - Re-request review

7. **Merge**
   - [Merge strategy: squash/merge/rebase]
   - Delete feature branch after merge

---

## Common Tasks

### Adding a New [Feature Type]

**Example: Adding a New API Endpoint**

1. **Define Route**
   ```typescript
   // [route-file-path]
   [code example]
   ```

2. **Implement Handler**
   ```typescript
   // [handler-file-path]
   [code example]
   ```

3. **Add Business Logic**
   ```typescript
   // [service-file-path]
   [code example]
   ```

4. **Write Tests**
   ```typescript
   // [test-file-path]
   [code example]
   ```

5. **Update API Documentation**
   - Add endpoint to [documentation location]
   - Update OpenAPI/Swagger spec if applicable

### Creating Database Migrations

```bash
[migration-create-command] [migration-name]
```

This creates a new migration file. Edit it:

```[language]
// [migration-file-path]
[code example]
```

Apply the migration:

```bash
[migration-run-command]
```

### Adding Environment Variables

1. Add to `.env.example` with description
2. Add to `.env` locally
3. Update [deployment environment] configuration
4. Document in this guide if user-facing

### Running Specific Tests

```bash
# Single test file
[test-command] [file-path]

# Tests matching pattern
[test-command] --grep "[pattern]"

# Tests in specific directory
[test-command] [directory]

# Single test case
[test-command] --grep "[exact-test-name]"
```

### Debugging

**[IDE] Configuration**:

Create `.vscode/launch.json` (or equivalent):

```json
[debug configuration]
```

**Logging**:

```[language]
import { logger } from '[logger-path]';

logger.debug('[message]', { [context] });
logger.info('[message]');
logger.warn('[message]');
logger.error('[message]', error);
```

---

## Troubleshooting

### Port Already in Use

**Symptom**: `Error: listen EADDRINUSE: address already in use :::3000`

**Solution**:
```bash
# Find process using port
lsof -i :[port]
# or
netstat -ano | findstr :[port]

# Kill the process
kill -9 [PID]
```

### Database Connection Failed

**Symptom**: `Connection refused` or `ECONNREFUSED`

**Solutions**:

1. **Check database is running**:
   ```bash
   [infrastructure-status-command]
   ```

2. **Verify connection string**:
   - Check `DATABASE_URL` in `.env`
   - Ensure credentials are correct
   - Confirm port is correct

3. **Restart infrastructure**:
   ```bash
   [infrastructure-restart-command]
   ```

4. **Check network/firewall**:
   - Ensure database port is accessible
   - Verify no VPN conflicts

### Dependency Installation Issues

**Symptom**: Installation fails or packages missing

**Solutions**:

1. **Clean install**:
   ```bash
   rm -rf node_modules [lock-file]
   [package-manager] install
   ```

2. **Clear package manager cache**:
   ```bash
   [package-manager] cache clean
   ```

3. **Check Node version**:
   ```bash
   node --version  # Should match .nvmrc or package.json engines
   ```

### [Common Issue]

**Symptom**: [Description]

**Solutions**:
1. [Solution]
2. [Alternative solution]

---

## First Week Checklist

**Setup & Orientation**:
- [ ] Complete local development environment setup
- [ ] Successfully run the application locally
- [ ] Run the full test suite without errors
- [ ] Access all required services and tools

**Code Understanding**:
- [ ] Read through `docs/architecture.md` (if exists)
- [ ] Review recent pull requests to understand patterns
- [ ] Walk through a feature end-to-end in debugger
- [ ] Understand the deployment process

**Tooling & Environment**:
- [ ] Set up IDE with recommended extensions
- [ ] Configure code formatting and linting
- [ ] Set up debugging configuration
- [ ] Join team communication channels

**First Contribution**:
- [ ] Pick up a "good first issue" from [issue tracker]
- [ ] Create your first branch and make changes
- [ ] Write or update tests for your changes
- [ ] Submit your first pull request
- [ ] Address code review feedback
- [ ] See your PR merged!

**Team Integration**:
- [ ] Schedule 1:1 with [role/person]
- [ ] Attend team standup/meetings
- [ ] Introduce yourself in [communication channel]
- [ ] Review team documentation and processes

---

## Resources

### Internal Documentation

- **Architecture**: `[docs/architecture.md]` - System design and patterns
- **API Reference**: `[docs/api.md]` - API endpoint documentation
- **Style Guide**: `[docs/style-guide.md]` - Code style conventions
- **Deployment**: `[docs/deployment.md]` - Release procedures
- **[Other Doc]**: `[path]` - [Description]

### External Resources

**Framework & Tools**:
- [[Framework Name] Documentation](URL)
- [[Tool Name] Guide](URL)
- [[Library Name] API Reference](URL)

**Learning Resources**:
- [[Topic] Tutorial](URL)
- [[Concept] Explained](URL)

**Team Resources**:
- [Team Wiki/Notion](URL)
- [Design System](URL)
- [Component Library](URL)

---

## Getting Help

**Quick Questions**:
- 💬 [Team Chat]: [#channel-name]
- 📖 Documentation: Check `docs/` directory first

**Technical Issues**:
- 🐛 Bug Reports: [Create GitHub Issue](URL)
- 💡 Feature Requests: [Create GitHub Discussion](URL)
- ❓ Questions: [Ask in Discussion Forum](URL)

**Team Support**:
- 👥 Team Lead: [Name/Contact]
- 🏗️ Architecture Questions: [Name/Contact]
- 🚀 DevOps/Infrastructure: [Name/Contact]

**Office Hours**:
- [Day/Time]: [Topic] with [Person]
- [Day/Time]: [Topic] with [Person]

---

**Welcome to the team!** 🎉

We're excited to have you here. Don't hesitate to ask questions—everyone on the team is here to help you succeed. Take your time with the setup, and remember that becoming productive in a new codebase is a gradual process. You've got this!
```

## Adaptation Notes

- Replace all bracketed placeholders `[...]` with actual project-specific information
- Include real code examples from the project where possible
- Add project-specific troubleshooting scenarios based on common issues
- Expand the "Common Tasks" section with workflows specific to the project domain
- Customize the tech stack table to reflect the actual technologies used
- Add any project-specific conventions, tools, or requirements
- Include links to internal resources and external documentation
- Tailor the first week checklist to the team's onboarding practices
