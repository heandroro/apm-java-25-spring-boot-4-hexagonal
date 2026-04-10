# APM — Agent Programming Model for Java 25 + Spring Boot 4

Modular documentation and skill system for AI coding assistants working with Java 25 and Spring Boot 4 projects following hexagonal architecture.

## Overview

This repository contains a structured collection of **skills**, **agents**, **instructions**, and **prompts** that guide AI assistants in generating high-quality, idiomatic code for modern Java applications.

## Structure

```
.apm/
├── agents/           # Specialized AI agents (quality, test, performance, devops)
├── instructions/     # Project-wide coding instructions
├── prompts/          # Reusable prompt templates
└── skills/           # Modular skill packages
    ├── arch-test/        # ArchUnit architecture testing
    ├── best-practices/   # Java 25 idioms, SOLID, Clean Code, MapStruct
    ├── code-quality/     # Checkstyle, SpotBugs, PMD, Error Prone, NullAway
    ├── container/        # Dockerfile, Jib, Buildpacks, GraalVM Native
    ├── integration-test/ # Testcontainers, WireMock, Spring Boot Test
    ├── local-test/       # Docker Compose, Testcontainers Desktop
    ├── observability/    # Actuator, Micrometer, Prometheus, OpenTelemetry
    ├── stress-test/      # Gatling, JMH, k6
    ├── tuning/           # JVM flags, Virtual Threads, caching, pools
    └── unit-test/        # JUnit 6, Mockito 5, AssertJ, Instancio, DataFaker
```

## Skill Format

Each skill follows a consistent structure:

- **`SKILL.md`** — Meta-guide with bundled resources table
- **`examples/`** — Complete, runnable code examples
- **`scripts/`** — Maven/Gradle configuration snippets
- **`references/`** — Concise technical documentation

## Tech Stack

- **Java 25** (with preview features)
- **Spring Boot 4.x** / Spring Framework 7.x
- **Hexagonal Architecture** (Ports & Adapters)
- **Virtual Threads** + Structured Concurrency
- **GraalVM Native Image** support

## APM CLI Setup

Before installing this package, you need the APM CLI.

### Requirements

- macOS, Linux, or Windows (x86_64 or ARM64)
- [git](https://git-scm.com/) for dependency management
- Python 3.10+ (only for pip or from-source installs)

### Quick Install (recommended)

**macOS / Linux:**

```bash
curl -sSL https://aka.ms/apm-unix | sh
```

**Windows (PowerShell):**

```powershell
irm https://aka.ms/apm-windows | iex
```

### Package Managers

**Homebrew (macOS/Linux):**

```bash
brew install microsoft/apm/apm
```

**Scoop (Windows):**

```powershell
scoop bucket add apm https://github.com/microsoft/scoop-apm
scoop install apm
```

**pip:**

```bash
pip install apm-cli   # requires Python 3.10+
```

### Verify Installation

```bash
apm --version
```

For more details, see the [official APM documentation](https://microsoft.github.io/apm/).

---

## Installation

Install in any project using APM CLI:

```bash
apm install heandroro/apm-java-25-spring-boot-4-hexagonal
```

APM automatically:
- Downloads the package to `apm_modules/`
- Copies instructions to `.github/instructions/`
- Copies prompts to `.github/prompts/`
- Updates `apm.yml` with the dependency

## Compile for Other Tools

If you use tools beyond **GitHub Copilot**, **Claude**, **Cursor**, and **OpenCode** (which read deployed primitives natively), generate compiled instruction files:

```bash
apm compile
```

This produces:
- **`AGENTS.md`** — for Codex, Gemini
- **`CLAUDE.md`** — for tools that need a single instructions file

> **Note:** Copilot, Claude, and Cursor users can skip this step. OpenCode users need `apm compile` only if packages include instructions (OpenCode reads `AGENTS.md` for those).

## License

MIT License

Copyright (c) 2026

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
