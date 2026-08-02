# Module Map: traycer

## Workspace Root

| Path | Purpose |
|---|---|
| `protocol/` | `@traycer/protocol` — client⇄host wire contract |
| `clients/traycer-cli/` | `@traycer-clients/traycer-cli` — CLI |
| `clients/shared/` | `@traycer-clients/shared` — transport, auth, formatting |
| `clients/gui-app/` | `@traycer-clients/gui-app` — React GUI renderer |
| `clients/desktop/` | `@traycer-clients/desktop` — Electron shell |
| `scripts/` | Workspace-level dev scripts (e.g. `dev-desktop.js`) |
| `eslint/` | Shared ESLint configs |
| `docs/` | Developer documentation (`DEVELOPMENT.md`) |

## @traycer/protocol (`protocol/`)

| Path | Purpose |
|---|---|
| `src/agent/` | Agent-related protocol types |
| `src/auth/` | Auth protocol types |
| `src/config/` | Config protocol types |
| `src/host/` | Host-related protocol types |
| `src/host-transport/` | Host transport multiplexer |
| `src/framework/` | Framework versioning (per-method `{ major, minor }`) |
| `src/persistence/` | Persistence protocol types |
| `src/notifications/` | Notification protocol types |
| `src/comments/` | Comment protocol types |
| `src/crypto/noise/` | Noise protocol crypto |
| `utils/` | Yjs utilities, text utilities |
| `__tests__/` | Protocol unit tests |

## @traycer-clients/traycer-cli (`clients/traycer-cli/`)

| Path | Purpose |
|---|---|
| `src/` | CLI entry point and commands |
| `scripts/` | Build scripts (SEA, npm, smoke tests) |

## @traycer-clients/shared (`clients/shared/`)

| Path | Purpose |
|---|---|
| `auth/` | PKCE/bearer authentication |
| `epic/` | Epic state management |
| `host-client/` | Host RPC client |
| `host-lifecycle/` | Host start/stop lifecycle |
| `host-lock/` | Host PID lock management |
| `host-transport/` | WebSocket transport and multiplexer |
| `host-version/` | Host version resolution |
| `keybindings/` | Keybinding management |
| `platform/` | Platform detection utilities |
| `support/` | Support utilities |
| `worktree/` | Git worktree integration |
| `__tests__/` | Shared unit tests |

## @traycer-clients/gui-app (`clients/gui-app/`)

| Path | Purpose |
|---|---|
| `src/routes/` | File-based routes (TanStack Router) |
| `src/components/` | App UI components |
| `src/components/ui/` | shadcn/ui primitives (compose, don't rewrite) |
| `src/stores/` | Zustand stores (UI/client state) |
| `src/stores/epics/open-epic/` | Per-epic Y.Doc projector |
| `src/hooks/` | Custom hooks (`hooks/<ns>/use-<verb>-<noun>-{mutation,query}.ts`) |
| `src/lib/query-keys/` | TanStack Query key builders |
| `src/lib/commands/` | Command palette sources + actions |
| `src/providers/` | App-wide React providers |
| `__tests__/` | GUI unit tests (Vitest + Testing Library) |

## @traycer-clients/desktop (`clients/desktop/`)

| Path | Purpose |
|---|---|
| `src/electron-main/` | Electron main process |
| `src/electron-main/app/` | App lifecycle |
| `src/electron-main/auth/` | Auth integration |
| `src/electron-main/host/` | Host discovery and lifecycle |
| `src/electron-main/windows/` | Window management |
| `src/electron-main/menu/` | Application menu |
| `src/electron-main/tray/` | System tray |
| `src/electron-main/ipc/` | IPC handlers |
| `src/electron-preload/` | contextBridge preload scripts |
| `src/renderer-shell/` | Thin React shell (embeds gui-app) |
| `src/ipc-contracts/` | Plain-data IPC types |
| `src/shared/` | Electron main-process shared utilities (e.g. CSP helpers) |
| `resources/cli/` | Staged CLI SEA binaries |
| `resources/tray/` | Tray icons |
| `scripts/` | Dev, prepack, and asset scripts |
