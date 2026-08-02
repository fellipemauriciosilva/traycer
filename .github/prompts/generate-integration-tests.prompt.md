---
mode: agent
description: >
  Gera ou atualiza testes de integracao para Java ou .NET com base no stack
  detectado e no escopo do ticket.
---

# Generate Integration Tests

Gerar ou atualizar a suite de integracao para `[PROJETO]`.

## Passo 1 - Identificar projeto e ticket

Se `[PROJETO]` nao foi informado, perguntar.
`[TICKET]` e opcional, mas recomendado para modo incremental.

## Passo 2 - Detectar stack

- Java: `pom.xml` + `src/main/java`
- .NET: `*.csproj` + `Program.cs`

## Passo 3 - Ler contexto

Ler:
- `[PROJETO]/.github/copilot-instructions.md` (se existir)
- `[PROJETO]/.github/docs/project-context/current-architecture.md` (se existir)
- `[PROJETO]/.github/docs/project-context/dependency-map.md` (se existir)
- `[PROJETO]/.github/docs/testing/testing-strategy.md` (se existir)
- `[PROJETO]/.github/docs/testing/integration/coverage-map.md` (se existir)

Se `[TICKET]` informado, ler:
- `[PROJETO]/.github/docs/specs/[TICKET]/task.md`
- arquivos de `[PROJETO]/.github/docs/specs/[TICKET]/test-case/` (se existirem)

## Passo 4 - Escolher estrategia

- Sem `coverage-map.md`: discovery completo
- Com `coverage-map.md`: atualizar apenas fluxos do ticket e gaps `not covered`

## Passo 5 - Gerar artefatos por stack

### Java

Estrutura alvo preferencial:
- `[PROJETO]/test/pom.xml`
- `[PROJETO]/test/integration/**`
- `[PROJETO]/test/container/**`

Stack:
- Cucumber + JUnit Platform
- WireMock
- Testcontainers

Regras:
- Nao alterar codigo de producao
- Nao acoplar suite no build principal sem pedido explicito
- Usar sufixos `*IT.java` e `*ContainerTest.java`

### .NET

Estrutura alvo:
- `[PROJETO]/.github/docs/testing/integration/`
- `[PROJETO]/.github/docs/testing/container/docker-compose.test.yml`

Stack:
- xUnit
- WireMock.Net
- WebApplicationFactory

Regras:
- Nao alterar codigo de producao
- Nao alterar projeto de testes principal sem pedido explicito

## Passo 6 - Atualizar coverage-map

Criar/atualizar:
- `[PROJETO]/.github/docs/testing/integration/coverage-map.md`

Registrar coberto x nao coberto por endpoint/consumer/client.

## Passo 7 - Entregar execucao local

Java (exemplo):
```bash
cd [PROJETO]/test
mvn test
```

.NET (exemplo):
```bash
docker-compose -f [PROJETO]/.github/docs/testing/container/docker-compose.test.yml up -d
dotnet test [PROJETO]/.github/docs/testing/integration/IntegrationTests.csproj
```

## Regras gerais

- Basear cenarios em evidencia real do codigo/spec.
- Evitar duplicar cenarios ja cobertos.
- Usar idioma do dominio (pt-BR quando aplicavel).
