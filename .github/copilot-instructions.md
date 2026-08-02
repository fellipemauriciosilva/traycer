# GitHub Copilot Repository Instructions

## Project Role
You are working as a senior TypeScript/Bun engineer in this repository. Help maintain, evolve, test and document this project while preserving architecture, public contracts (protocol versioning) and open-source contribution guidelines.

**traycer** is an open-source AI orchestration desktop app. It is a **Bun 1.3.12 + NX monorepo** with five packages: `@traycer/protocol` (client⇄host wire contract), `@traycer-clients/traycer-cli` (CLI), `@traycer-clients/shared` (transport/auth), `@traycer-clients/gui-app` (React renderer), and `@traycer-clients/desktop` (Electron shell). The Traycer Host and cloud backends are **not** in this repo — the CLI provisions a signed host from GitHub Releases.

## General Rules
- Do not invent business rules.
- Inspect existing code and nearby tests before suggesting changes.
- Follow the current project style instead of introducing a new one.
- Do not add dependencies unless explicitly requested or technically justified.
- Do not change the `@traycer/protocol` wire contract unless required by a spec — protocol uses per-method `{ major, minor }` versioning negotiated at runtime.
- Do not change public APIs, DTOs or message contracts unless required by a spec.
- Prefer small incremental changes.
- Keep changes focused on the requested task.
- Always consider compatibility, tests, error handling and observability.
- Never add secrets, tokens or credentials to source code.
- All commits require DCO sign-off (`git commit -s`).

## TypeScript Rules
- Use TypeScript strict mode as enforced by each package's `tsconfig.json`.
- Prefer explicit types over `any`.
- Use `bun run compile` (via NX) to type-check; never call `tsc` directly.
- Keep domain logic out of Electron main process and React render layer.
- Use meaningful names and avoid overengineering.

## NX Monorepo Rules
- Always run targets via NX: `bunx nx run <package>:<target>`.
- Never break the `^build` / `^compile` dependency chain defined in `nx.json`.
- Do not call `compile` / `build` / `lint` / `format` manually before committing — `pre-commit` runs affected workspace checks automatically.
- Tests run in CI (`test.yml`), not in the pre-commit hook.

## React / GUI Rules
- Components live in `clients/gui-app/src/`.
- Follow existing component and hook patterns — do not introduce new state management libraries.
- Use Tailwind CSS as already configured; do not add separate CSS files unless required.

## Electron Rules
- Main process code lives in `clients/desktop/src/`.
- Do not blur the boundary between main process and renderer; use IPC bridges as currently established.
- Do not embed secrets or trust keys; production values are stamped at release time by CI.

## Testing Rules
- Always add or update tests for changed behavior.
- Use Vitest with the same conventions already in place (`*.spec.ts`, `*.test.ts`).
- Cover happy path, validation errors, exceptions and edge cases.
- Run tests with: `bun run test` or `bunx nx run <package>:test`.

## Documentation Rules
- Use `/create-spec` to scaffold the demand folder with an empty `task.md`.
- Use `/implement-spec` to analyze, fill `task.md` and implement.
- Update docs under `.github/docs/` when relevant.
- Consult `.github/docs/project-context/` before making architectural decisions.

## Final Response Format
When completing a task, summarize: what was analyzed, what changed, files changed, tests added/updated, risks/assumptions and how to validate.
