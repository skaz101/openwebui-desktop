# AGENTS.md

## Cursor Cloud specific instructions

### Overview

This is **Open WebUI Desktop** — an Electron app (macOS/Windows/Linux) wrapping the Open WebUI AI chat interface. It uses `electron-vite` + Svelte 5 + TypeScript + Tailwind CSS 4. The bundled Python-based Open WebUI server and llama.cpp engine are managed at runtime by the app itself (not dev dependencies).

### Development Commands

| Task | Command |
|------|---------|
| Install deps | `npm ci` |
| Dev mode | `npm run dev` |
| Lint | `npm run lint` |
| Typecheck | `npm run typecheck` |
| Build | `npm run build` (runs typecheck then electron-vite build) |
| Format | `npm run format` |

### Key Notes

- **Node.js 22+ required.** Use `source /home/ubuntu/.nvm/nvm.sh && nvm use 22` before running commands.
- **Native dependency `node-pty`** is rebuilt for Electron during `postinstall` via `electron-builder install-app-deps`. If `npm ci` succeeds, native deps are ready.
- **D-Bus errors** (e.g. "Failed to connect to the bus") are expected in the Cloud Agent headless environment and do not affect app functionality.
- **Display :1** is pre-configured (Xvfb). Set `DISPLAY=:1` when launching the Electron app.
- **Lint has pre-existing errors** in the codebase (prettier/unused-vars/no-explicit-any). The linter itself works correctly; these are not regressions from your changes.
- The app auto-installs its Python runtime and open-webui server on first "Get Started" click. This takes ~30 seconds. No external Python setup is needed for development.
- No Docker, no databases, no external services required for development of the Electron shell.
