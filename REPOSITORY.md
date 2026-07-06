# REPOSITORY.md

# PortableHermes Repository Organization

**Document Version:** 1.0

**Status:** Living Document

**Last Updated:** 2026-07-05

---

# 1. Purpose

This document defines the official repository structure for PortableHermes.

Every directory has a clearly defined responsibility.

No file should exist without belonging to one of these responsibilities.

Whenever possible:

* directories should have a single purpose
* responsibilities should never overlap
* business logic belongs only in Python

---

# 2. Repository Layout

```text
PortableHermes/

├── bootstrap/
├── config/
├── core/
├── docs/
├── hermes/
├── plugins/
├── providers/
├── resources/
├── scripts/
│
├── runtime/
├── workspace/
├── cache/
├── state/
├── logs/
├── tmp/
├── tools/
├── downloads/
├── backups/
│
├── tests/
│
├── .github/
│
├── README.md
├── PROJECT_SPEC.md
├── ARCHITECTURE.md
├── REPOSITORY.md
├── ROADMAP.md
├── CODING_STANDARD.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── TESTING.md
├── TODO.md
└── LICENSE
```

---

# 3. Directory Responsibilities

## bootstrap/

Purpose

Platform bootstrap.

Contains the minimal code required to start PortableHermes.

Typical contents:

```text
Start.ps1
Bootstrap.ps1
```

Allowed

* startup
* runtime detection
* environment validation

Forbidden

* application logic
* AI logic
* plugin management

---

## config/

Purpose

Static configuration.

Example:

```text
logging.json

runtime.json

providers.json

plugins.json

models.json

tools.json

network.json
```

Only configuration belongs here.

No generated files.

---

## core/

Purpose

Low-level reusable Python infrastructure.

Examples

```text
logging/

configuration/

runtime/

events/

scheduler/

filesystem/

security/
```

Everything inside core should be reusable by higher layers.

Core should never depend on plugins.

---

## hermes/

Purpose

Main application.

Example

```text
hermes/

main.py

cli.py

application.py

bootstrap.py

services/
```

This is the entry point for the Python runtime.

---

## plugins/

Purpose

Feature extensions.

Every plugin lives in its own directory.

Example

```text
plugins/

docker/

git/

terraform/

kubernetes/

homeassistant/
```

Plugins communicate with Hermes through public interfaces.

Plugins should not communicate directly with one another.

---

## providers/

Purpose

AI inference providers.

Example

```text
providers/

llamacpp/

ollama/

openai/

anthropic/

huggingface/
```

Provider implementations expose a common interface.

---

## resources/

Purpose

Static assets.

Examples

* icons
* images
* templates
* prompt libraries
* default configurations

Resources contain no executable code.

---

## scripts/

Purpose

Operating-system-specific helper scripts.

Example

```text
scripts/

linux/

windows/
```

Scripts should never contain business logic.

---

## docs/

Purpose

Project documentation.

Contains:

* specifications
* ADRs
* diagrams
* user guides
* developer guides

---

## tests/

Purpose

Automated tests.

Structure should mirror the source tree.

Example

```text
tests/

core/

plugins/

providers/

integration/

unit/
```

---

## .github/

Purpose

GitHub automation.

Contains

* workflows
* issue templates
* pull request templates
* discussions configuration

---

# 4. Generated Directories

The following directories are generated at runtime.

They should not contain source code.

---

## runtime/

Contains runtime HOME.

Typical contents

```text
runtime/

config/

share/

venv/
```

May be deleted and recreated.

---

## workspace/

User projects.

Scratch files.

Temporary work.

PortableHermes never stores source code here.

---

## cache/

Downloaded cache.

May be safely deleted.

---

## state/

Persistent runtime state.

Examples

* installed tools
* plugin state
* runtime database

---

## logs/

Application logs.

Rotated automatically.

May be cleaned periodically.

---

## tmp/

Temporary files.

Always disposable.

---

## downloads/

Temporary download storage.

---

## backups/

Configuration backups.

Database backups.

Export archives.

---

# 5. Python Package Layout

Recommended structure

```text
hermes/

application.py

main.py

cli.py

runtime.py

config.py

logging.py

events.py

services/

models/

interfaces/
```

Modules should remain small.

Prefer composition over inheritance.

---

# 6. Plugin Layout

Every plugin follows the same structure.

Example

```text
plugins/

docker/

plugin.py

manifest.json

config.json

README.md
```

Future additions

```text
icons/

tests/

resources/
```

---

# 7. Provider Layout

Each provider is isolated.

Example

```text
providers/

llamacpp/

provider.py

config.py

manifest.json
```

Providers should not know about other providers.

---

# 8. Naming Conventions

Directories

lowercase

Example

```text
runtime

providers

plugins
```

Python packages

snake_case

Python classes

PascalCase

Python functions

snake_case

Constants

UPPER_CASE

Configuration

lowercase JSON filenames

---

# 9. File Ownership

Every file has one owner.

Example

Bootstrap

bootstrap/

Runtime

core/runtime/

Configuration

core/config/

Providers

providers/

Plugins

plugins/

Avoid duplicate implementations.

---

# 10. Dependency Rules

Allowed

```text
bootstrap

↓

scripts

↓

hermes

↓

core

↓

providers

↓

plugins
```

Forbidden

Plugins importing bootstrap.

Providers importing plugins.

Bootstrap importing providers.

Core importing plugins.

Circular dependencies are not permitted.

---

# 11. Repository Growth Strategy

New functionality should be added by introducing:

* new plugin
* new provider
* new manager
* new service

Avoid modifying stable components whenever practical.

---

# 12. Documentation Requirements

Every public module should eventually include:

README.md

Purpose

Responsibilities

Dependencies

Examples

Future work

---

# 13. Versioning

Repository structure should evolve conservatively.

Breaking structural changes require:

* PROJECT_SPEC update
* ARCHITECTURE update
* CHANGELOG entry
* ADR (Architecture Decision Record)

---

# 14. Repository Principles

1. Every directory has one responsibility.
2. Generated files never mix with source code.
3. Business logic belongs in Python.
4. Platform scripts remain minimal.
5. Configuration remains external.
6. Plugins remain isolated.
7. Providers remain interchangeable.
8. Repository organization should remain stable as the project grows.

---

# 15. Future Expansion

The repository is expected to grow to include:

* Multiple AI providers
* Multiple model families
* Desktop GUI
* REST API
* Web UI
* Voice interfaces
* Image generation
* 3D model generation
* DevOps automation modules
* Home automation integrations
* Monitoring and telemetry

The repository structure defined in this document is intended to accommodate that growth without requiring major reorganization.
