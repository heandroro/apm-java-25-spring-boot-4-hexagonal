---
name: java-performance
description: Performance tuning and load testing for Java 25 + Spring Boot 4 — JVM flags, Virtual Threads, Gatling, JMH, k6
---

# Java Performance

Group skill covering performance engineering for Java 25 + Spring Boot 4 applications.

## Overview

This skill bundles two complementary performance sub-domains:

- **`tuning/`** — JVM flags, GraalVM Native Image, Virtual Threads, HikariCP sizing, Caffeine, Redis caching, JFR profiling
- **`stress-test/`** — Load testing with Gatling 4, JMH microbenchmarks, k6, SLA threshold enforcement

## Sub-skills

| Sub-skill | Path | Purpose |
|-----------|------|---------|
| `tuning` | `tuning/` | JVM flags, GraalVM Native, Virtual Threads, caching, connection pools, profiling |
| `stress-test` | `stress-test/` | Gatling 4, JMH microbenchmarks, k6, SLA assertions |

## Guidelines

### JVM
- Use `-XX:+UseZGC -XX:+ZGenerational` for low-latency production workloads
- Set `-Xms` = `-Xmx` in containers to prevent heap resizing
- Use `-XX:MaxRAMPercentage=75.0` — reserve 25% for off-heap (metaspace, thread stacks, NIO)
- Enable `spring.threads.virtual.enabled=true`; avoid `synchronized` blocks with Virtual Threads — use `ReentrantLock`
- Profile with JFR in production (`-XX:+FlightRecorder`) — overhead < 1%

### Caching and pools
- Size HikariCP with: `pool_size = (core_count × 2) + effective_spindle_count`
- Set `max-lifetime=1800000` (30 min) to recycle connections before database timeout
- Use Caffeine for local cache; Redis for distributed — always set TTL

### Load testing
- Always test: smoke → load → stress → soak → spike scenarios
- SLA thresholds: p99 ≤ 500ms, error rate ≤ 0.1%, throughput ≥ 1000 req/s (adjust per endpoint)
- Run stress tests in dedicated environment, not standard CI
- Archive Gatling HTML reports as CI artifacts

## Examples

| File | Sub-skill | Topic |
|------|-----------|-------|
| `stress-test/examples/OrderSimulation.java` | stress-test | Gatling 4 ramp-up scenarios, SLA assertions, multi-scenario |
| `stress-test/examples/SerializationBenchmark.java` | stress-test | JMH with `@Param`, `Blackhole`, `@State(Scope.Benchmark)` |

## References

| File | Content |
|------|---------|
| `tuning/references/tuning-guide.md` | JVM flags, Virtual Threads, web servers, HikariCP, Caffeine, Redis, JFR |
