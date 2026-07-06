# ARCHITECTURE.md

# PortableHermes Architecture

**Document Version:** 1.0

**Status:** Living Document

**Last Updated:** 2026-07-05

---

# 1. Overview

PortableHermes is architected as a layered, modular platform that separates platform-specific concerns from application logic.

The architecture follows these core principles:

* Separation of concerns
* Single responsibility
* Modular components
* Plugin-first design
* Configuration-driven behavior
* Platform abstraction

The vast majority of application logic resides within the Python runtime. Platform-specific scripts exist only to bootstrap the environment and start the Python runtime.

---

# 2. High-Level Architecture

```text
                +----------------------+
                |      Windows 11      |
                +----------+-----------+
                           |
                           |
                           v
                 bootstrap/Start.ps1
                           |
                           v
                    Runtime.ps1
                           |
                           v
                      WSL Runtime
                           |
                           v
               scripts/linux/launch.sh
                           |
                           v
                 python -m hermes
                           |
                           v
                  Hermes Core Runtime
                           |
      +--------------------+--------------------+
      |                    |                    |
      v                    v                    v
 Configuration       Runtime Manager      Plugin Manager
      |                    |                    |
      +---------+----------+----------+---------+
                |                     |
                v                     v
          Provider Manager      Tool Manager
                |                     |
                +----------+----------+
                           |
                           v
                    AI Providers
```

---

# 3. Layered Architecture

PortableHermes is divided into six logical layers.

```text
Layer 6  User Interfaces

CLI
GUI (Future)
REST API (Future)

──────────────────────────────────────────

Layer 5  Services

Plugins
Providers
Tools
Models
MCP

──────────────────────────────────────────

Layer 4  Core

Runtime
Configuration
Logging
Scheduler
Events

──────────────────────────────────────────

Layer 3  Platform

Windows
Linux
WSL

──────────────────────────────────────────

Layer 2  Bootstrap

PowerShell
Bash

──────────────────────────────────────────

Layer 1  Operating System

Windows
Linux
```

Dependencies always flow downward. Lower layers must never depend on higher layers.

---

# 4. Startup Sequence

```text
User

↓

Start.ps1

↓

Initialize Logger

↓

Load Configuration

↓

Create Runtime Directories

↓

Validate Environment

↓

Validate WSL

↓

Launch Linux Runtime

↓

launch.sh

↓

Load Linux Environment

↓

Filesystem Isolation

↓

Start Python Runtime

↓

Hermes Core

↓

Discover Plugins

↓

Discover Providers

↓

Discover Models

↓

Initialize Scheduler

↓

Ready
```

---

# 5. Runtime Responsibilities

## Windows Bootstrap

Responsible for:

* Project root detection
* Logger initialization
* Configuration loading
* Runtime directory creation
* WSL validation
* Launching Linux runtime

Not responsible for:

* Business logic
* Plugins
* Models
* AI
* Tools

---

## Linux Launcher

Responsible for:

* Environment variables
* Runtime isolation
* XDG directory setup
* HOME redirection
* Temporary directory setup
* Starting Python

Not responsible for:

* Configuration parsing
* Plugin loading
* AI execution

---

## Python Runtime

Responsible for everything else.

This includes:

* Runtime lifecycle
* Configuration
* Logging
* Plugins
* Providers
* Models
* Scheduler
* CLI
* Future GUI
* Update system

---

# 6. Hermes Core

Hermes Core is the central orchestrator of the entire platform.

```text
Hermes Core

├── Runtime Manager
├── Configuration Manager
├── Logging Manager
├── Event Bus
├── Scheduler
├── Plugin Manager
├── Provider Manager
├── Tool Manager
├── Model Manager
├── MCP Manager
├── Update Manager
└── CLI
```

Each subsystem has a single responsibility and communicates through well-defined interfaces.

---

# 7. Runtime Manager

Responsibilities:

