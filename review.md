# Code Review Guide — Java 25 + Spring Boot 4

Guia completo de code review para projetos usando Java 25 e Spring Boot 4.

---

## Checklist de Review

### 1. Qualidade de código

- [ ] Código segue Google Java Style / Checkstyle configurado
- [ ] Zero warnings de SpotBugs, PMD, Error Prone
- [ ] Complexidade ciclomática ≤ 10 por método
- [ ] Métodos ≤ 30 linhas, classes ≤ 300 linhas
- [ ] Sem código morto, imports não utilizados, ou TODOs sem tracking
- [ ] `@SuppressWarnings` usado apenas com justificativa

### 2. Java 25

- [ ] DTOs e value objects são records (não classes mutáveis)
- [ ] Sealed interfaces para tipos de domínio fechados
- [ ] Pattern matching em switch expressions (sem if/else chains)
- [ ] Virtual Threads para operações I/O-bound
- [ ] Structured Concurrency para operações paralelas
- [ ] Unnamed variables (`_`) para bindings não utilizados
- [ ] Scoped Values em vez de ThreadLocal com Virtual Threads

### 3. Spring Boot 4

- [ ] Constructor injection exclusivamente (sem `@Autowired` em campo)
- [ ] `@ConfigurationProperties` com records imutáveis
- [ ] `ProblemDetail` (RFC 9457) para respostas de erro
- [ ] `RestClient` ou `@HttpExchange` para chamadas HTTP
- [ ] Bean Validation (`jakarta.validation`) nos DTOs de entrada
- [ ] Observability configurada (Micrometer + OpenTelemetry)

### 3. Arquitetura & SOLID

- [ ] Domain layer sem imports de Spring ou infraestrutura
- [ ] Controllers apenas em `adapter.web`
- [ ] Repository interfaces no domain, implementações no infrastructure
- [ ] Sem dependências circulares
- [ ] Testes ArchUnit cobrindo novas regras
- [ ] **Single Responsibility**: classes/métodos com uma única razão para mudar
- [ ] **Open/Closed**: extensível sem modificar código existente
- [ ] **Dependency Inversion**: dependências de abstrações, não implementações

### 3.1. Clean Code

- [ ] Nomes revelam intenção (evitar `process()`, `handle()`)
- [ ] Métodos pequenos (≤ 20 linhas), funções fazem uma única coisa
- [ ] Sem comentários desnecessários — código autoexplicativo
- [ ] Sem argumentos booleanos (flag arguments)
- [ ] Não retornar null — usar `Optional` ou Null Object

### 3.2. Rich Domain Model

- [ ] Entidades possuem comportamento, não apenas getters/setters
- [ ] Regras de negócio encapsuladas no domínio
- [ ] Value Objects para tipos de domínio (`Money`, `Email`, `Cpf`)
- [ ] Validações e invariants no próprio domínio
- [ ] Eventos de domínio para notificar mudanças de estado

### 3.3. MapStruct

- [ ] Mapeamento entre camadas via MapStruct (não manual)
- [ ] Mappers testados com casos edge (nulls, conversões complexas)
- [ ] Value Objects mapeados via métodos customizados `@Named`

### 3.4. Exceções

- [ ] Hierarquia de exceções de domínio (`DomainException` base)
- [ ] `@ControllerAdvice` com tratamento global via `ProblemDetail` (RFC 9457)
- [ ] Error codes únicos e documentáveis (ex: `ORDER_NOT_FOUND`)
- [ ] Exceções incluem contexto rico (IDs, valores relevantes)
- [ ] Não usar exceções para fluxo de controle (use `Optional`, retornos booleanos)
- [ ] Preservar causa original ao wrapar exceções
- [ ] Não expor detalhes técnicos em mensagens ao usuário final
- [ ] Logar no nível correto: WARN para negócio, ERROR para técnico

### 3.5. Null Safety (Programação Defensiva)

