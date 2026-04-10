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

## Usage

Reference this repository in your AI assistant's context or include the `AGENTS.md` file in your project root.

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
