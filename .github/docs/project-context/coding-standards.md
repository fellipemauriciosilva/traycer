# Coding Standards: traycer

## Language
TypeScript — strict mode enforced via each package's `tsconfig.json`. No `any` unless absolutely unavoidable and documented.

## Package Manager
Bun 1.3.12 (pinned). Use `bun install`, `bun add`, `bun run`. Do not use `npm` or `yarn`.

## Build
- Run all targets via NX: `bunx nx run <package>:<target>`.
- Type-check: `bun run compile` (never call `tsc` directly).
- Never manually run `compile` / `build` / `lint` / `format` before committing.

## Commits
- All commits require DCO sign-off: `git commit -s` (appends `Signed-off-by:` trailer).
- No enforced commit message format beyond DCO; keep messages descriptive and open a PR with the provided template.
- Pre-commit hook runs affected workspace checks automatically.

## Naming Conventions
- Files: kebab-case (e.g., `host-lifecycle.ts`).
- React hooks: `use-<verb>-<noun>-{mutation,query}.ts` under `hooks/<ns>/`.
- TypeScript types/interfaces: PascalCase.
- Variables/functions: camelCase.

## React / GUI Standards
- All composed `className`s use `cn(...)` from `@/lib/utils` — no template literals, `+`, or `.join(" ")`. Static single strings OK.
- **Fluid layout sizing** — `w-full`, `max-w-*`, viewport caps. No fixed px/rem for layout surfaces.
- Prefer composition over editing `src/components/ui/` (shadcn primitives).
- Loading spinners: use `AgentSpinningDots` only — no new ad-hoc spinners.
- Do not introduce new state management libraries — use Zustand (client state) and TanStack Query (server state).

## Generated Files (Do Not Edit)
- `clients/gui-app/src/routeTree.gen.ts`
- `clients/gui-app/dist/`
- `clients/gui-app/.tanstack/`

## Testing Standards
- Framework: Vitest.
- Test files: `*.spec.ts` or `*.test.ts`.
- React component tests: Vitest + Testing Library.
- Run: `bun run test` or `bunx nx run <package>:test`.
- Tests run in CI, not in pre-commit hook.

## Error Monitoring
- `@sentry/browser` for GUI, `@sentry/node` for CLI, `@sentry/electron` for Desktop.
- Production DSNs are stamped at release time — not committed.

## Protocol Contract Rules
- The `@traycer/protocol` package uses per-method `{ major, minor }` RPC versioning.
- Do NOT change the protocol wire contract without an explicit spec and compatibility analysis.
- The CLI inlines the protocol at build time.

## Security
- Never commit secrets, API keys, trust keys, or credentials.
- Production config values are stamped at CI release time via `scripts/set-deploy-target.cjs`.
- `pre-commit` includes gitleaks (see `.gitleaks.toml`).
