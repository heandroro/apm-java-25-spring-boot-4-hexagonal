---
name: java-spring-boot
description: "Use when working on Java 25 and Spring Boot 4 code, especially for hexagonal architecture, Spring conventions, DTO design, validation, logging, and testing expectations."
applyTo: "**/*.java"
---

# Java 25 + Spring Boot 4 Instructions

## Language & Framework

- Java 25 with preview features enabled
- Spring Boot 4.x with Spring Framework 7.x
- Jakarta EE 11 APIs (jakarta.* namespace)

## Code Style

- Follow Google Java Style Guide
- Use records for all DTOs, value objects, and configuration properties
- Use sealed interfaces/classes for closed type hierarchies
- Use pattern matching with switch expressions
- Use Virtual Threads for I/O-bound operations
- Use Structured Concurrency (`StructuredTaskScope`) for parallel tasks
- Prefer `var` for local variables when type is obvious

## Spring Conventions

- Constructor injection only — never use `@Autowired` on fields
- `@ConfigurationProperties` bound to record classes
- Error handling via `ProblemDetail` (RFC 9457)
- HTTP clients via `RestClient` or `@HttpExchange` interfaces
- Observability via Micrometer + OpenTelemetry
- Virtual Threads enabled: `spring.threads.virtual.enabled=true`
- **`@Bean`** apenas para objetos transversais ou de infraestrutura, encoders, clients e factories.

## Architecture

- Hexagonal / Ports & Adapters architecture
- Domain layer: entities, value objects, repository interfaces, domain services — no framework dependencies
- Application layer: use cases, ports, DTOs
- Infrastructure layer: persistence, HTTP clients, messaging, configuration
- Adapter layer: REST controllers, JPA implementations, message listeners

## Testing

- JUnit 6 + Mockito 5 + AssertJ for unit tests
- Testcontainers + WireMock for integration tests
- ArchUnit for architecture validation
- JaCoCo coverage ≥ 80%
- Test naming: `should_[result]_when_[condition]`

## Null Safety

- Use `Optional<T>` for return types that may be absent
- Never use `Optional` as parameter or field type
- Use `@Nullable` / `@NonNull` annotations from Spring framework
- Validate inputs at entry points with Bean Validation

## Logging

- SLF4J with Logback
- Structured logging with MDC context
- Never use `System.out` or `System.err`
- Log levels: ERROR for failures, WARN for degraded, INFO for business events, DEBUG for troubleshooting
