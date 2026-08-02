---
mode: agent
description: >
  Gera ou atualiza testes para o comportamento selecionado seguindo os
  padroes existentes no projeto.
---

# Generate Tests

Generate or update tests for selected code/behavior.

## Rules

- Follow `[PROJETO]/.github/copilot-instructions.md` and test instructions.
- Inspect nearby tests before creating new ones.
- Reuse existing libraries and patterns.
- Avoid unnecessary stubbing.
- Cover happy path, invalid input, dependency failures, exceptions and boundary conditions.
- Keep test names descriptive.
