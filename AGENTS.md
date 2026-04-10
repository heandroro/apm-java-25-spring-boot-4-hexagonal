# AGENTS.md — Java 25 + Spring Boot 4

This file is the compiled agent instructions for tools that read a single `AGENTS.md` file (Codex, Gemini).
For tools that support native APM primitives (Copilot, Claude, Cursor), use `apm install` instead.

---

## Project Context

- **Language**: Java 25 (with preview features)
- **Framework**: Spring Boot 4.x / Spring Framework 7.x
- **Architecture**: Hexagonal (Ports & Adapters)
- **Build**: Maven or Gradle with Java 25 toolchain
- **Testing**: JUnit 6, Mockito 5, Testcontainers, ArchUnit

---

## Code Standards

### Java 25 Idioms
- Use **records** for DTOs, value objects, and `@ConfigurationProperties`
- Use **sealed interfaces** to model closed domain types
- Use **pattern matching** in switch expressions for business logic
- Use **Virtual Threads** for I/O-bound workloads (`spring.threads.virtual.enabled=true`)
- Use **Structured Concurrency** (`StructuredTaskScope`) for parallel operations
- Use **unnamed variables** (`_`) for unused bindings in lambdas and catches
- Use **Scoped Values** instead of `ThreadLocal` with Virtual Threads

### Spring Boot 4 Patterns
- **Constructor injection** only — never `@Autowired` on fields
- **`@ConfigurationProperties`** bound to immutable records
- **`ProblemDetail`** (RFC 9457) for all error responses
- **`RestClient`** or **`@HttpExchange`** for HTTP calls (not `RestTemplate`)
- **Bean Validation** (`jakarta.validation`) on all input DTOs
- **Observability**: Micrometer + OpenTelemetry for traces, metrics, correlated logs

### Architecture Rules
- **Domain** (`..domain..`): entities, value objects, repository interfaces — no Spring imports
- **Application** (`..application..`): use cases, ports, DTOs — depends only on domain
- **Infrastructure** (`..infrastructure..`): JPA implementations, HTTP clients, config
- **Adapter** (`..adapter.web..`): REST controllers, request/response mappers
- No circular dependencies between layers
- ArchUnit tests enforce all architecture rules

---

## Quality Gates

| Metric | Threshold |
|---|---|
| Line coverage (JaCoCo) | ≥ 90% |
| Branch coverage | ≥ 90% |
| Cyclomatic complexity | ≤ 10 per method |
| Code duplication | ≤ 3% |
| Bugs / Vulnerabilities | 0 critical |

---

## Testing Strategy

### Unit Tests
- **JUnit 6** + **Mockito 5** + **AssertJ**
- Naming: `should_[result]_when_[condition]`
- BDDMockito style: `given()` / `then()`
- One logical assertion per test
- `@Nested` for scenario grouping

### Integration Tests
- **Testcontainers** for databases, Redis, Kafka
- **WireMock** for external HTTP APIs
- `@Tag("integration")` for separate CI stage
- `@ServiceConnection` for container property injection
- Fixed image tags (never `latest`)

### Architecture Tests
- **ArchUnit** rules for hexagonal architecture
- Domain must not depend on infrastructure
- Controllers only in `adapter.web`
- Run with unit tests in CI

### Stress Tests
- **Gatling 4** or **k6** for load testing
- SLA: p99 ≤ 500ms, throughput ≥ 1000 req/s, error rate ≤ 0.1%
- **JMH** for microbenchmarks
- Run in dedicated environment before releases

---

## Container & Deployment

- **Multi-stage Dockerfile** with layered JARs or **Jib** for Dockerless builds
- Base image: `eclipse-temurin:25-jre` (JVM) or `distroless` (native)
- Non-root user mandatory
- Health probes: `/actuator/health/liveness` + `/actuator/health/readiness`
- JVM flags: `-XX:+UseZGC -XX:+ZGenerational -XX:MaxRAMPercentage=75.0`
- Image tags: `semver-gitsha` (e.g., `1.0.0-abc1234`)

---

## Performance Tuning

- ZGC Generational as default GC
- Fixed heap in containers (`-Xms` = `-Xmx`)
- Virtual Threads enabled by default
- Caching: Caffeine (local) + Redis (distributed)
- HikariCP pool sizing based on load testing
- JFR enabled in production for continuous profiling
- Monitor: GC pauses, allocation rate, thread count, p99 latency

---

## Agents

This project includes 4 specialized agents:

1. **Quality Agent** — code quality, static analysis, Java 25 idioms, Spring Boot 4 best practices
2. **Test Agent** — testing strategy, coverage, test quality, architecture validation
3. **Performance Agent** — JVM tuning, load testing, caching, Virtual Threads optimization
4. **DevOps Agent** — containerization, CI/CD pipelines, Kubernetes deployment, image security, observability

## Skills

This package includes 10 specialized skills:

- **code-quality** — Checkstyle, SpotBugs, PMD, SonarQube, Error Prone, NullAway
- **unit-test** — JUnit 6, Mockito 5, AssertJ, JaCoCo (≥ 90% coverage)
- **integration-test** — Testcontainers, WireMock, Spring Boot Test
- **stress-test** — Gatling 4, JMH, k6, load testing SLAs
- **arch-test** — ArchUnit, hexagonal architecture rules
- **local-test** — Docker Compose, Testcontainers Desktop, Spring profiles
- **Best Practices** — Java 25 idioms (records, sealed, pattern matching), SOLID, Clean Code, Rich Domain Model, MapStruct, JSpecify, NullAway
- **tuning** — JVM flags, Virtual Threads, caching, connection pools
- **container** — Dockerfile, Jib, Buildpacks, GraalVM Native
- **observability** — Actuator, Micrometer, Prometheus, OpenTelemetry, tracing
