# TESTING.md

# PortableHermes Testing Strategy

**Document Version:** 1.0

**Status:** Active

**Last Updated:** 2026-07-05

---

# Purpose

This document defines the testing strategy for PortableHermes.

Testing aims to ensure:

* reliability
* portability
* reproducibility
* maintainability
* regression prevention

Every component of PortableHermes should be testable independently.

---

# Testing Philosophy

PortableHermes follows a layered testing approach.

```
Manual Validation
        ▲
Acceptance Tests
        ▲
Integration Tests
        ▲
Component Tests
        ▲
Unit Tests
```

Lower layers should provide confidence before higher layers are executed.

---

# Testing Goals

Every release should verify:

* bootstrap functionality
* WSL integration
* runtime initialization
* Python components
* plugin loading
* AI providers
* configuration parsing
* logging
* file system isolation

---

# Test Categories

## Unit Tests

Purpose

Verify a single function or class.

Characteristics

* fast
* isolated
* deterministic
* no external dependencies

Examples

* Config parser
* Logger
* Utility functions
* Provider selection
* Plugin discovery

Framework

pytest

Target Coverage

90%+

---

## Component Tests

Purpose

Verify one module.

Examples

* Runtime Manager
* Provider Manager
* Plugin Loader
* Workspace Manager
* Configuration Loader

External systems should be mocked whenever possible.

---

## Integration Tests

Purpose

Verify interaction between multiple components.

Examples

Windows Bootstrap

↓

WSL Runtime

↓

Python Agent

↓

Provider

↓

Response

These tests validate complete execution paths.

---

## End-to-End Tests

Purpose

Validate the complete application.

Example

Start.ps1

↓

Environment

↓

WSL

↓

launch.sh

↓

Python

↓

Agent

↓

Model

↓

Response

These tests simulate real user execution.

---

## Regression Tests

Purpose

Prevent previously fixed bugs from returning.

Every resolved bug should include a regression test when practical.

---

# Platform Testing

## Windows

Verify

* Bootstrap
* Configuration
* Logging
* Runtime directories
* WSL detection
* Path conversion

Supported Versions

* Windows 11
* Windows 10 (best effort)

---

## WSL

Verify

* Distribution detection
* Path translation
* Bash execution
* Environment initialization

Supported

* Ubuntu 22.04+
* Ubuntu 24.04+

---

## Linux Runtime

Verify

* environment.sh
* launch.sh
* Python startup
* Runtime isolation

---

# Python Testing

Every Python package should include tests.

Example layout

```
tests/

    unit/

    integration/

    providers/

    plugins/

    regression/
```

---

# Bootstrap Testing

Test Cases

✓ Project root detection

✓ Configuration loading

✓ Runtime directory creation

✓ Logging initialization

✓ WSL detection

✓ Runtime launch

Failure Cases

Missing config

Missing runtime

Missing WSL

Invalid paths

Permission issues

---

# Runtime Testing

Verify

* HOME isolation
* Cache
* State
* Temporary files
* Tool discovery
* Environment variables

---

# Configuration Testing

Validate

* Required fields
* Optional fields
* Invalid JSON
* Missing values
* Default values

---

# Plugin Testing

Every plugin should verify

Initialization

Configuration

Registration

Execution

Shutdown

Error handling

A failing plugin must never crash PortableHermes.

---

# Provider Testing

Every AI provider must support identical tests.

Examples

Model listing

Prompt execution

Streaming

Error handling

Timeout

Cancellation

Token counting

Capability discovery

---

# CLI Testing

Verify

* help
* version
* configuration
* logging
* prompt execution
* invalid arguments

---

# Logging Tests

Verify

DEBUG

INFO

WARNING

ERROR

CRITICAL

Also verify

* timestamps
* formatting
* log rotation
* file output

---

# Configuration Validation Tests

Every configuration file should be validated.

Examples

config.json

providers.json

models.json

plugins.json

Expected validation

Required fields

Data types

Duplicate entries

Unknown fields

---

# File System Tests

Verify

Runtime directories

Workspace

Cache

Downloads

Logs

Temporary files

Backups

Nothing should be written outside the project unless explicitly configured.

---

# Performance Testing

Measure

Startup time

Model loading

Plugin loading

Prompt latency

Memory usage

GPU utilization

Large repository indexing

---

# Memory Testing

Monitor

Memory leaks

Context growth

Cache cleanup

Session persistence

Long-running workloads

---

# Stress Testing

Examples

100 plugin loads

Large repositories

Large documents

Long conversations

Large prompts

Multiple providers

Repeated startup/shutdown

---

# Security Testing

Verify

Secret handling

Configuration isolation

Plugin sandboxing

Temporary files

Permissions

Path traversal prevention

---

# WSL Validation Matrix

Required Tests

✓ WSL available

✓ Distribution exists

✓ Bash available

✓ Project mount accessible

✓ Runtime directories writable

✓ Python installed

✓ Launch script executable

---

# AI Testing

Every supported model family should be tested.

Examples

Qwen

DeepSeek

Llama

Phi

Mistral

Gemma

Validation

Prompt execution

Streaming

Tool calling

Context limits

Performance

---

# Plugin Compatibility Matrix

Each release should verify compatibility.

| Plugin         | Unit | Integration | E2E |
| -------------- | ---- | ----------- | --- |
| Git            | ✓    | ✓           | ✓   |
| Docker         | ✓    | ✓           | ✓   |
| Kubernetes     | ✓    | ✓           | ✓   |
| Terraform      | ✓    | ✓           | ✓   |
| Home Assistant | ✓    | ✓           | ✓   |

---

# Continuous Integration

Every Pull Request should execute

Formatting

Linting

Unit Tests

Integration Tests

Documentation Validation

Static Analysis

No Pull Request should be merged if required checks fail.

---

# Code Coverage

Targets

Core libraries

95%

Plugins

85%

Providers

90%

Overall project

90%

Coverage should guide testing but never replace thoughtful test design.

---

# Manual Test Checklist

Before every release verify

□ Fresh clone works

□ Windows bootstrap succeeds

□ WSL runtime launches

□ Python starts

□ Configuration loads

□ Runtime directories created

□ Logs generated

□ AI provider loads

□ Sample prompt succeeds

□ Shutdown completes cleanly

---

# Release Acceptance Criteria

A release is acceptable only if

* all automated tests pass
* documentation is updated
* no critical defects remain
* regression suite passes
* manual validation succeeds

---

# Bug Reporting

Every reported defect should include

Operating System

PortableHermes version

Python version

WSL version

AI provider

Model

Steps to reproduce

Expected behavior

Actual behavior

Relevant logs

---

# Future Improvements

Planned additions

* Automated GUI testing
* Performance benchmarking dashboard
* GPU stress tests
* Multi-platform CI
* Plugin certification tests
* AI response quality benchmarks
* Chaos testing for provider failures
* Automated upgrade and migration testing

---

# Testing Principles

PortableHermes values correctness over speed.

Every new feature should include appropriate tests.

Every bug fix should include a regression test whenever practical.

Testing is considered part of the implementation, not an optional post-development activity.
