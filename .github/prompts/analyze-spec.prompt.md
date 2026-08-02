---
mode: agent
description: >
  Le documentos da demanda, analisa o codigo existente e completa a spec
  sem escrever codigo de producao.
---

# Analyze Spec

Leia a documentacao da demanda, analise o codigo e complete os arquivos da spec antes de implementar.

## Passo 1 - Identificar projeto e ticket

Se nao foram informados, pergunte ao usuario.
A pasta da demanda fica em `[PROJETO]/.github/docs/specs/[TICKET]/`.

Liste os arquivos da pasta antes de iniciar.

## Passo 2 - Ler contexto do projeto

Leia nesta ordem:
1. `[PROJETO]/.github/copilot-instructions.md`
2. `[PROJETO]/.github/docs/project-context/project-overview.md`
3. `[PROJETO]/.github/docs/project-context/current-architecture.md`
4. `[PROJETO]/.github/docs/project-context/module-map.md`
5. `[PROJETO]/.github/docs/project-context/dependency-map.md`

## Passo 3 - Ler documentos da demanda

Leia todos os arquivos em `[PROJETO]/.github/docs/specs/[TICKET]/`:
- `task.md`
- `spec.md`
- `acceptance-criteria.md`
- `risks.md`
- `test-plan.md`
- `decisions.md`
- qualquer outro `.md`, `.txt`, `.pdf` ou `.docx`

Se houver `.docx`, usar skill `doc-reader`.
Se houver `.pdf`, usar skill `pdf-reader`.

## Passo 4 - Analisar codigo

Com base nos documentos:
1. Identificar ponto de entrada (REST, consumer, scheduler, etc.).
2. Trazer fluxo atual de Controller -> Service -> Repository/Client.
3. Listar arquivos afetados (create/modify/delete).
4. Localizar testes existentes proximos.
5. Identificar dependencias afetadas.
6. Verificar feature flags.
7. Verificar contratos publicos que nao podem quebrar.

## Passo 5 - Completar `task.md`

Atualizar `[PROJETO]/.github/docs/specs/[TICKET]/task.md` preenchendo:
- Demand Summary
- Current Behavior
- Expected Behavior
- Affected Files
- Entry Point
- Flow Analysis
- Implementation Plan
- Tests to Add/Update
- Risks and Assumptions
- Open Questions

Em `Status`, trocar `analysis` para `ready-for-implementation`.
Nao preencher `Decisions Made` neste passo.

## Passo 6 - Atualizar outros docs da spec

- `spec.md`: completar Context, Problem, Goal, Business Rules, Affected Areas.
- `acceptance-criteria.md`: criar AC-001, AC-002... mensuraveis.
- `risks.md`: listar impacto, probabilidade e mitigacao.
- `test-plan.md`: atualizar cenarios unitarios e edge cases.

## Passo 7 - Resumo para usuario

Apresentar:
- Escopo em 1 frase.
- Arquivos a criar/alterar/remover.
- Testes a adicionar/atualizar.
- Riscos.
- Questoes em aberto.

Se houver bloqueio real, pedir esclarecimento antes de finalizar.

## Passo 8 - Atualizar `status.md`

Atualizar `[PROJETO]/.github/docs/specs/[TICKET]/status.md`:

```markdown
| Passo atual | 2 - Analisada |
| Proximo passo | 3 - Implementacao |
| Proximo agent | `/implement-spec [PROJETO] [TICKET]` |
```

Adicionar ao historico:

```markdown
| 2 | Analisada | `/analyze-spec` | [DATA DE HOJE] |
```

Exibir:

```
PROXIMO PASSO -> /implement-spec [PROJETO] [TICKET]
```

## Regras

- Nao escrever codigo de producao.
- Nao alterar arquivos fora de `[PROJETO]/.github/docs/specs/[TICKET]/`.
- Basear tudo em evidencias do codigo e dos docs.
- Se faltar dado, manter TODO e registrar Open Question.
- Preservar conteudo ja preenchido; apenas complementar.
