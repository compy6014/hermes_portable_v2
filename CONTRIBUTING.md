# CONTRIBUTING.md

# Contributing to PortableHermes

**Document Version:** 1.0

**Status:** Active

**Last Updated:** 2026-07-05

---

# Welcome

Thank you for your interest in contributing to PortableHermes.

PortableHermes aims to be a professional, maintainable, and extensible AI platform. Every contribution—whether code, documentation, testing, or design—helps improve the project.

This document defines the expected workflow and quality standards for all contributions.

---

# Guiding Principles

Contributors should prioritize:

* readability over cleverness
* maintainability over shortcuts
* simplicity over unnecessary complexity
* documentation alongside implementation
* testing as part of development

Every change should leave the project in a better state than before.

---

# Development Workflow

The recommended workflow is:

1. Synchronize with the latest `main` branch.
2. Create a feature branch.
3. Implement the change.
4. Update documentation if required.
5. Add or update tests.
6. Run the test suite.
7. Commit using the project's commit conventions.
8. Open a Pull Request.

---

# Branch Strategy

The repository uses a simplified Git workflow.

## Main Branch

`main`

* Always stable
* Always deployable
* Protected
* No direct commits

---

## Feature Branches

Naming convention:

```text
feature/<short-description>
```

Examples:

```text
feature/provider-ollama
feature/plugin-homeassistant
feature/runtime-manager
feature/gui-settings
```

---

## Bug Fix Branches

Naming convention:

```text
fix/<short-description>
```

Examples:

```text
fix/wsl-path-conversion
fix/logger-rotation
fix/plugin-loader
```

---

## Documentation Branches

Naming convention:

```text
docs/<short-description>
```

Examples:

```text
docs/update-roadmap
docs/testing-guide
```

---

## Experimental Work

Naming convention:

```text
experiment/<topic>
```

Experimental branches are not expected to be production ready.

---

# Commit Message Convention

PortableHermes follows the Conventional Commits specification.

Format:

```text
<type>: <short description>
```

Examples:

```text
feat: add provider abstraction
fix: correct WSL path conversion
docs: update architecture diagram
refactor: simplify plugin loader
test: add runtime integration tests
chore: update dependencies
```

---

## Supported Commit Types

| Type     | Purpose                                     |
| -------- | ------------------------------------------- |
| feat     | New functionality                           |
| fix      | Bug fix                                     |
| docs     | Documentation only                          |
| refactor | Code restructuring without behavior changes |
| test     | Tests                                       |
| style    | Formatting only                             |
| perf     | Performance improvements                    |
| build    | Build system changes                        |
| ci       | CI/CD changes                               |
| chore    | Maintenance tasks                           |

---

# Pull Request Guidelines

Each Pull Request should:

* solve one logical problem
* remain reasonably small
* include documentation updates when applicable
* include tests where appropriate
* avoid unrelated changes

Large changes should be split into multiple Pull Requests whenever practical.

---

# Pull Request Checklist

Before submitting:

* [ ] Project builds successfully
* [ ] Tests pass
* [ ] Documentation updated
* [ ] No unnecessary files included
* [ ] Coding standards followed
* [ ] Commit history cleaned up
* [ ] Self-review completed

---

# Code Style

PortableHermes follows the standards defined in `CODING_STANDARD.md`.

Highlights include:

* descriptive naming
* small functions
* modular architecture
* single responsibility
* clear comments where needed

Code should be understandable without requiring external explanation.

---

# Documentation Requirements

Documentation is considered part of the implementation.

Documentation updates are expected whenever:

* architecture changes
* configuration changes
* new plugins are added
* public interfaces change
* user workflows change

Documentation should not lag behind the codebase.

---

# Testing Requirements

New functionality should include appropriate tests.

At a minimum:

* unit tests for core logic
* integration tests for system interactions
* regression tests for bug fixes

Refer to `TESTING.md` for detailed testing expectations.

---

# Issue Reporting

Bug reports should include:

* PortableHermes version
* Operating System
* WSL version (if applicable)
* Python version
* AI provider
* Model used
* Steps to reproduce
* Expected behavior
* Actual behavior
* Relevant logs

Clear, reproducible reports are more valuable than lengthy descriptions.

---

# Feature Requests

Feature requests should explain:

* the problem being solved
* proposed solution
* possible alternatives
* expected benefits
* potential drawbacks

Architectural consistency is more important than feature quantity.

---

# Code Review

Every contribution should be reviewed for:

* correctness
* readability
* maintainability
* architecture alignment
* security implications
* documentation completeness
* test coverage

Feedback should focus on improving the project rather than criticizing contributors.

---

# Dependency Policy

New dependencies should be introduced only when they provide clear value.

Before adding a dependency, consider:

* maintenance activity
* licensing
* security history
* portability
* project size
* long-term support

Whenever practical, prefer the Python standard library over third-party packages.

---

# Backward Compatibility

Breaking changes should be avoided whenever possible.

If a breaking change is necessary:

* document it
* update migration guidance
* note it in `CHANGELOG.md`
* increment the appropriate version

---

# Security

Contributors should never commit:

* API keys
* passwords
* authentication tokens
* private certificates
* confidential user data

Configuration examples should use placeholder values.

---

# Plugin Development

Plugins should:

* implement the required interfaces
* remain self-contained
* avoid modifying global state
* include documentation
* include tests
* fail gracefully

A malfunctioning plugin must not compromise the stability of PortableHermes.

---

# AI Provider Contributions

New AI providers should:

* implement the common provider interface
* support capability discovery
* provide meaningful error messages
* integrate with the logging system
* include provider-specific tests

Provider-specific logic should remain isolated from the core framework.

---

# Documentation Contributions

Documentation should:

* use Markdown
* follow existing formatting
* remain concise and accurate
* avoid duplication where possible
* be updated alongside implementation

Examples and diagrams are encouraged where they improve understanding.

---

# Versioning

PortableHermes follows Semantic Versioning.

```text
MAJOR.MINOR.PATCH
```

Examples:

* 0.1.0
* 0.4.2
* 1.0.0

Version numbers should reflect the impact of changes.

---

# Release Process

A release typically includes:

1. Code freeze
2. Final testing
3. Documentation review
4. Version update
5. Changelog update
6. Tag creation
7. Release publication

Releases should always be reproducible from a tagged commit.

---

# Community Standards

Contributors are expected to:

* communicate respectfully
* provide constructive feedback
* assume good intentions
* welcome differing viewpoints
* focus discussions on technical merit

Professional collaboration benefits everyone.

---

# Long-Term Vision

PortableHermes is designed as a long-lived engineering project.

Contributions should favor solutions that remain understandable, maintainable, and extensible over many years.

When in doubt, choose the solution that best aligns with the project's architectural principles and documented standards.

Thank you for helping build PortableHermes.
