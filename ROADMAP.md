# ROADMAP.md

# PortableHermes Development Roadmap

**Document Version:** 1.0

**Status:** Active

**Last Updated:** 2026-07-05

---

# Purpose

This roadmap defines the long-term development strategy for PortableHermes.

It is intended to:

* communicate project direction
* prioritize development effort
* define release goals
* document future capabilities
* guide architectural decisions

The roadmap is intentionally ambitious. Not every feature is required for the initial release.

---

# Project Vision

PortableHermes aims to become a completely self-contained AI engineering workstation that can run on any supported Windows computer without installation.

The project should provide:

* local AI assistants
* DevOps automation
* software engineering workflows
* document intelligence
* coding assistance
* extensible plugins
* reproducible environments

Long term, PortableHermes should function as an "AI Operating System" for technical professionals.

---

# Guiding Principles

Every release should improve one or more of the following:

* usability
* portability
* extensibility
* performance
* reliability
* maintainability
* documentation

Features that compromise these goals should not be merged.

---

# Release Strategy

Development follows incremental milestones.

Each release should be fully functional.

No release should intentionally leave the repository in a broken state.

Major versions represent architectural maturity rather than feature count.

---

# Development Phases

## Phase 0

Bootstrap

Status:

Completed

Goals

* Windows bootstrap
* WSL integration
* Runtime isolation
* Repository layout
* Documentation
* Logging
* Configuration loading

---

## Phase 1

Minimal AI Runtime

Target Version

v0.1

Primary Goal

Run a local LLM successfully.

Features

* Runtime launcher
* Python agent
* Configuration loader
* Basic logging
* Model discovery
* Simple CLI
* Health checks

Deliverable

PortableHermes can answer prompts using a local model.

---

## Phase 2

Core Framework

Target Version

v0.2

Features

* Service manager
* Provider abstraction
* Plugin loader
* Event system
* Settings manager
* Tool registry
* Workspace manager

Deliverable

Stable application framework.

---

## Phase 3

Developer Assistant

Target Version

v0.3

Features

* Repository analysis
* Git integration
* Pull request review
* Code explanation
* Refactoring support
* Commit generation
* Documentation generation

Supported Languages

* Python
* PowerShell
* Bash
* YAML
* JSON
* Markdown

---

## Phase 4

DevOps Assistant

Target Version

v0.4

Features

* Docker
* Kubernetes
* Helm
* Terraform
* Ansible
* GitHub Actions
* GitLab CI
* Jenkins
* Azure DevOps

Capabilities

* Pipeline review
* Security recommendations
* Infrastructure explanation
* Deployment validation

---

## Phase 5

Infrastructure Intelligence

Target Version

v0.5

Features

* SSH support
* Remote execution
* Log analysis
* Linux diagnostics
* Windows diagnostics
* Network inspection

Future

Optional agent mode.

---

## Phase 6

Knowledge Management

Target Version

v0.6

Features

* Document indexing
* Vector database
* Semantic search
* Personal knowledge base
* PDF ingestion
* Markdown indexing

Supported Formats

* PDF
* Markdown
* DOCX
* TXT
* HTML

---

## Phase 7

Automation Platform

Target Version

v0.7

Features

* Scheduled tasks
* Workflow engine
* Automation rules
* Notification system
* Event triggers

Possible Integrations

* Discord
* Slack
* Email
* Telegram
* Home Assistant

---

## Phase 8

Desktop Application

Target Version

v0.8

Features

* GUI
* Settings editor
* Chat interface
* Model manager
* Plugin manager
* Update manager

Current Candidate

PySide6

---

## Phase 9

Advanced AI

Target Version

v0.9

Features

* Multi-agent workflows
* Long-term memory
* Tool chaining
* Autonomous planning
* Context compression
* Session persistence

---

## Phase 10

Production Release

Target Version

v1.0

Goals

* Stable APIs
* Stable plugin system
* Complete documentation
* Automated testing
* Installer
* Update mechanism

---

# AI Provider Roadmap

## Initial

* llama.cpp

## Planned

* Ollama
* OpenAI
* Anthropic
* Google Gemini
* Azure OpenAI
* OpenRouter

Future providers can be added through the provider abstraction layer.

---

# Local Model Roadmap

Supported families should include:

* Qwen
* DeepSeek
* Llama
* Phi
* Mistral
* Gemma

Model management should eventually include:

* discovery
* download
* updates
* quantization information
* GPU compatibility

---

# Plugin Roadmap

Core plugins

* Git
* Docker
* Kubernetes
* Terraform
* Ansible

Developer plugins

* Python
* PowerShell
* Bash
* YAML
* JSON

Infrastructure plugins

* SSH
* Linux
* Windows
* Networking

AI plugins

* Image generation
* Speech recognition
* Text-to-speech
* Embeddings

Personal productivity

* Calendar
* Notes
* Knowledge base

Home automation

* Home Assistant
* MQTT

Future

Community-developed plugins.

---

# User Interface Roadmap

CLI

First release.

GUI

Second milestone.

Web interface

Optional.

REST API

Planned.

Remote dashboard

Future consideration.

---

# Security Roadmap

Planned improvements

* encrypted configuration
* secret vault
* API key management
* plugin signing
* integrity verification
* secure updates

---

# Performance Roadmap

Future optimization work

* lazy plugin loading
* model caching
* startup optimization
* asynchronous execution
* GPU scheduling
* parallel indexing

---

# Documentation Roadmap

Required documents

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

Future documentation

* Plugin SDK
* API Reference
* User Manual
* Administrator Guide
* Troubleshooting Guide
* Developer Guide

---

# Technical Debt

Known future improvements

* Improve Windows bootstrap diagnostics
* Better WSL detection
* Automatic dependency installation
* Improved logging
* Configuration validation
* Runtime health monitoring
* Update manager
* Plugin sandboxing

Technical debt should be tracked continuously and addressed incrementally.

---

# Stretch Goals

These features are desirable but not required for v1.0.

* Voice assistant
* OCR support
* Local speech-to-text
* Local text-to-speech
* Multi-user profiles
* Distributed agents
* Remote execution clusters
* AI workflow designer
* Visual automation builder
* Local image generation
* Local video generation
* 3D model generation for CAD and 3D printing
* RAG knowledge graph
* MCP server/client support
* Native mobile companion application

---

# Success Criteria

PortableHermes v1.0 will be considered successful if it can:

* bootstrap on a clean Windows system
* launch a Linux runtime automatically
* load local AI models
* manage plugins
* analyze repositories
* assist with DevOps workflows
* maintain isolated runtime environments
* operate without installation
* provide complete documentation
* be easily extended by contributors

---

# Long-Term Vision

PortableHermes should evolve into a modular, extensible AI platform that combines local intelligence, developer tooling, infrastructure automation, and personal knowledge management into a single portable application.

The architecture should remain stable while allowing rapid expansion through plugins, provider integrations, and community contributions.