* Startup
* Shutdown
* Health checks
* Lifecycle state
* Dependency validation

The Runtime Manager is the first Python component to initialize and the last to terminate.

---

# 8. Configuration Manager

Loads configuration from the `config/` directory.

Responsibilities:

* File loading
* Schema validation
* Default values
* Runtime overrides
* Configuration caching

No component should read configuration files directly.

---

# 9. Logging Manager

Provides centralized logging.

Features:

* Console output
* File logging
* Log levels
* Log rotation (future)
* Structured JSON logging (future)

Every component receives a logger from the Logging Manager.

---

# 10. Event Bus

Components communicate through events rather than direct coupling.

Example:

```text
Model Installed

↓

Event Bus

↓

Plugin Manager

↓

Scheduler

↓

GUI
```

This architecture minimizes dependencies between components.

---

# 11. Scheduler

Executes background tasks.

Examples:

* Update checks
* Plugin health checks
* Model indexing
* Cleanup
* Telemetry (optional)

Tasks are scheduled independently of the user interface.

---

# 12. Plugin Manager

Discovers and manages plugins.

Plugin lifecycle:

```text
Discover

↓

Validate

↓

Load

↓

Initialize

↓

Register Services

↓

Ready
```

Future plugin types may include:

* Tool plugins
* AI provider plugins
* GUI extensions
* Automation workflows

---

# 13. Provider Manager

AI providers expose a common interface.

Examples:

* llama.cpp
* Ollama
* OpenAI-compatible
* Anthropic-compatible
* Hugging Face
* Future providers

The rest of Hermes interacts only with the provider interface, never with provider-specific APIs.

---

# 14. Model Manager

Tracks installed models.

Responsibilities:

* Installation
* Updates
* Metadata
* Storage locations
* Compatibility checks

The Model Manager does not execute models; execution is delegated to providers.

---

# 15. Tool Manager

Responsible for external development tools.

Examples:

* Git
* Docker
* Terraform
* Kubernetes
* Helm
* kubectl
* Python
* Node.js

Functions:

* Installation
* Version management
* Updates
* Discovery
* Validation

---

# 16. MCP Manager

Responsible for Model Context Protocol servers.

Responsibilities:

* Discovery
* Configuration
* Lifecycle management
* Health monitoring

MCP servers should be configurable and independently managed.

---

# 17. Update Manager

Handles updates for:

* PortableHermes
* Plugins
* Models
* Tools
* Providers

Updates should support offline caching and integrity verification.

---

# 18. Plugin Architecture

All extensions implement a common interface.

```text
Plugin

Initialize()

Start()

Stop()

HealthCheck()

Shutdown()
```

Plugins should not depend on one another unless explicitly declared.

Dependencies are resolved by the Plugin Manager.

---

# 19. Error Handling

Errors are categorized as:

* Recoverable
* Configuration
* Dependency
* Runtime
* Fatal

Fatal errors terminate initialization with a clear diagnostic message.

Recoverable errors are logged and reported to the user without stopping the runtime where possible.

---

# 20. Future GUI

The GUI will act as a client of Hermes Core.

It will not contain business logic.

Communication will occur through internal APIs or the event bus.

This allows CLI and GUI to share the same runtime.

---

# 21. Security Model

PortableHermes follows the principle of least privilege.

Secrets are never stored in source code.

Future secure credential storage may integrate with operating system facilities where appropriate.

---

# 22. Extensibility

New functionality should be added by introducing new plugins, providers, or managers rather than modifying existing core components whenever practical.

The architecture is intended to evolve without requiring large-scale refactoring.

---

# 23. Architectural Principles Summary

1. Python owns application logic.
2. Bootstrap scripts remain minimal.
3. Configuration drives behavior.
4. Plugins isolate integrations.
5. Providers abstract AI backends.
6. Components communicate through interfaces and events.
7. Business logic is independent of operating system specifics.
8. The platform remains portable and self-contained.
