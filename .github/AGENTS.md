# Agent Instructions

This repository uses Context Engineering and Spec-Driven Development.

## Mandatory Reading Order
1. `.github/copilot-instructions.md`
2. Relevant files inside `.github/instructions/`
3. `.github/docs/project-context/project-overview.md`
4. `.github/docs/project-context/current-architecture.md`
5. Relevant spec under `.github/docs/specs/`
6. Root-level `AGENTS.md` (project map, commands and non-negotiables)
7. Package-level `AGENTS.md` files when editing a specific client:
   - `clients/gui-app/AGENTS.md`
   - `clients/desktop/AGENTS.md`
8. Existing code near the target implementation
9. Existing tests near the target implementation

## Agent Behavior
- Do not implement before understanding the code.
- Do not invent requirements.
- Do not create broad refactors unless requested.
- Do not change `@traycer/protocol` wire contract unless required by spec.
- Do not change public contracts unless required by spec.
- Always add/update tests for changed behavior.
- **Use `/create-spec` only to scaffold the demand folder** (`TASK-XXXX/`, `BUG-XXXX/`, etc.) with empty template files.
- **Use `/implement-spec` to read context, analyze code, fill `task.md` and implement.** All analysis and development happens here.

## Implementation Flow
`/create-spec` → scaffold folder → `/implement-spec` → read context → analyze code → fill `task.md` → confirm plan → implement → add/update tests → `/review-code` → summarize validation.
