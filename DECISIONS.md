# DECISIONS.md

# PortableHermes Architecture Decisions

**Document Version:** 1.0

**Status:** Living Document

**Last Updated:** 2026-07-05

---

# Purpose

This document records major architectural and engineering decisions made during the development of PortableHermes.

Each decision captures:

* The problem
* The chosen solution
* Alternatives considered
* Reasons for the decision
* Expected consequences

The objective is to preserve engineering knowledge and avoid repeatedly revisiting previously settled design questions.

---

# Decision Format

Each decision follows this template.

```text
Decision ID
Status
Date

Problem

Decision

Alternatives

Reasoning

Consequences
```

---

# PH-001

## Title

Portable-first Architecture

## Status

Accepted

## Date

2026-07-05

### Problem

PortableHermes should run on different Windows computers without requiring installation or administrator privileges.

### Decision

The entire project shall be self-contained inside the repository directory.

Runtime data is stored locally.

No system-wide installation is required.

### Alternatives

* Traditional installer
* MSI package
* Windows service

### Reasoning

Portability is one of the primary project goals.

A portable architecture also simplifies backups and migration.

### Consequences

Advantages

* Easy deployment
* Easy backup
* Easy cloning
* Predictable runtime

Disadvantages

* Larger repository footprint
* Runtime directories must be managed carefully

---

# PH-002

## Title

Windows Bootstrap + Linux Runtime

## Status

Accepted

## Date

2026-07-05

### Problem

The application should provide a native Windows user experience while leveraging the Linux AI ecosystem.

### Decision

Windows is responsible only for bootstrap.

Python executes entirely inside WSL.

### Alternatives

* Native Windows Python
* Docker
* Hyper-V VM

### Reasoning

Linux provides significantly better compatibility with:

* llama.cpp
* CUDA
* Ollama
* AI tooling

Keeping Windows responsible only for startup minimizes platform-specific complexity.

### Consequences

Advantages

* Better AI compatibility
* Simpler runtime
* Easier maintenance

Disadvantages

* Requires WSL

---

# PH-003

## Title

Python as Primary Language

## Status

Accepted

## Date

2026-07-05

### Problem

Multiple implementation languages increase complexity.

### Decision

Business logic shall be implemented exclusively in Python.

PowerShell and Bash are limited to bootstrap and runtime orchestration.

### Alternatives

* Mixed PowerShell/Python
* C#
* Go

### Reasoning

Python offers:

* Rich AI ecosystem
* Excellent tooling
* Extensive libraries
* Strong community support

### Consequences

Simpler architecture.

Reduced duplicated logic.

---

# PH-004

## Title

Business Logic Never Lives in Scripts

## Status

Accepted

### Decision

PowerShell and Bash scripts are responsible only for:

* Environment preparation
* Validation
* Runtime startup

No application logic belongs in scripts.

### Reasoning

Shell scripting is difficult to test and maintain.

Python provides superior maintainability.

---

# PH-005

## Title

Configuration Outside Source Code

## Status

Accepted

### Decision

Configuration shall reside in JSON files.

Source code must never contain:

* API keys
* URLs
* Model names
* Tool paths
* Runtime directories

### Reasoning

Configuration changes should not require source code modifications.

---

# PH-006

## Title

Plugin-Based Architecture

## Status

Accepted

### Problem

PortableHermes is expected to grow considerably.

### Decision

Major functionality shall be implemented as plugins.

Examples include:

* Docker
* Kubernetes
* Git
* Terraform
* Home Assistant

### Alternatives

Large monolithic application.

### Reasoning

Plugins improve maintainability and reduce coupling.

---

# PH-007

## Title

Provider Abstraction

## Status

Accepted

### Problem

AI providers evolve rapidly.

### Decision

All inference engines implement a common provider interface.

Examples

* llama.cpp
* Ollama
* OpenAI
* Anthropic

### Reasoning

Switching providers should require minimal application changes.

---

# PH-008

## Title

Repository Organization

## Status

Accepted

### Decision

Repository structure follows the layout defined in REPOSITORY.md.

Generated runtime files remain isolated from source code.

### Reasoning

Clear separation simplifies maintenance.

---

# PH-009

## Title

Documentation-First Development

## Status

Accepted

### Decision

Major architectural changes require documentation updates before implementation.

Affected documents may include:

* PROJECT_SPEC.md
* ARCHITECTURE.md
* REPOSITORY.md
* CODING_STANDARD.md
* ROADMAP.md

### Reasoning

Documentation is considered part of the implementation.

---

# PH-010

## Title

Single Responsibility Principle

## Status

Accepted

### Decision

Modules should have one clearly defined responsibility.

Large classes should be decomposed.

### Reasoning

Improves maintainability.

---

# PH-011

## Title

Runtime Isolation

## Status

Accepted

### Decision

PortableHermes uses its own isolated runtime directories.

Examples

* HOME
* Cache
* State
* Temporary files

System user directories should not be modified.

### Reasoning

Supports portability and predictable behavior.

---

# PH-012

## Title

UTF-8 Encoding Policy

## Status

Accepted

### Decision

Python

UTF-8

PowerShell

UTF-8

Bash

UTF-8 without BOM

Markdown

UTF-8

### Reasoning

Avoid cross-platform encoding issues.

---

# PH-013

## Title

Line Ending Policy

## Status

Accepted

### Decision

Python

LF

Bash

LF

PowerShell

CRLF

### Reasoning

Matches platform conventions while ensuring WSL compatibility.

---

# PH-014

## Title

External Tool Management

## Status

Accepted

### Decision

PortableHermes manages its own tools inside:

```text
tools/
```

No assumptions are made about globally installed tools beyond the minimal prerequisites documented for the project.

### Reasoning

Ensures consistent behavior across systems.

---

# PH-015

## Title

Logging Strategy

## Status

Accepted

### Decision

Application logging uses a centralized logging subsystem.

Logging levels:

* DEBUG
* INFO
* WARNING
* ERROR
* CRITICAL

Direct `print()` statements are reserved for development and debugging only.

### Reasoning

Centralized logging improves diagnostics and observability.

---

# Pending Decisions

The following topics require future architectural decisions.

## GUI Framework

Status

Pending

Candidates

* PySide6
* Qt
* Tauri
* Web UI

---

## Database

Status

Pending

Candidates

* SQLite
* PostgreSQL
* DuckDB

---

## Secrets Management

Status

Pending

Candidates

* Windows Credential Manager
* Encrypted local vault
* External secret providers

---

## Plugin Marketplace

Status

Pending

Topics

* Discovery
* Installation
* Signing
* Updates
* Trust model

---

## Remote API

Status

Pending

Topics

* Authentication
* REST
* WebSocket
* gRPC

---

## Multi-user Support

Status

Pending

Topics

* User profiles
* Permissions
* Shared workspaces

---

## Telemetry

Status

Pending

Topics

* Anonymous usage statistics
* Performance metrics
* Crash reporting
* Privacy controls

---

# Decision Lifecycle

Every decision shall be assigned one of the following states:

* Proposed
* Accepted
* Superseded
* Deprecated
* Rejected

Superseded decisions remain in this document for historical reference.

They must never be deleted.

---

# Modification Policy

Changes to accepted decisions require:

1. A documented rationale.
2. Review of affected architecture documents.
3. Updates to implementation where necessary.
4. Recording of the superseding decision.

This ensures that the reasoning behind architectural changes is preserved throughout the lifetime of the project.
