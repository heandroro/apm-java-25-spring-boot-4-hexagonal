---
description: Run a comprehensive code review for Java 25 + Spring Boot 4
---

Review this code applying the following checklist for Java 25 + Spring Boot 4:

## Quality & Style
- [ ] Follows Google Java Style / project Checkstyle rules
- [ ] No SpotBugs, PMD, or Error Prone warnings
- [ ] Cyclomatic complexity ≤ 10 per method
- [ ] Methods ≤ 30 lines, classes ≤ 300 lines

## Java 25 Idioms
- [ ] Uses records for DTOs and value objects
- [ ] Uses sealed interfaces for closed domain types
- [ ] Uses pattern matching in switch expressions
- [ ] Uses Virtual Threads where appropriate (I/O-bound)
- [ ] Uses Structured Concurrency for parallel operations
- [ ] Uses unnamed variables (`_`) for unused bindings

## Spring Boot 4 Patterns
- [ ] Constructor injection only (no field `@Autowired`)
- [ ] `@ConfigurationProperties` with record classes
- [ ] `ProblemDetail` (RFC 9457) for error responses
- [ ] `RestClient` or `@HttpExchange` for HTTP calls
- [ ] Bean Validation on input DTOs

## Architecture
- [ ] Domain layer has no Spring/infrastructure imports
- [ ] Controllers only in `adapter.web` package
- [ ] Repository interfaces in domain, implementations in infrastructure
- [ ] No circular dependencies

## Testing
- [ ] Unit tests exist for all new/modified code
- [ ] Tests follow `should_X_when_Y` naming
- [ ] Integration tests use Testcontainers with fixed image tags
- [ ] Coverage ≥ 80% for modified files

## Security
- [ ] No hardcoded secrets or credentials
- [ ] Input validation on all external data
- [ ] Proper authentication/authorization checks
- [ ] SQL injection and XSS prevention

## Performance
- [ ] No N+1 query problems
- [ ] Appropriate caching for hot paths
- [ ] Connection pool sizing reviewed
- [ ] No blocking calls on Virtual Threads

Provide specific line numbers, severity (critical/warning/info), and suggested fixes for each finding.
