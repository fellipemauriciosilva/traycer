# Dependency Map: traycer

## Build & Toolchain

| Tool | Version | Purpose |
|---|---|---|
| Bun | 1.3.12 (pinned) | Package manager, runtime, build runner |
| Node.js | >=24.0.0 | Runtime for CLI and Electron main |
| NX | ^22.7.8 | Monorepo orchestration, caching, affected builds |
| TypeScript | ^6.0.3 | Primary language |
| Vite | ^8.2.0 | Bundler for `gui-app` and `desktop` renderer |
| @rolldown/plugin-babel | ^0.2.3 | Desktop main-process bundle |
| Electron | ^42.8.0 | Desktop shell |
| electron-builder | ^26.15.3 | Desktop packaging |
| pre-commit | (pip) | Git hooks |

## Testing

| Tool | Purpose |
|---|---|
| Vitest | Unit/integration tests across all packages |
| @testing-library/react | React component testing in `gui-app` |
| @testing-library/user-event | User interaction simulation |

## Key Runtime Dependencies by Package

### @traycer/protocol
- `zod` — schema validation
- `yjs` — CRDT for collaborative state

### @traycer-clients/traycer-cli
- `commander` — CLI argument parsing
- `zod` — schema validation
- `undici` — HTTP client
- `node-stream-zip` — archive extraction
- `tar` — archive extraction
- `@sentry/node` — error monitoring

### @traycer-clients/shared
- `zod` — schema validation (only explicit runtime dep; imports `@traycer/protocol` via TypeScript workspace resolution)

### @traycer-clients/gui-app
- `@traycer-clients/shared` — transport/auth
- `@traycer/protocol` — wire types
- `react`, `react-dom` — UI framework
- `@tanstack/react-router` — file-based routing
- `@tanstack/react-query` — server state management
- `@tanstack/react-virtual` — virtualized lists
- `zustand` (via `@legendapp/list`) — client state
- `tailwindcss` v4 — styling
- `shadcn/ui` components (via `@radix-ui/*`) — UI primitives
- `@tiptap/*` — rich text editor (collaborative, Yjs-backed)
- `@xterm/*` — terminal emulator
- `yjs` — CRDT for collaborative editing
- `@codemirror/*` — code editor
- `@sentry/browser` — error monitoring
- `@dnd-kit/*` — drag and drop

### @traycer-clients/desktop
- `@traycer-clients/gui-app` — renderer
- `@traycer-clients/shared` — transport
- `electron` — desktop shell
- `@sentry/electron` — error monitoring

## External Integrations

| Integration | Direction | Purpose |
|---|---|---|
| GitHub Releases | CLI downloads | Host binary provisioning |
| Traycer Cloud | GUI/CLI outbound | Auth, sync, agent orchestration |
| Claude Code | User-configured | AI coding agent |
| Codex (OpenAI) | User-configured | AI coding agent |
| Cursor | User-configured | AI coding agent |
| OpenCode | User-configured | AI coding agent |
| Sentry | Outbound | Error monitoring (production only) |

## Security Notes
- Production trust keys (host minisign public keys) are embedded at release time by CI — not committed.
- No secrets should ever be committed to this repository.
- Contributors need no secrets to build or test.
