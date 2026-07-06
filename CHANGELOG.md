# CHANGELOG.md

# Changelog

All notable changes to PortableHermes will be documented in this file.

This project follows the principles of **Keep a Changelog** and **Semantic Versioning**.

---

# Format

Versions are organized as follows:

```text
MAJOR.MINOR.PATCH
```

Example:

```
0.1.0
0.2.3
1.0.0
```

Release types:

* **MAJOR** — incompatible architectural or API changes
* **MINOR** — new features with backward compatibility
* **PATCH** — bug fixes, documentation updates, minor improvements

---

# Categories

Each release may contain one or more of the following sections:

* Added
* Changed
* Deprecated
* Removed
* Fixed
* Security

Only sections containing changes should be included.

---

# [Unreleased]

## Planned

### Core

* Provider abstraction layer
* Plugin framework
* Runtime manager
* Model discovery
* Session manager

### AI

* llama.cpp integration
* Ollama provider
* OpenAI provider
* Anthropic provider
* Multi-provider routing

### Plugins

* Git
* Docker
* Kubernetes
* Terraform
* Ansible
* Home Assistant

### Documentation

* User Guide
* Plugin SDK
* API Reference
* Administrator Guide

### Testing

* Automated unit tests
* Integration tests
* CI validation
* Performance benchmarks

---

# [0.0.3] - In Development

## Added

### Documentation

Complete project documentation including:

* README
* PROJECT_SPEC
* ARCHITECTURE
* REPOSITORY
* CODING_STANDARD
* DECISIONS
* ROADMAP
* TESTING
* CONTRIBUTING
* CHANGELOG

### Runtime

* Windows bootstrap improvements
* Linux runtime launcher
* WSL runtime bridge
* Runtime isolation model

### Environment

* Portable runtime directories
* Environment initialization
* Linux environment configuration
* Cross-platform path handling

### Logging

* Central logging library
* Log level configuration
* Runtime diagnostics

### Repository

* Standardized directory structure
* Modular library layout
* Initial project conventions

## Changed

* Improved project initialization sequence
* Improved runtime directory handling
* Improved WSL command execution
* Refined bootstrap architecture
* Simplified startup flow

## Fixed

* Multiple WSL path translation issues
* Runtime startup reliability
* Directory creation logic
* Bootstrap sequencing
* Configuration loading order

## Known Issues

* Windows editors may save shell scripts using incompatible encoding or line endings.
* WSL execution depends on Linux shell scripts being UTF-8 without BOM and using LF line endings.
* Runtime diagnostics continue to be improved during bootstrap stabilization.

---

# [0.0.2] - Initial Bootstrap

## Added

### Bootstrap

* Windows PowerShell bootstrap
* Configuration loader
* Logger
* Environment initialization

### Runtime

* Initial WSL support
* Runtime bridge
* Linux launcher

### Repository

* Initial directory structure
* Configuration files
* Runtime folders

### Development

* Early project documentation
* Logging infrastructure
* Configuration framework

## Changed

* Bootstrap architecture reorganized
* Library separation introduced

---

# [0.0.1] - Project Initialization

## Added

### Repository

* Initial repository creation
* Basic folder structure
* Git initialization

### Vision

* Portable AI assistant concept
* Windows-first architecture
* WSL execution strategy
* Python runtime design

---

# Release Checklist

Before publishing a release:

* [ ] All tests pass
* [ ] Documentation updated
* [ ] Version number updated
* [ ] Changelog updated
* [ ] Release notes prepared
* [ ] Git tag created
* [ ] Repository archived for release
* [ ] Portable package generated

---

# Versioning Policy

PortableHermes follows Semantic Versioning.

## Patch Releases

Examples:

```
0.2.1
0.2.2
0.2.3
```

Used for:

* Bug fixes
* Documentation updates
* Minor improvements
* Small refactoring
* Non-breaking maintenance

---

## Minor Releases

Examples:

```
0.3.0
0.4.0
0.5.0
```

Used for:

* New features
* New plugins
* New providers
* New commands
* Backward-compatible enhancements

---

## Major Releases

Examples:

```
1.0.0
2.0.0
```

Used for:

* Architectural redesign
* Breaking API changes
* Large framework evolution
* Major compatibility changes

---

# Release Naming

Development releases use:

```
0.x.y-dev
```

Release candidates:

```
0.x.y-rc1
0.x.y-rc2
```

Stable releases:

```
0.x.y
```

---

# Support Policy

The latest stable release is the primary supported version.

Development builds are intended for testing and may contain incomplete functionality.

Critical fixes may be backported to previous stable releases when practical.

---

# Historical Notes

The earliest development of PortableHermes focused on establishing a robust, portable foundation before implementing AI capabilities.

Key architectural decisions made during this phase include:

* Windows as the primary host platform
* WSL as the Linux execution environment
* Python as the implementation language for business logic
* PowerShell for Windows bootstrap
* Bash for Linux runtime orchestration
* Documentation-first development methodology
* Modular, plugin-based architecture
* Local AI model support as the default
* Strong emphasis on portability and reproducibility

These principles continue to guide future development and provide continuity as the project evolves.

---

# Future Releases

Future changelog entries should be added in reverse chronological order, with the newest release appearing immediately below the **Unreleased** section.

Each release should accurately describe user-visible changes and avoid documenting internal implementation details unless they materially affect users, contributors, or plugin developers.
