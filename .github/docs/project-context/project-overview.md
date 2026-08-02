# Project Overview: traycer

## Summary
Traycer is an open-source AI orchestration desktop application. It lets users bring their own AI agent subscriptions (Claude Code, Codex, Cursor, OpenCode) and run multiple agents in parallel with shared memory, model switching, agent-to-agent communication, and real-time collaboration.

## Repository
- **GitHub:** https://github.com/traycerai/traycer
- **License:** MIT
- **Default branch:** `main`
- **Contribution:** Open-source; DCO sign-off required on all commits

## Type
Desktop application (Electron) + CLI + GUI renderer + protocol library

## Primary Language
TypeScript

## Business Purpose
Enable developers to use their existing AI provider subscriptions across multiple models and agents simultaneously — without vendor lock-in — with persistent context and real-time collaboration features.

## Key Capabilities
- **Bring Your Own Agent (BYOA):** Connect Claude Code, Codex, Cursor, OpenCode, or Traycer native inference.
- **Unified Context:** Switch models within the same agent; context is shared across providers.
- **Agent-to-Agent Communication:** Automated loops where agents communicate, debate architecture, or review code.
- **Collaboration:** Shareable boards, real-time editing, ticket assignment.
- **Cross-Device Sync:** Same agent state across devices and OS.

## Versioning Strategy
- **App version:** Semantic Versioning (published on GitHub Releases)
- **Protocol versioning:** Per-method `{ major, minor }` RPC versions negotiated at handshake — independent of npm semver.

## Deployment Model
- Desktop binaries (macOS, Linux, Windows) published on GitHub Releases — built and signed in Traycer's internal repo.
- The **Traycer Host** (backend) is NOT in this repo; the CLI provisions a signed host binary from GitHub Releases.
- **Contributors need no secrets** to build or test the open-source code here.

## Changelog
Maintained in `CHANGELOG.md`, following Keep a Changelog convention.
