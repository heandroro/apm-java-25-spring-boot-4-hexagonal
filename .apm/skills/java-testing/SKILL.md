---
name: java-testing
description: Full testing strategy for Java 25 + Spring Boot 4 — unit, integration, architecture, and local environment testing
---

# Java Testing

Group skill covering the full testing pyramid for Java 25 + Spring Boot 4 hexagonal architecture projects.

## Overview

This skill bundles four complementary testing layers:

- **`unit-test/`** — JUnit 6, Mockito 5, AssertJ, JaCoCo ≥ 90%, Instancio, DataFaker
- **`integration-test/`** — Testcontainers, WireMock, Spring Boot Test, REST Assured, WebTestClient
- **`arch-test/`** — ArchUnit architecture rules for hexagonal layers and dependency enforcement
- **`local-test/`** — Docker Compose, Testcontainers Desktop, Spring Profiles, Spring Boot DevTools

## Sub-skills

| Sub-skill | Path | Purpose |
|-----------|------|---------|
| `unit-test` | `unit-test/` | JUnit 6, Mockito 5, AssertJ, JaCoCo ≥ 90%, Instancio, DataFaker |
| `integration-test` | `integration-test/` | Testcontainers, WireMock, Spring Boot Test, REST Assured, WebTestClient |
| `arch-test` | `arch-test/` | ArchUnit rules for hexagonal layers and dependency enforcement |
| `local-test` | `local-test/` | Docker Compose, Testcontainers Desktop, Spring Profiles, DevTools |

## Guidelines

- Test naming: `should_[resultado]_when_[condição]`
- Unit tests: no network, no database, no filesystem — strict isolation with Mockito
- Use `BDDMockito` (`given/when/then`) over raw `Mockito.when`
- Include the global `@RestControllerAdvice` in every `MockMvcBuilders` setup so `ProblemDetail` error mapping is exercised
- Use `@ServiceConnection` and `@Container` static for shared Testcontainers between tests
- Architecture tests run alongside unit tests in CI; block merge on failure
- Use `.withReuse(true)` on containers during local development for faster feedback
- Containers must use pinned image tags — never `latest`

## Examples

| File | Sub-skill | Topic |
|------|-----------|-------|
| `unit-test/examples/OrderServiceTest.java` | unit-test | JUnit 6 + Mockito + AssertJ, BDDMockito, Instancio, DataFaker, `@Nested` |
| `integration-test/examples/IntegrationTestExamples.java` | integration-test | `@SpringBootTest`, Testcontainers, WireMock, `@ServiceConnection`, MockMvc |
| `arch-test/examples/ArchitectureTest.java` | arch-test | ArchUnit: layer rules, class location, cycle detection |
| `local-test/examples/TestcontainersConfig.java` | local-test | `@TestConfiguration` with reusable postgres/redis/kafka, `TestApplication` |

## References

| File | Content |
|------|---------|
| `unit-test/references/testing-guide.md` | BDD naming, coverage, Instancio, DataFaker, fixtures |

## Build Scripts

| File | Content |
|------|---------|
| `unit-test/scripts/maven-jacoco.xml` | JaCoCo with 90% line and branch threshold |
