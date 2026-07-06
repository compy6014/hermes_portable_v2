# PortableHermes

> A portable, self-contained AI workstation for Windows and Linux.

---

## Overview

PortableHermes is an open-source project whose goal is to provide a completely portable AI workstation capable of running entirely from a single directory without requiring installation.

The project combines:

* Local Large Language Models
* AI tool orchestration
* DevOps automation
* MCP server hosting
* Python runtime management
* Model management
* Tool management
* Future GUI support

PortableHermes is designed to run primarily on Windows while executing its runtime inside WSL2 Ubuntu. The long-term objective is to support native Linux with minimal changes.

---

# Project Goals

PortableHermes should be able to:

* bootstrap itself
* require no installer
* manage its own runtime
* download required tools automatically
* host local AI models
* expose a unified CLI
* expose a future desktop GUI
* remain completely portable

A user should only need to execute:

```
bootstrap/Start.ps1
```

Everything else should happen automatically.

---

# Core Principles

## Portable

Nothing should depend on system installation whenever possible.

The repository should remain movable to another drive or computer.

---

## Offline First

Internet access should only be required when downloading optional components.

The core runtime must work completely offline.

---

## Modular

Every major capability should exist as its own module.

Examples:

* Logger
* Runtime
* Configuration
* Plugin Manager
* Tool Manager
* Model Manager

---

## Plugin Based

The Hermes Core should not know about individual tools.

Docker, Git, Home Assistant, Terraform, Kubernetes, Ollama, llama.cpp and future integrations should all be implemented as plugins.

---

## Configuration Driven

Behavior should be controlled by configuration files instead of hardcoded values.

---

## Cross Platform

Initial support:

* Windows 11
* WSL2 Ubuntu

Future support:

* Native Linux

---

# High-Level Architecture

```
Windows

↓

Bootstrap (PowerShell)

↓

WSL Runtime

↓

Linux Launcher

↓

Hermes Core (Python)

↓

Plugins
Models
Tools
MCP
```

Business logic belongs in Python.

PowerShell performs bootstrap.

Bash prepares Linux.

---

# Repository Layout

```
bootstrap/
config/
core/
docs/
hermes/
plugins/
providers/
scripts/
runtime/
workspace/
tools/
logs/
```

Generated directories are excluded from version control.

---

# Development Roadmap

## v0.0.3

Foundation

* Bootstrap
* Logger
* Configuration
* Runtime Bridge
* Linux Launcher
* Python Skeleton

---

## v0.0.4

Runtime

* Python Environment
* Package Installer
* Tool Downloader
* Runtime Manager

---

## v0.0.5

Plugin System

* Plugin Loader
* Tool Registry
* Extension API

---

## v0.0.6

AI

* llama.cpp
* Ollama
* OpenAI-compatible APIs
* Model Manager
* Routing

---

## v0.1

First usable release.

---

# Development Workflow

Development follows release milestones.

Every release should include:

* updated documentation
* changelog
* migration notes
* testing checklist

---

# Coding Standards

See:

* CODING_STANDARD.md

---

# Architecture

See:

* ARCHITECTURE.md

---

# Roadmap

See:

* ROADMAP.md

---

# Contributing

See:

* CONTRIBUTING.md

---

# License

To be determined.

