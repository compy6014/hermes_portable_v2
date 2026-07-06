# CODING_STANDARD.md

# PortableHermes Coding Standards

**Document Version:** 1.0

**Status:** Living Document

**Last Updated:** 2026-07-05

---

# 1. Purpose

This document defines the official coding standards for PortableHermes.

Its objectives are to:

* Maintain a consistent codebase
* Improve readability
* Reduce bugs
* Simplify maintenance
* Support long-term development
* Minimize unnecessary refactoring

These standards apply to every contribution.

---

# 2. General Principles

Code should prioritize:

* Readability
* Simplicity
* Maintainability
* Explicit behavior
* Testability
* Modularity

Avoid "clever" implementations when a simpler solution exists.

Code is read far more often than it is written.

---

# 3. Supported Languages

Primary language

* Python

Bootstrap

* PowerShell

Linux Runtime

* Bash

Configuration

* JSON

Documentation

* Markdown

---

# 4. Language Versions

Python

```text
Python 3.12+
```

PowerShell

```text
PowerShell 7+
```

Bash

```text
GNU Bash 5+
```

---

# 5. File Encoding

## Python

Encoding

```text
UTF-8
```

Line endings

```text
LF
```

---

## Bash

Encoding

```text
UTF-8 without BOM
```

Line endings

```text
LF
```

---

## PowerShell

Encoding

```text
UTF-8
```

Line endings

```text
CRLF
```

---

## Markdown

Encoding

```text
UTF-8
```

Line endings

Either LF or CRLF are acceptable.

---

# 6. Repository Rules

Source code shall never be generated inside:

* runtime/
* workspace/
* cache/
* state/
* downloads/
* tmp/

Generated files belong only in runtime directories.

---

# 7. Python Style

Formatting

* Black

Linting

* Ruff

Type checking

* mypy (future)

PEP 8 compliance is expected unless an explicit exception improves readability.

---

# 8. Type Hints

Every public function shall include type hints.

Example

```python
def load_configuration(path: Path) -> Configuration:
```

Avoid using `Any` unless absolutely necessary.

---

# 9. Imports

Imports are grouped as:

1. Standard Library
2. Third-party Packages
3. Hermes Packages

Example

```python
import json
from pathlib import Path

import requests

from hermes.runtime import Runtime
```

Wildcard imports are prohibited.

```python
from module import *
```

Never use them.

---

# 10. Naming Conventions

## Modules

snake_case

```text
runtime_manager.py
```

---

## Packages

snake_case

```text
provider_manager
```

---

## Classes

PascalCase

```python
class RuntimeManager:
```

---

## Functions

snake_case

```python
load_runtime()
```

---

## Variables

snake_case

```python
project_root
```

---

## Constants

UPPER_CASE

```python
DEFAULT_TIMEOUT
```

---

## Private Members

Prefix with underscore.

```python
_initialize()
```

---

# 11. Class Design

Classes should have a single responsibility.

Prefer composition over inheritance.

Avoid "god classes."

Classes larger than approximately 500 lines should be evaluated for decomposition.

---

# 12. Function Design

Functions should:

* Do one thing
* Have descriptive names
* Return predictable values
* Avoid side effects where practical

Aim for functions under 50 lines.

Longer functions require justification.

---

# 13. Error Handling

Do not silently ignore exceptions.

Bad

```python
try:
    ...
except:
    pass
```

Good

* Catch specific exceptions
* Log the error
* Recover if possible
* Re-raise when appropriate

---

# 14. Logging

Never use:

```python
print()
```

inside production Python code.

Always use the Hermes logging framework.

Log levels

* DEBUG
* INFO
* WARNING
* ERROR
* CRITICAL

Log messages should describe:

* What happened
* Why it happened (if known)
* What component generated it

---

# 15. Configuration

Never hardcode:

* Paths
* Ports
* URLs
* API endpoints
* Tokens
* Model names
* Tool locations

These belong in configuration files.

---

# 16. PowerShell Standards

PowerShell performs only:

* Bootstrap
* Validation
* Runtime launch

PowerShell must not contain application logic.

Functions should use approved verbs.

Example

```powershell
Initialize-Logger
Start-HermesRuntime
Test-WSL
```

---

# 17. Bash Standards

Bash scripts remain minimal.

Responsibilities

* Environment
* Runtime isolation
* Launch Python

Avoid implementing business logic.

Use:

```bash
set -euo pipefail
```

for production scripts.

All Bash files must use:

* UTF-8 without BOM
* LF line endings

---

# 18. Configuration Files

Configuration uses JSON.

Rules

* Lowercase filenames
* Four-space indentation
* UTF-8
* Human-readable
* Schema validation where practical

---

# 19. Plugin Standards

Each plugin is isolated.

A plugin should not directly manipulate another plugin.

Plugins communicate through Hermes interfaces.

Required files

```text
plugin.py
manifest.json
README.md
```

Optional

```text
tests/
resources/
config.json
```

---

# 20. Provider Standards

Providers expose a common interface.

Required capabilities

* Initialize
* Health Check
* Capability Discovery
* Model Listing
* Inference

Provider-specific implementation details remain internal.

---

# 21. Documentation

Every public module should eventually include:

* Purpose
* Responsibilities
* Dependencies
* Examples
* Limitations

Complex logic requires comments explaining the rationale, not simply restating the code.

---

# 22. Comments

Comments explain *why*, not *what*.

Avoid:

```python
# Increment counter
counter += 1
```

Prefer:

```python
# Retry counter prevents infinite reconnect loops.
counter += 1
```

---

# 23. Dependency Management

Minimize external dependencies.

Before adding a new package:

1. Is it actively maintained?
2. Is it widely used?
3. Can the standard library solve the problem?
4. Is the dependency justified?

---

# 24. Testing

Every new feature should include:

* Unit tests where appropriate
* Integration tests when interacting with external systems
* Manual validation steps documented in TESTING.md

---

# 25. Git Commit Convention

Use Conventional Commits.

Examples

```text
feat: add runtime manager
fix: resolve WSL path conversion
docs: update architecture specification
refactor: simplify provider loading
test: add configuration validation tests
chore: update development dependencies
```

---

# 26. Code Review Checklist

Before merging:

* Builds successfully
* Passes tests
* No duplicated logic
* Documentation updated
* Logging included
* Configuration externalized
* Error handling implemented
* Style checks pass

---

# 27. Forbidden Practices

The following are prohibited unless explicitly justified:

* Circular dependencies
* Global mutable state
* Hardcoded credentials
* Hardcoded filesystem paths
* Wildcard imports
* Silent exception handling
* Copy-paste implementations
* Business logic in PowerShell or Bash

---

# 28. Architecture First

Before implementing significant new functionality:

1. Update PROJECT_SPEC.md if the feature changes project scope.
2. Update ARCHITECTURE.md if component interactions change.
3. Record major architectural decisions in DECISIONS.md or a new ADR.
4. Only then begin implementation.

---

# 29. Continuous Improvement

These standards are intended to evolve with the project.

Changes should improve consistency and maintainability without introducing unnecessary complexity.

When in doubt, choose the solution that makes the codebase easier to understand for the next developer.
