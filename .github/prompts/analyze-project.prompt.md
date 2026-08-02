---
mode: agent
description: >
  Analisa um projeto Java ou .NET sem alterar codigo e devolve um resumo
  arquitetural com riscos, lacunas e proximos passos.
---

# Analyze Project

Analise o projeto `[PROJETO]` sem modificar codigo.

## Passo 1 - Identificar projeto

Se `[PROJETO]` nao foi informado, pergunte ao usuario.

## Passo 2 - Detectar stack

Detectar pelo repositorio:
- Java: `pom.xml` + `src/main/java`
- .NET: `*.csproj` + `Program.cs`

## Passo 3 - Ler contexto e codigo

Ler sempre:
- `[PROJETO]/.github/copilot-instructions.md` (se existir)
- `[PROJETO]/.github/AGENTS.md` (se existir)
- `[PROJETO]/README.md` (se existir)

Se Java, ler adicionalmente:
- `[PROJETO]/pom.xml`
- `[PROJETO]/src/main/java/**`
- `[PROJETO]/src/main/resources/application*.yml`

Se .NET, ler adicionalmente:
- `[PROJETO]/**/*.csproj`
- `[PROJETO]/**/Program.cs`
- `[PROJETO]/**/Controllers/**/*.cs`
- `[PROJETO]/**/Services/**/*.cs`
- `[PROJETO]/**/Repository/**/*.cs`
- `[PROJETO]/**/appsettings*.json`

## Passo 4 - Entregar resumo

Retornar:
- resumo do projeto e objetivo tecnico
- stack e versoes principais
- estrutura de modulos/pacotes
- pontos de entrada
- integracoes externas e dependencias
- estrategia de testes observada
- riscos e incognitas

## Passo 5 - Proximo passo de contexto

Se docs em `[PROJETO]/.github/docs/project-context/` estiverem incompletos, orientar:

```text
/fill-project-context [PROJETO]
```

## Passo 6 - Oferecer geracao de integracao

Perguntar ao usuario:

- Para Java: gerar suite com Cucumber + WireMock + Testcontainers?
- Para .NET: gerar suite com xUnit + WireMock.Net + WebApplicationFactory?

Se confirmar, executar `/generate-integration-tests [PROJETO] [TICKET-opcional]`.
