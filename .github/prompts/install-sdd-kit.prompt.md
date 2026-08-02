---
mode: agent
description: >
  Instala o kit SDD em um projeto do workspace usando os arquivos canonicos
  da pasta .github raiz e atualiza o status geral.
---

# Install SDD Kit

Instala o kit SDD no projeto escolhido e atualiza `.github/sdd-kit-status.md`.

## Step 0 - Scan workspace and refresh registry

1. List top-level directories in workspace root, excluding hidden/system folders.
2. For each directory, mark as `installed` only if both files exist:
   - `[PROJETO]/.github/copilot-instructions.md`
   - `[PROJETO]/.github/AGENTS.md`
3. Rebuild `.github/sdd-kit-status.md` preserving existing install dates whenever possible.
4. Show table and ask which project should receive the kit.

## Step 1 - Analyze selected project

Read minimal evidence from selected `[PROJETO]`:
- `pom.xml` or `*.csproj`
- `README.md`
- `src/main/**` (or equivalent source root)

Detect stack (Java or .NET) and summarize before file creation.

## Step 2 - Create base structure in selected project

Create if missing:

```
[PROJETO]/.github/
  instructions/
  prompts/
  docs/
    architecture/
    project-context/
    specs/_template/
    testing/integration/
    testing/container/
    operations/
```

## Step 3 - Copy canonical kit files

Use workspace root `.github/` as source of truth.
Copy to `[PROJETO]/.github/`:
- `AGENTS.md` (from root template equivalent when available)
- relevant files from `instructions/`
- all files from `prompts/`
- spec templates from `docs/specs/_template/` when available (`task.md`, `spec.md`, `acceptance-criteria.md`, `risks.md`, `decisions.md`, `test-plan.md`)

If a file already exists in target project, merge conservatively and do not erase project-specific rules.

## Step 4 - Generate project-specific context skeleton

Create/update in `[PROJETO]/.github/docs/project-context/`:
- `project-overview.md`
- `current-architecture.md`
- `module-map.md`
- `dependency-map.md`
- `coding-standards.md`
- `business-glossary.md`

Fill only with repository evidence. Unknown values remain `TODO`.

## Step 5 - Update gitignore in target project

Ensure entries exist:

```
### Copilot SDD Kit ###
.github/copilot-instructions.md
.github/AGENTS.md
.github/instructions/
.github/skills/
.github/prompts/
.github/docs/
```

## Step 6 - Finalize and report

1. Mark selected project as installed in `.github/sdd-kit-status.md` with today's date.
2. Report:
- detected stack
- files/directories created
- TODOs needing human review
- next step: `/fill-project-context [PROJETO]`

## Rules

- Do not change production code.
- Do not change test code.
- Do not invent business rules.
- Prefer copying canonical files over duplicating embedded templates.