- [ ] Campos `final` com inicialização no construtor (imutabilidade)
- [ ] `Objects.requireNonNull()` em construtores para validação
- [ ] `Optional<T>` para retornos potencialmente vazios
- [ ] Nunca `Optional` em parâmetros ou campos
- [ ] Coleções vazias (`List.of()`) ao invés de `null`
- [ ] Null Object Pattern para comportamentos default
- [ ] **JSpecify + NullAway configurados** — null safety em tempo de compilação
- [ ] Pacotes/classes anotados com `@NullMarked` (padrão não-nulo)
- [ ] `@Nullable`/`@NonNull` para documentar contratos de API
- [ ] Bean Validation em entrada de dados (`@NotNull`, `@NotBlank`)
- [ ] Não usar `null` como flag de estado (preferir enum/boolean)
- [ ] Não retornar `null` em vez de `Optional` ou coleção vazia

### 4. Testes

- [ ] Testes unitários para todo código novo/modificado
- [ ] Nomenclatura: `should_[resultado]_when_[condição]`
- [ ] BDDMockito (given/when/then)
- [ ] Testes de integração com Testcontainers (tags fixas)
- [ ] Cobertura ≥ 90% nos arquivos modificados
- [ ] Sem testes flaky ou dependentes de ordem

### 5. Segurança

- [ ] Sem secrets ou credenciais hardcoded
- [ ] Validação de input em todos os dados externos
- [ ] Autenticação e autorização verificadas
- [ ] Proteção contra SQL injection e XSS
- [ ] Dependências sem vulnerabilidades conhecidas (CVEs)

### 6. Performance

- [ ] Sem N+1 queries
- [ ] Caching apropriado para hot paths
- [ ] Pool sizing de conexões revisado
- [ ] Sem chamadas bloqueantes em hot paths com Virtual Threads
- [ ] Queries com índices adequados

### 7. Concorrência e Race Conditions

- [ ] Variáveis compartilhadas entre threads são `Atomic`, `volatile`, ou imutáveis
- [ ] Coleções compartilhadas são thread-safe (`ConcurrentHashMap`, `CopyOnWriteArrayList`)
- [ ] Não há operações `check-then-act` sem sincronização (ex: `if (contains) then get`)
- [ ] Não há `synchronized` em métodos longos — usar `ReentrantLock` com seção crítica mínima
- [ ] Entidades JPA não são compartilhadas entre threads
- [ ] Singleton thread-safe (enum ou `synchronized` correto com `volatile`)
- [ ] Preferir imutabilidade — `record`, `List.copyOf()`, objetos defensivamente copiados
- [ ] Testes de concorrência existem para código multi-thread

### 8. Container e deploy

- [ ] Dockerfile multi-stage com non-root user
- [ ] Health probes (liveness + readiness) configuradas
- [ ] JVM flags adequados para container
- [ ] `.dockerignore` atualizado
- [ ] Resource limits definidos

---

## Severidades

| Nível | Descrição | Ação |
|---|---|---|
| **🔴 Critical** | Bug, vulnerabilidade, ou violação arquitetural | Bloqueia merge |
| **🟡 Warning** | Melhoria importante de qualidade ou performance | Deve ser corrigido antes do merge |
| **🔵 Info** | Sugestão de melhoria, refactoring opcional | Pode ser tratado em PR futuro |

---

## Processo de Review

1. **Autor** — executa análise estática e testes localmente antes de abrir PR
2. **CI** — roda quality gates automaticamente (Checkstyle, SpotBugs, JaCoCo, ArchUnit)
3. **Reviewer** — aplica este checklist, focando em itens não cobertos pela automação
4. **Aprovação** — mínimo 1 aprovação; PRs com mudanças arquiteturais requerem 2
5. **Merge** — squash merge na branch principal

---

## Critérios de aprovação

- Zero findings **Critical**
- Zero findings **Warning** não justificados
- Testes passando no CI
- Quality gate aprovado no SonarQube/SonarCloud
- Cobertura ≥ 90% nos arquivos modificados
