---
mode: agent
description: >
  Le o codigo do projeto e preenche os docs de contexto de forma cirurgica,
  sem alterar codigo de producao.
---

# Fill Project Context

Preencha os docs de contexto em `[PROJETO]/.github/docs/project-context/` com base no codigo-fonte.

## Passo 1 - Identificar projeto

Se o projeto nao foi informado, perguntar antes de continuar.

## Passo 2 - Ler docs existentes

Ler:
- `[PROJETO]/.github/docs/project-context/project-overview.md`
- `[PROJETO]/.github/docs/project-context/current-architecture.md`
- `[PROJETO]/.github/docs/project-context/module-map.md`
- `[PROJETO]/.github/docs/project-context/dependency-map.md`
- `[PROJETO]/.github/docs/project-context/coding-standards.md`
- `[PROJETO]/.github/docs/project-context/business-glossary.md`

Mapear lacunas: TODO, celulas vazias, secoes ausentes.

## Passo 3 - Discovery no codigo

Detectar stack:
- Java: existe `pom.xml` e `src/main/java`
- .NET: existem `*.csproj` e `Program.cs`

Se Java, ler principalmente:
- `[PROJETO]/pom.xml`
- `[PROJETO]/src/main/java/**/controller/**/*.java`
- `[PROJETO]/src/main/java/**/service/**/*.java`
- `[PROJETO]/src/main/java/**/repository/**/*.java`
- `[PROJETO]/src/main/java/**/client/**/*.java`
- `[PROJETO]/src/main/resources/application*.yml`

Se .NET, ler principalmente:
- `[PROJETO]/**/*.csproj`
- `[PROJETO]/**/Program.cs`
- `[PROJETO]/**/Controllers/**/*.cs`
- `[PROJETO]/**/Services/**/*.cs`
- `[PROJETO]/**/Repository/**/*.cs`
- `[PROJETO]/**/Clients/**/*.cs`
- `[PROJETO]/**/appsettings*.json`

## Passo 4 - Mostrar plano de preenchimento

Antes de editar, apresentar gaps por arquivo/secoes e aguardar confirmacao do usuario.

## Passo 5 - Preencher docs

- Editar apenas trechos necessarios.
- Preservar formato existente.
- Trocar TODO por evidencias reais.
- Se valor nao estiver configurado no codigo, manter `-` e comentar `<!-- nao configurado -->`.

Ordem sugerida:
1. `project-overview.md`
2. `current-architecture.md`
3. `module-map.md`
4. `dependency-map.md`
5. `coding-standards.md`
6. `business-glossary.md`

## Passo 6 - Atualizar prompt de discovery

Se faltar no final de `[PROJETO]/.github/prompts/analyze-project.prompt.md`, adicionar:

```markdown
## Apos o discovery

Se os docs de contexto ainda estiverem incompletos, execute:

`/fill-project-context [PROJETO]`
```

## Regras

- Nunca reescrever doc inteiro.
- Nunca inventar informacao.
- Nunca alterar codigo de producao ou testes.
- Criar docs faltantes apenas se forem os 6 docs padrao acima.
