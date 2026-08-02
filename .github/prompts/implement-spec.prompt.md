---
mode: agent
description: >
  Implementa o escopo definido na spec para um projeto e ticket especificos,
  com confirmacao antes de codificar.
---

# Implement Spec

Implemente exatamente o escopo definido na spec para `[PROJETO]` e `[TICKET]`.

## Step 1 - Identify project and ticket

If not provided, ask for both.
Spec folder: `[PROJETO]/.github/docs/specs/[TICKET]/`.

## Step 2 - Read project context

Before any code changes, read:
- `[PROJETO]/.github/copilot-instructions.md`
- `[PROJETO]/.github/AGENTS.md`
- `[PROJETO]/.github/docs/project-context/project-overview.md`
- `[PROJETO]/.github/docs/project-context/current-architecture.md`
- `[PROJETO]/.github/docs/project-context/module-map.md`
- Spec files in the ticket folder (`task.md`, `spec.md`, `acceptance-criteria.md`)

## Step 3 - Analyze current code

Based on `task.md` and notes:
- identify entry point
- trace current flow
- identify files to create/modify
- locate existing tests

## Step 4 - Complete `task.md` if needed

Update `[PROJETO]/.github/docs/specs/[TICKET]/task.md` with missing analysis sections:
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

Keep `Decisions Made` empty until implementation decisions happen.

## Step 5 - Confirm before coding

Present to the user:
- scope to implement
- files to create/modify
- tests to add/update
- open questions

If there are blockers, ask before coding. Wait for explicit confirmation.

## Step 6 - Implement

- implement only spec scope
- follow existing architecture/style
- avoid unrelated refactors
- preserve public contracts unless spec requires change
- avoid new dependencies unless required

## Step 7 - Add/update tests

Detect stack and use matching pattern:

Java:
- Unit tests with JUnit 5 + Mockito
- `@WebMvcTest` for isolated controller tests
- `@SpringBootTest` only for integration tests

.NET:
- Unit tests with xUnit + Moq
- No full ASP.NET context in pure unit tests
- Integration tests only when required by scope

Cover happy path, validation, dependency failures and edge cases.

## Step 8 - Update spec status

In `[PROJETO]/.github/docs/specs/[TICKET]/task.md`:
- Status: `analysis` -> `implemented`
- fill `Decisions Made`
- close resolved Open Questions

In `[PROJETO]/.github/docs/specs/[TICKET]/status.md`:

```markdown
| Passo atual | 3 - Implementada |
| Proximo passo | 4 - Documentacao |
| Proximo agent | `/update-documentation [PROJETO] [TICKET]` |
```

Add to history:

```markdown
| 3 | Implementada | `/implement-spec` | [DATA DE HOJE] |
```

## Step 9 - Final summary

Report:
- changed files
- tests added/updated
- risks
- local validation steps
- related spec confirmation

Display:

```
PROXIMO PASSO -> /update-documentation [PROJETO] [TICKET]
```

## Rules

- Do not implement before Step 5 confirmation.
- Do not invent requirements.
- Do not broaden scope beyond spec.
- Always update `task.md` status after implementation.
