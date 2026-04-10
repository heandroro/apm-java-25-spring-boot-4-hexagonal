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
- Resolves dependencies and updates `apm.yml` with the package reference
- Deploys supported primitives from the package to the native directories your AI tools already watch, such as `.github/`, `.claude/`, `.cursor/`, and `.opencode/`
- Creates or refreshes the lockfile so the installed agent configuration stays reproducible across machines

## Compile for Other Tools

If you use tools beyond **GitHub Copilot**, **Claude**, **Cursor**, and **OpenCode** (which read deployed primitives natively), generate compiled instruction files:

```bash
apm compile
```

This produces:
- **`AGENTS.md`** — for Codex, Gemini
- **`CLAUDE.md`** — for tools that need a single instructions file

> **Note:** Copilot, Claude, Cursor, and OpenCode primarily consume deployed primitives from their native directories after `apm install`. Use `apm compile` when you need generated files for tools that rely on compiled outputs such as `AGENTS.md` or `CLAUDE.md`.

## Day-to-Day Workflow

For a project that consumes this package:

1. Commit `apm.yml` and `apm.lock.yaml` so every contributor gets the same resolved agent configuration.
2. Commit deployed directories such as `.github/`, `.claude/`, `.cursor/`, and `.opencode/` when your team wants agent context to be available immediately after clone.
3. Keep `apm_modules/` out of version control because it is rebuilt from the lockfile during `apm install`.
4. Re-run `apm install` after updating dependencies so deployed primitives and the lockfile stay in sync.

This repository includes a minimal `.gitignore` that follows this workflow by excluding `apm_modules/` and common local pack outputs such as `build/`, `dist/`, `release-artifacts/`, and archived bundles.

## Package Authoring Notes

This repository is the **source package**, so its primitives live under `.apm/` and are meant to be installed into another project with `apm install`.

- Use `.apm/` as the source of truth for agents, instructions, prompts, and skills.
- Treat `AGENTS.md` as generated output from `apm compile`, not a hand-edited source file.
- Expect `apm compile` in this repository to warn that `**/*.java` matches no files, because this package distributes Java guidance but does not contain a Java application itself.

## Distribution Options

If you need to distribute resolved output without requiring APM on the consumer side, use the pack workflow described in the official docs:

```bash
apm install
apm pack --archive
```

This produces a portable bundle of the deployed primitives that can be unpacked or attached to CI and release workflows.

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
