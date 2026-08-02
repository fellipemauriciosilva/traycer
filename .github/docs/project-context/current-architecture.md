# Current Architecture: traycer

## Architecture Style
**Monorepo** (Bun workspaces + NX). Five independently buildable packages in a layered dependency graph.

## Package Dependency Graph

```
clients/desktop  ──────┐
                        ↓
clients/gui-app  ──→  @traycer-clients/shared  ──→  @traycer/protocol
clients/traycer-cli ──→  @traycer-clients/shared  ──→  @traycer/protocol
```

- `@traycer/protocol` has no internal dependencies — it is the wire contract.
- `@traycer-clients/shared` depends only on `@traycer/protocol`.
- `@traycer-clients/gui-app` and `@traycer-clients/traycer-cli` depend on `shared` and `protocol`.
- `@traycer-clients/desktop` depends on `gui-app` (bundles it) and `shared`.

## Runtime Communication

```
[Desktop (Electron main)]
   ↕ IPC / contextBridge
[GUI App (React renderer)]
   ↕ WebSocket / HTTP (localhost)
[Traycer Host] ← provisioned by CLI from GitHub Releases; NOT in this repo
   ↕
[Cloud / AI Providers]
```

Desktop discovers host WS URL from `~/.traycer/host[/dev]/pid.json`.  
Desktop does NOT proxy host RPC — `gui-app` talks directly to the host after resolving `LocalHostSnapshot`.

## Package Internals

### @traycer/protocol
- Wire contract for all client⇄host communication.
- Per-method `{ major, minor }` RPC versioning negotiated at handshake.
- CLI inlines protocol at build time (no runtime dependency).
- Subpath exports: `agent/*`, `auth`, `host/*`, `framework/*`, `persistence/*`, `utils/*`.

### @traycer-clients/traycer-cli
- Host supervisor: downloads, verifies (minisign), and starts signed host binaries from GitHub Releases.
- Auth surface: PKCE OAuth flow.
- Agent and workspace commands.
- Built as a Node.js SEA (Single Executable Application) for distribution.
- Key scripts: `build:sea`, `smoke:sea`, `smoke:ndjson`.

### @traycer-clients/shared
- Transport: WebSocket + RPC multiplexer.
- Auth: PKCE/bearer token management.
- Comment formatting and agent formatting utilities.
- Modules: `auth/`, `epic/`, `host-client/`, `host-lifecycle/`, `host-lock/`, `host-transport/`, `host-version/`, `keybindings/`, `platform/`, `support/`, `worktree/`.

### @traycer-clients/gui-app
- React application (Vite + ES modules, strict mode).
- **Routing:** TanStack Router (file-based routes in `src/routes/`).
- **State:** Zustand for UI/client state only; TanStack Query for server state.
- **UI:** Tailwind v4 + shadcn/ui primitives in `src/components/ui/` (compose, don't rewrite).
- **Rich text:** Tiptap with collaboration extensions (Yjs-based).
- **Terminal:** xterm.js.
- Key directories: `src/routes/`, `src/components/`, `src/stores/`, `src/hooks/`, `src/lib/`.
- Generated (do not hand-edit): `src/routeTree.gen.ts`, `dist/`, `.tanstack/`.

### @traycer-clients/desktop
- Electron main process: `src/electron-main/` (feature folders: `app/`, `auth/`, `host/`, `windows/`, `menu/`, `tray/`, `ipc/`).
- Preload bridges: `src/electron-preload/` (exposes `window.runnerHost` via contextBridge).
- Renderer shell: `src/renderer-shell/` (thin React host; UI from gui-app via vite aliases).
- IPC contracts: `src/ipc-contracts/` (plain-data types shared across main/preload/renderer).
- Production trust keys and host version pinned at release time by CI; never committed.

## Config Strategy
- Each client's `src/config.ts` defaults to **dev** (localhost endpoints, empty trust keys).
- Production values stamped at release time by `scripts/set-deploy-target.cjs --target=production`.
- `--restore` returns to dev defaults after a build.

## CI / CD
- GitHub Actions workflows in `.github/workflows/`.
- Tests run in CI (`test.yml`), not in pre-commit hook.
- Releases built and signed in Traycer's internal repo; published here cross-repo.

## Pre-commit
- Hooks run affected workspace checks: build, compile, lint, format.
- DCO sign-off enforced by `commit-msg` hook type.
- Install: `pipx install pre-commit && pre-commit install --hook-type pre-commit --hook-type commit-msg`.
