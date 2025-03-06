# Nhanced.Tech GitHub Organization

## Table of Contents
1. [Introduction](#introduction)
2. [Organization Structure](#organization-structure)
3. [Repository Naming](#repository-naming)
4. [Repository Structure](#repository-structure)
5. [Branch Strategy](#branch-strategy)
6. [Commit Guidelines](#commit-guidelines)
7. [Pull Request Process](#pull-request-process)
8. [Code Review](#code-review)
9. [Issue Management](#issue-management)
10. [Project Management](#project-management)
11. [CI/CD Integration](#cicd-integration)
12. [Documentation](#documentation)
13. [Security](#security)
14. [Onboarding New Team Members](#onboarding-new-team-members)

## Introduction

This document outlines the GitHub organization guidelines for Nhanced.Tech. Our goal is to establish consistent practices across all our repositories to improve collaboration, code quality, and development efficiency.

## Organization Structure

The Nhanced.Tech GitHub organization is structured as follows:

- **Core Product Repositories**: Main products and services
- **Library Repositories**: Shared code libraries and components
- **Tool Repositories**: Development, testing, and deployment tools
- **Documentation Repositories**: Company-wide and product documentation
- **Archive**: Deprecated or historical projects

Each repository should belong to at least one team with appropriate access rights.

## Repository Naming

Follow these naming conventions for repositories:

- Use lowercase letters and hyphens (e.g., `device-firmware`, `cloud-api`)
- For product repositories: `product-name` or `product-name-component`
- For libraries: `lib-purpose` (e.g., `lib-networking`, `lib-analytics`)
- For tools: `tool-purpose` (e.g., `tool-deployment`, `tool-testing`)
- For documentation: `docs-subject` (e.g., `docs-api`, `docs-architecture`)

## Repository Structure

### For Embedded C Projects

```
/project-root
  README.md
  LICENSE
  CONTRIBUTING.md
  CHANGELOG.md
  .gitignore
  .github/              # GitHub specific files (actions, templates)
    /workflows/         # GitHub Actions workflows
    /ISSUE_TEMPLATE/    # Issue templates
    /PULL_REQUEST_TEMPLATE.md
  /inc/                 # Header files
  /src/                 # Source files
  /drivers/             # Hardware-specific drivers
  /middlewares/         # Middleware components
  /utils/               # Utility functions
  /tests/               # Test code
  /docs/                # Documentation
  /build/               # Build outputs (gitignored)
  CMakeLists.txt        # Or other build system files
```

### For Python Projects

```
/project-root
  README.md
  LICENSE
  CONTRIBUTING.md
  CHANGELOG.md
  .gitignore
  .github/              # GitHub specific files (actions, templates)
  /project_name/        # Main package
    /__init__.py        # Package initializer
    /core/              # Core functionality
    /utils/             # Utility functions
    /models/            # Data models
    /api/               # API endpoints
  /tests/               # Test code
  /docs/                # Documentation
  /scripts/             # Standalone scripts
  /examples/            # Example usage
  requirements.txt      # Dependencies
  setup.py              # Package setup
  pyproject.toml        # Modern project configuration
```

### For Web/Frontend Projects

```
/project-root
  README.md
  LICENSE
  CONTRIBUTING.md
  CHANGELOG.md
  .gitignore
  .github/              # GitHub specific files
  /src/                 # Source code
  /public/              # Static assets
  /docs/                # Documentation
  /tests/               # Test code
  package.json          # Dependencies and scripts
  tsconfig.json         # TypeScript configuration (if applicable)
```

## Branch Strategy

We follow a modified GitFlow workflow:

- `main` - Production-ready code. Protected branch.
- `develop` - Integration branch for features. Protected branch.
- `feature/*` - New features (branched from and merged to `develop`)
- `bugfix/*` - Bug fixes (branched from and merged to `develop`)
- `release/*` - Release preparation (branched from `develop`, merged to `main` and back to `develop`)
- `hotfix/*` - Emergency production fixes (branched from `main`, merged to `main` and `develop`)

### Branch Naming

- Feature branches: `feature/short-description` or `feature/ISSUE-123-short-description`
- Bugfix branches: `bugfix/short-description` or `bugfix/ISSUE-123-short-description`
- Release branches: `release/vX.Y.Z`
- Hotfix branches: `hotfix/vX.Y.Z` or `hotfix/critical-issue-description`

## Commit Guidelines

Follow these guidelines for commit messages:

- Use the present tense ("Add feature" not "Added feature")
- Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
- Limit the first line to 72 characters or less
- Reference issues and pull requests after the first line
- Consider using a structured format:
  ```
  <type>(<scope>): <subject>
  
  <body>
  
  <footer>
  ```
  Where `<type>` is one of:
  - feat: A new feature
  - fix: A bug fix
  - docs: Documentation only changes
  - style: Changes that do not affect the meaning of the code
  - refactor: A code change that neither fixes a bug nor adds a feature
  - perf: A code change that improves performance
  - test: Adding missing or correcting existing tests
  - chore: Changes to the build process or auxiliary tools

## Pull Request Process

1. Ensure your branch is up to date with the base branch
2. Update documentation if needed
3. Add or update tests as necessary
4. Fill out the pull request template completely
5. Request review from appropriate team members
6. Address all review comments
7. Squash commits if necessary before merging
8. Delete the branch after merging

### Pull Request Template

Every repository should include a PR template with the following sections:
- Description of changes
- Related issue(s)
- Type of change (bugfix, new feature, etc.)
- How has this been tested?
- Checklist (tests, documentation, etc.)

## Code Review

Guidelines for effective code reviews:

- Review code within 24-48 business hours
- Be respectful and constructive
- Comment on specific lines for clarity
- Differentiate between required changes and suggestions
- Approve PR once all required changes are addressed
- For complex changes, consider pair programming or real-time review sessions

## Issue Management

Use GitHub Issues for tracking bugs, enhancements, and tasks:

- Use issue templates for bugs, features, and documentation
- Label issues appropriately (priority, type, status)
- Assign issues to responsible individuals
- Link PRs to issues they address
- Use milestones to organize issues into releases

### Issue Labels

Standardized labels across repositories:
- `bug`: Something isn't working
- `enhancement`: New feature or request
- `documentation`: Documentation improvements
- `question`: Further information is needed
- `priority:high/medium/low`: Issue priority
- `good first issue`: Good for newcomers
- `help wanted`: Extra attention is needed

## Project Management

Use GitHub Projects for tracking work:

- Create project boards for major initiatives
- Structure columns (e.g., To Do, In Progress, Review, Done)
- Link issues and PRs to project boards
- Use automated workflows when possible

## CI/CD Integration

Every repository should include GitHub Actions workflows for:

- Continuous Integration (build, lint, test)
- Code quality checks
- Dependency scanning
- Deployment (for appropriate repositories)

Example workflow structure:
```
.github/workflows/
  ci.yml          # Build and test on PRs and pushes
  quality.yml     # Code quality checks (linting, formatting)
  security.yml    # Dependency and security scanning
  deploy-dev.yml  # Deploy to development environment
  deploy-prod.yml # Deploy to production environment
```

## Documentation

Documentation standards:

- Every repository must include a README.md with:
  - Project description and purpose
  - Prerequisites and dependencies
  - Installation/setup instructions
  - Basic usage examples
  - Development guide
  - Link to more comprehensive documentation

- Maintain comprehensive documentation in:
  - Code comments (following language-specific standards)
  - /docs directory (architecture, API docs, etc.)
  - Wiki (for user guides and evolving documentation)

## Security

Security practices:

- No secrets or credentials in repositories
- Use GitHub Secrets for sensitive information
- Regular dependency updates
- Security scanning in CI pipeline
- Protected branches for production code
- Required reviews before merging to protected branches

## Onboarding New Team Members

For new team members:

1. Add to the Nhanced.Tech GitHub organization with appropriate team membership
2. Provide read access to all repositories initially
3. Grant write access to specific repositories as needed
4. Assign a mentor for initial PRs
5. Start with `good first issue` labeled issues

---

This document is maintained by the Nhanced.Tech Engineering Team and should be reviewed quarterly for updates.

Last updated: [Date]
