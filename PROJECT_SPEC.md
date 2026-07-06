# PortableHermes Project Specification

**Document Version:** 1.0

**Status:** Living Document

**Last Updated:** 2026-07-05

---

# 1. Purpose

PortableHermes is a portable AI workstation designed to provide a complete local AI ecosystem from a single directory without requiring installation.

The project is intended to be:

* portable
* self-contained
* offline-first
* modular
* extensible
* open-source

PortableHermes is not simply an AI application. It is an extensible platform capable of managing AI models, developer tools, automation workflows, and local services through a unified runtime.

---

# 2. Vision

A user should be able to:

1. Clone or extract the repository.
2. Execute:

```text
bootstrap/Start.ps1
```

3. Begin using PortableHermes immediately.

No manual installation.

No environment configuration.

No dependency management performed by the user.

Everything required by the runtime is handled automatically.

---

# 3. Long-Term Objectives

PortableHermes shall provide:

* Local LLM execution
* Image generation
* Future voice generation
* Future video generation
* Future 3D model generation
* DevOps automation
* Local MCP server hosting
* Plugin management
* Tool management
* Runtime management
* Automatic updates
* Cross-platform operation

---

# 4. Supported Platforms

## Initial

Host Operating System

* Windows 11

Runtime

* WSL2
* Ubuntu LTS

---

## Future

Host

* Native Linux

Potential Future

* macOS

---

# 5. Architectural Principles

## Python is the Core

Business logic belongs exclusively in Python.

Python owns:

* runtime
* configuration
* logging
* plugins
* tools
* AI providers
* models
* scheduling
* event system

Neither PowerShell nor Bash shall contain business logic.

---

## Windows Performs Bootstrap Only

PowerShell is responsible only for:

* startup
* logging initialization
* directory creation
* configuration loading
* WSL detection
* launching Linux runtime

No application logic belongs in PowerShell.

---

## Linux Performs Runtime Preparation Only

Bash is responsible only for:

* environment variables
* runtime isolation
* directory verification
* launching Python

Linux scripts must remain minimal.

---

## Configuration Driven

Behavior shall never be controlled by hardcoded values when configuration is appropriate.

Configuration files define:

* logging
* runtime
* tools
* plugins
* models
* networking
* updates

---

## Plugin Architecture

PortableHermes Core must not depend directly on external tools.

Every integration shall be implemented as a plugin.

Examples:

* Docker
* Git
* Terraform
* Kubernetes
* Home Assistant
* Ollama
* llama.cpp
* ComfyUI

The core should remain unchanged when new plugins are introduced.

---

## Provider Architecture

AI providers are independent modules.

Examples:

* llama.cpp
* Ollama
* OpenAI-compatible
* Anthropic-compatible
* HuggingFace

The remainder of Hermes interacts only with a provider interface.

---

# 6. Repository Structure

```text
bootstrap/
config/
core/
docs/
hermes/
plugins/
providers/
scripts/
resources/

runtime/
workspace/
cache/
state/
tools/
downloads/
logs/
backups/
tmp/
```

Generated directories are excluded from version control.

---

# 7. Startup Flow

Windows

↓

Bootstrap.ps1

↓

Runtime.ps1

↓

WSL

↓

launch.sh

↓

python -m hermes

↓

Hermes Core

↓

Plugins

↓

User Interface

---

# 8. Runtime Lifecycle

Initialization

↓

Configuration

↓

Logging

↓

Environment

↓

Plugin Discovery

↓

Provider Discovery

↓

Tool Discovery

↓

Model Discovery

↓

Scheduler

↓

CLI / GUI

↓

Runtime Loop

---

# 9. Hermes Core Components

The Python runtime shall eventually contain the following subsystems.

## Configuration Manager

Loads all configuration.

Validates schema.

Provides runtime configuration.

---

## Logging Manager

Structured logging.

Multiple outputs.

Runtime log levels.

Log rotation.

---

## Runtime Manager

Startup.

Shutdown.

Lifecycle.

Environment validation.

---

## Plugin Manager

Discovers plugins.

Loads plugins.

Dependency validation.

Plugin lifecycle.

---

## Provider Manager

Loads AI providers.

Provider selection.

Capability discovery.

---

## Model Manager

Installed models.

Model metadata.

Downloads.

Updates.

Storage management.

---

## Tool Manager

External tools.

Version management.

Installation.

Updates.

Capability discovery.

---

## MCP Manager

Server lifecycle.

Discovery.

Configuration.

Health monitoring.

---

## Scheduler

Background tasks.

Updates.

Health checks.

Maintenance.

---

## CLI

Interactive command interface.

Automation entry point.

---

## GUI (Future)

Desktop application.

Visualization.

Configuration.

Monitoring.

---

# 10. Configuration System

Configuration shall be separated by responsibility.

Example:

```text
config/

runtime.json

logging.json

models.json

plugins.json

providers.json

network.json

tools.json
```

Every configuration file shall have schema validation.

---

# 11. Logging Requirements

Logging shall support:

* Console
* File
* Structured JSON (future)

Levels:

* DEBUG
* INFO
* WARNING
* ERROR
* CRITICAL

Every subsystem shall use the same logging framework.

---

# 12. Security Principles

Secrets shall never be committed.

API keys belong in:

* GitHub Secrets
* Environment Variables
* Future Secure Credential Store

PortableHermes should operate with the principle of least privilege.

---

# 13. Development Philosophy

The project values:

* readability
* maintainability
* modularity
* explicit behavior
* portability
* automation

Premature optimization should be avoided.

Clear architecture is preferred over clever implementation.

---

# 14. Release Strategy

Development progresses through incremental milestones.

Current target:

v0.0.3

Foundation

Next:

v0.0.4

Runtime

v0.0.5

Plugin Framework

v0.0.6

AI Integration

v0.1

First Stable Release

---

# 15. Definition of Done

A feature is complete only when:

* implementation finished
* documented
* tested
* logged in CHANGELOG
* migration documented if required
* no duplicated logic introduced
* coding standards satisfied

---

# 16. Source of Truth

This document is the primary architectural reference for PortableHermes.

If implementation conflicts with this specification, the implementation should be considered incorrect unless this specification is explicitly revised.

All future architectural decisions should update this document or an accompanying Architecture Decision Record (ADR).
