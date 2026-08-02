---
mode: agent
description: >
  Atualiza docs de contexto apos implementacao com base no task.md da demanda,
  sem alterar codigo de producao.
---

# Update Documentation

Atualize docs de contexto com base no que foi implementado para `[PROJETO]` e `[TICKET]`.

## Passo 1 - Identificar projeto e ticket

Se faltarem parametros, pergunte ao usuario.
Pasta da spec: `[PROJETO]/.github/docs/specs/[TICKET]/`.

## Passo 2 - Ler spec da demanda

Ler obrigatoriamente:
- `[PROJETO]/.github/docs/specs/[TICKET]/task.md`
  - Affected Files
  - Implementation Plan
  - Decisions Made

## Passo 3 - Ler docs de contexto atuais

Ler:
- `[PROJETO]/.github/docs/project-context/project-overview.md`
- `[PROJETO]/.github/docs/project-context/current-architecture.md`
- `[PROJETO]/.github/docs/project-context/module-map.md`
- `[PROJETO]/.github/docs/project-context/dependency-map.md`

## Passo 4 - Mapear mudancas documentais

Comparar implementacao x documentacao e listar o que sera atualizado.
Aguardar confirmacao do usuario antes de editar.

## Passo 5 - Editar apenas trechos afetados

- Nao reescrever docs inteiros.
- Preservar formato existente.
- Nao adicionar TODO novo onde nao existia.
- Documentar contratos, fluxos e estrutura; evitar detalhes internos de codigo.

## Passo 6 - Atualizar status da demanda

Se `task.md` estiver com `implemented`, mudar para `documented`.

Atualizar `[PROJETO]/.github/docs/specs/[TICKET]/status.md`:

```markdown
| Passo atual | 4 - Documentada |
| Proximo passo | 5 - Validacao local + Revisao |
| Proximo agent | `/generate-integration-tests` (opcional) depois `/review-code` |
```

Adicionar historico:

```markdown
| 4 | Documentada | `/update-documentation` | [DATA DE HOJE] |
```

Exibir:

```
PROXIMO PASSO -> Validar localmente
Opcional -> /generate-integration-tests [PROJETO] [TICKET]
Depois -> /review-code [PROJETO]
```

## Regras

- Nunca alterar codigo de producao ou testes.
- Nunca inventar informacoes.
- Basear-se em `task.md` e no codigo existente.
