# Business Glossary: traycer

## Core Concepts

| Term | Definition |
|---|---|
| **Agent** | A durable session created within a Task; the user works with it through a Chat or Terminal interface. Not to be confused with a Coding Agent. |
| **Coding Agent** | The underlying AI provider powering an agent (e.g. Claude Code, Codex, Cursor, OpenCode, Traycer native). |
| **Task** | The unit of work that contains one or more Agents. |
| **Epic** | Primary organizational unit in Traycer. A versioned persistence record (V200) containing chats, agents, artifacts, spec and review bodies. Each Epic has a **Canvas** (tiled workspace of panels) and multiple tabs. Epics are shareable and support real-time collaborative editing via Yjs. |
| **Host** | The Traycer Host binary that runs locally; provisioned by the CLI from GitHub Releases. NOT in this repo. |
| **Host Snapshot / LocalHostSnapshot** | The runtime object describing a discovered running host instance (WS URL, version, etc.). |
| **BYOA (Bring Your Own Agent)** | The feature allowing users to connect their existing AI provider subscriptions. |
| **Board** | Marketing term for a shared/collaborative Epic workspace. Not a distinct technical concept in the codebase — maps to an Epic with its Canvas view. |
| **Protocol** | The versioned client⇄host wire contract (`@traycer/protocol`). |
| **RPC Version** | Per-method `{ major, minor }` version pair negotiated at handshake (not npm semver). |
| **DCO** | Developer Certificate of Origin — sign-off required on every commit (`git commit -s`). |

## Packages (User-Facing Names)

| Package | User-Facing Name |
|---|---|
| `@traycer-clients/desktop` | Traycer Desktop (the app) |
| `@traycer-clients/traycer-cli` | `traycer` CLI |
| `@traycer-clients/gui-app` | GUI renderer (internal) |
| `@traycer/protocol` | Protocol (internal) |
| `@traycer-clients/shared` | Shared transport (internal) |

## Integration Points

| Term | Definition |
|---|---|
| **Claude Code** | Anthropic's coding agent, supported as a Coding Agent in Traycer. |
| **Codex** | OpenAI's coding agent, supported as a Coding Agent. |
| **Cursor** | Cursor AI coding agent, supported as a Coding Agent. |
| **OpenCode** | OpenCode AI coding agent, supported as a Coding Agent. |
| **Traycer native** | Traycer's own inference subscription, built into the platform. |

## Technical Terms

| Term | Definition |
|---|---|
| **SEA** | Single Executable Application — the CLI distribution format for Node.js. |
| **minisign** | Signature format used to verify signed host binaries downloaded from GitHub Releases. |
| **PID lock** (`~/.traycer/host[/dev]/pid.json`) | File that the running host writes; Desktop reads it to discover the host WS URL. |
| **pre-commit** | Git hook framework used to run affected workspace checks before each commit. |
| **NX** | Build orchestration tool for the monorepo; handles caching and affected-only builds. |
| **Canvas** | Tiled workspace inside an Epic; each tab has its own `EpicCanvasState` (root tile tree + active pane + instance/size maps). Managed by `src/stores/epics/canvas/`. |
| **Tile** | An individual panel within a Canvas (e.g., a chat, terminal, artifact view). Identified by `instanceId`; layout defined by the tile tree. |
| **IRunnerHost** | Platform-agnostic interface defined in `@traycer-clients/shared/platform/runner-host`. Exposes auth, host discovery (`onLocalHostChange`), window management, tray, host picker, workspace folders, and more to `gui-app`. Implemented by `clients/desktop` via `contextBridge.exposeInMainWorld('runnerHost', …)`. Constructed at bootstrap and passed explicitly into `<TraycerApp />`. |
