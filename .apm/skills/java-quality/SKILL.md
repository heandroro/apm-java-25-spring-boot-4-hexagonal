---
name: java-quality
description: Code quality and best practices for Java 25 + Spring Boot 4 — SOLID, Clean Code, static analysis, null safety, and formatting
---

# Java Quality

Group skill covering coding standards and automated quality enforcement for Java 25 + Spring Boot 4 projects.

## Overview

This skill bundles two complementary sub-domains:

- **`best-practices/`** — Java 25 idioms, SOLID, Clean Code, Rich Domain Modeling, MapStruct, Streams, Virtual Threads, JSpecify
- **`code-quality/`** — Static analysis with Checkstyle, SpotBugs, PMD, Error Prone, NullAway, SonarQube, Google Java Format

## Sub-skills

| Sub-skill | Path | Purpose |
|-----------|------|---------|
| `best-practices` | `best-practices/` | Java 25 idioms, SOLID, Clean Code, Rich Domain, MapStruct, Streams, Virtual Threads, JSpecify |
| `code-quality` | `code-quality/` | Checkstyle, SpotBugs, PMD, Error Prone, NullAway, SonarQube, Google Java Format |

## Guidelines

- Use **records** for DTOs and value objects; use **classes** only for JPA entities and aggregates with mutable state
- Apply **sealed interfaces** for closed type hierarchies; use **pattern matching** for exhaustive branching
- Enforce **constructor injection** only — never `@Autowired` on fields
- Prefer **component scan** over manual `@Bean` registration for Spring-managed use cases
- Run static analysis on every PR; block merge on quality gate failure
- Quality gate thresholds: zero critical bugs, zero vulnerabilities, coverage ≥ 80%, duplication ≤ 3%

## Examples

See `best-practices/examples/` for complete, runnable Java 25 code covering:

| File | Topic |
|------|-------|
| `RecordsAndSealed.java` | Records, sealed classes, pattern matching |
| `SolidPrinciples.java` | SOLID in practice |
| `CleanCode.java` | Before/after refactoring examples |
| `RichDomainModel.java` | Anemic vs rich domain |
| `VirtualThreads.java` | Virtual Threads and Structured Concurrency |
| `StreamsExamples.java` | Stream API best and worst practices |
| `ExceptionsExamples.java` | DomainException hierarchy and anti-patterns |

## References

| File | Content |
|------|---------|
| `best-practices/references/solid-principles.md` | Detailed SOLID guide |
| `best-practices/references/clean-code-guide.md` | Clean code manual |
| `best-practices/references/rich-domain-guide.md` | Rich domain modeling |
| `best-practices/references/record-vs-class-guide.md` | When to use Record vs Class |
| `best-practices/references/jspecify-nullaway.md` | Null safety at compile time |
| `best-practices/references/mapstruct-guide.md` | MapStruct advanced usage |
| `best-practices/references/threads-concurrency-guide.md` | Concurrency with Virtual Threads |
| `code-quality/references/quality-rules.md` | Quality gates, tools configuration |

## Build Scripts

| File | Content |
|------|---------|
| `best-practices/scripts/maven-dependencies.xml` | Maven snippets (JSpecify, NullAway, MapStruct) |
| `best-practices/scripts/gradle-dependencies.gradle` | Gradle plugins and dependencies |
| `code-quality/scripts/maven-quality.xml` | Checkstyle, SpotBugs, PMD, Error Prone for Maven |
| `code-quality/scripts/gradle-quality.gradle` | Same toolchain for Gradle |
