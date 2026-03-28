# OpenClaw Architecture Guide

An architectural overview of OpenClaw, the multi-channel personal AI assistant.
Written for developers approaching the codebase for the first time.

## Documents

| Document | What it covers |
|---|---|
| [System Architecture](system-architecture.md) | Core components, message pipeline, gateway, agent runtime, provider layer |
| [Context and Memory](context-and-memory.md) | Context window management, transcript compaction, long-term memory, embeddings, retrieval |
| [Plugin System](plugin-system.md) | Extension lifecycle, SDK surface, extension points, plugin authoring model |
| [Development Process](development-process.md) | AI-assisted development (self-dogfooding), CI/CD, testing, release workflow |

## Quick Orientation

OpenClaw is a **multi-channel AI gateway** that connects messaging platforms
(Discord, Slack, Telegram, iMessage, WhatsApp, Signal, and more) to LLM providers
(Anthropic, OpenAI, Google, Ollama, and 20+ others) through a unified agent runtime.

It runs as a local daemon (the **gateway**) on the user's machine, with native apps
for macOS, iOS, and Android, plus a full-featured CLI.

### Repository Layout

| Directory | Purpose |
|---|---|
| `src/` | Core runtime (~84 modules, TypeScript/ESM) |
| `extensions/` | 82+ plugin packages (channels, providers, tools) |
| `apps/` | Native clients: `macos/` (SwiftUI), `ios/` (SwiftUI), `android/` (Kotlin/Compose) |
| `skills/` | 53 AI agent skill definitions (used in development) |
| `scripts/` | 177 build, dev, and release scripts |
| `docs/` | Mintlify-hosted documentation |
| `packages/` | Shared monorepo packages |
| `ui/` | Web UI components (control panel) |
| `test/` | Test infrastructure and fixtures |

### Key Technical Facts

- **Language:** TypeScript (ESM), strict typing, no `any`
- **Runtime:** Node 22+ (Bun for dev/scripts)
- **Package manager:** pnpm (monorepo with workspaces)
- **Agent engine:** `@mariozechner/pi-coding-agent` SessionManager
- **Build:** tsdown with custom post-build pipeline
- **Test:** Vitest with V8 coverage (70% threshold)
- **CI:** GitHub Actions with dynamic scope detection
- **Formatting/Linting:** Oxfmt + Oxlint
