---
name: apm-java-25-spring-boot-4-hexagonal
description: APM package for Java 25 and Spring Boot 4 with instructions, prompts, agents, and specialized sub-skills for quality, testing, performance, observability, and containerization.
---

# apm-java-25-spring-boot-4-hexagonal

Package-level guide for using this APM package in Java 25 + Spring Boot 4 projects.

## Overview

This package provides reusable guidance and workflows for modern Java applications built with Spring Boot 4 and hexagonal architecture.

It combines:

- Project-wide Java and Spring instructions
- Reusable review prompts
- Specialized agents for quality, testing, performance, and DevOps concerns
- Sub-skills under `.apm/skills/` that are promoted independently on install

## Sub-skills

Sub-skills are grouped into 4 domain groups. Each group is promoted to a top-level `.github/skills/<name>/` entry on install, with its sub-domains bundled inside.

| Group skill | Bundled sub-domains | Purpose |
|-------------|---------------------|---------|
| `java-quality` | `best-practices`, `code-quality` | Java 25 idioms, SOLID, Clean Code, static analysis, null safety, formatting |
| `java-testing` | `unit-test`, `integration-test`, `arch-test`, `local-test` | Full testing pyramid — unit, integration, architecture, and local environment |
| `java-performance` | `tuning`, `stress-test` | JVM tuning, Virtual Threads, caching, load testing with Gatling/JMH/k6 |
| `java-operations` | `observability`, `container` | Micrometer, OpenTelemetry, Prometheus, Dockerfile, Jib, Kubernetes probes |

## How To Use

1. Install the package with `apm install heandroro/apm-java-25-spring-boot-4-hexagonal` in a consumer project.
2. Let APM deploy the primitives to the tool-native directories such as `.github/`, `.claude/`, `.cursor/`, or `.opencode/`.
3. Use the package-level instructions for general Java and Spring work, and rely on the promoted sub-skills for focused tasks.
4. Use `apm compile` only when you need generated outputs such as `AGENTS.md` or `CLAUDE.md` for tools that depend on compiled files.

## Bundled Resources

- `.apm/instructions/` contains the Java 25 + Spring Boot 4 guidance
- `.apm/prompts/` contains reusable prompt workflows
- `.apm/agents/` contains specialized personas for common engineering domains
- `.apm/skills/` contains focused sub-skills with references, examples, and scripts

## Notes

- This repository is a source package, so `.apm/` is the source of truth.
- `AGENTS.md` is generated output and should be regenerated rather than edited manually.
- The package itself does not contain Java application sources, so compilation may warn that `**/*.java` matches no files in this repository.