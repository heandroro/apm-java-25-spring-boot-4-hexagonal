---
name: java-operations
description: Observability and containerization for Java 25 + Spring Boot 4 — Micrometer, OpenTelemetry, Prometheus, Dockerfile, Jib, Kubernetes probes
---

# Java Operations

Group skill covering runtime observability and container packaging for Java 25 + Spring Boot 4 applications.

## Overview

This skill bundles two complementary operations sub-domains:

- **`observability/`** — Actuator, Micrometer, Prometheus, OpenTelemetry distributed tracing, structured logging, health probes
- **`container/`** — Dockerfile multi-stage, Jib, Cloud Native Buildpacks, GraalVM Native + Distroless, Kubernetes health probes

## Sub-skills

| Sub-skill | Path | Purpose |
|-----------|------|---------|
| `observability` | `observability/` | Actuator, Micrometer, Prometheus, OpenTelemetry, structured logs, distributed tracing |
| `container` | `container/` | Dockerfile multi-stage, Jib, Buildpacks, GraalVM Distroless, Kubernetes probes |

## Guidelines

### Observability
- Always use `@Observed` + `ObservedAspect` for method-level tracing — not `@Span` directly
- Metrics must carry consistent tags: `application`, `environment`, `region`
- Health indicators must respond in < 1 second
- Use JSON structured logging in production; plain text in local profile
- Propagate trace ID via W3C `traceparent` header on all outbound HTTP calls
- Never expose `env`, `configprops`, or `heapdump` endpoints without authentication

### Container
- Always use non-root user: `addgroup --system app && adduser --system --ingroup app app`
- Prefer multi-stage Dockerfile with layer extraction for optimal build cache
- Use Jib for CI pipelines — no Docker daemon required
- Target image efficiency ≥ 95% (validate with `dive`)
- Health probes: `management.endpoint.health.probes.enabled=true` with separate liveness/readiness groups

## Examples

| File | Sub-skill | Topic |
|------|-----------|-------|
| `observability/examples/ObservabilityExamples.java` | observability | HealthIndicator, custom metrics, `@Observed`, ObservationFilter |
| `container/examples/` | container | Java code examples (none — see assets/ for config templates) |

## Assets

Configuration templates ready to copy into consumer projects:

| File | Sub-skill | Purpose |
|------|-----------|---------|
| `observability/assets/observability-config.yml` | observability | Complete `application.yml` for Actuator, Micrometer, tracing |
| `observability/assets/alerting-rules.yml` | observability | Prometheus scrape config + Alertmanager alert rules |
| `observability/assets/logback-spring.xml` | observability | JSON (prod) and text (local) logging with trace ID |
| `container/assets/Dockerfile-multi-stage` | container | 3-stage build with layer extraction and non-root user |
| `container/assets/Dockerfile-native` | container | GraalVM Native + Distroless (~50MB, startup < 100ms) |
| `container/assets/kubernetes-probes.yml` | container | Spring Boot health probes + K8s deployment + `.dive-ci.yaml` |

## References

| File | Content |
|------|---------|
| `container/references/dockerfile-guide.md` | Multi-stage best practices, Jib, Buildpacks, health probes |

## Build Scripts

| File | Content |
|------|---------|
| `observability/scripts/maven-observability.xml` | Actuator, Micrometer, OpenTelemetry, Logback JSON dependencies |
| `container/scripts/maven-jib.xml` | Jib Maven plugin with ZGC flags and non-root user |
