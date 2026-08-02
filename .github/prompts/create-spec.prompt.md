---
mode: agent
description: >
  Cria a pasta da demanda e os arquivos base de spec no projeto informado.
  Nao le codigo e nao implementa nada.
---

# Create Spec (workspace)

Cria a estrutura da demanda em `[PROJETO]/.github/docs/specs/[TICKET]/`.

## Passo 1 - Coletar parametros

Se algum item abaixo nao foi informado, pergunte antes de continuar:

| Parametro | Exemplo | Obrigatorio |
|-----------|---------|-------------|
| Projeto | `rest-auditor` | Sim |
| Ticket | `TASK-1234`, `BUG-5678` | Sim |
| Tipo | `feature`, `bugfix`, `task`, `refactor`, `chore` | Nao |
| Descricao curta | uma linha sobre o pedido | Nao |

## Passo 2 - Localizar templates

Templates esperados em:

```
[PROJETO]/.github/docs/specs/_template/
```

Arquivos de template:
- `task.md`
- `spec.md`
- `acceptance-criteria.md`
- `risks.md`
- `decisions.md`
- `test-plan.md`

## Passo 3 - Criar estrutura da demanda

1. Criar pasta `[PROJETO]/.github/docs/specs/[TICKET]/`.
2. Criar subpasta `[PROJETO]/.github/docs/specs/[TICKET]/test-case/`.
3. Criar arquivo `[PROJETO]/.github/docs/specs/[TICKET]/status.md` com:

```markdown
# Status - [TICKET]

| Campo | Valor |
|-------|-------|
| Ticket | [TICKET] |
| Passo atual | 1 - Spec criada |
| Proximo passo | 2 - Analise |
| Proximo agent | `/analyze-spec [PROJETO] [TICKET]` |

## Historico

| # | Passo | Agent | Data |
|---|-------|-------|------|
| 1 | Spec criada | `/create-spec` | [DATA DE HOJE] |
```

4. Copiar templates para a pasta da demanda:
- Obrigatorio: `task.md` (preencher somente Identification)
- Opcional: `spec.md` (somente se houver descricao)
- Opcionais sob demanda explicita: `acceptance-criteria.md`, `risks.md`, `test-plan.md`, `decisions.md`

Para `task.md`, preencher apenas:

```markdown
| Ticket   | [TICKET]       |
| Type     | [TIPO ou TODO] |
| Priority | TODO           |
| Status   | analysis       |
```

Se houver descricao curta, preencher apenas uma linha em **Demand Summary**.

## Passo 4 - Confirmar

Exibir:

```
Spec criada em [PROJETO]/.github/docs/specs/[TICKET]/

Arquivos criados:
- task.md
- status.md
- test-case/

PROXIMO PASSO -> /analyze-spec [PROJETO] [TICKET]
```

## Regras

- Nao ler codigo-fonte do projeto.
- Nao analisar arquitetura, fluxos ou dependencias.
- Nao preencher secoes alem de Identification (e Demand Summary opcional).
- Nao implementar nada.
- Se o projeto nao existir no workspace, avisar e parar.
- Se a pasta `[TICKET]/` ja existir, avisar e nao sobrescrever.
