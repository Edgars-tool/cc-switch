# GitHub Copilot Instructions — cc-switch (fork)

## Project Overview
Fork of farion1231/cc-switch — cross-platform desktop app for managing Claude Code, Codex, Gemini CLI, OpenCode, and OpenClaw.
  Stack: Tauri 2 + Rust (backend) + React + TypeScript (frontend) + SQLite

  ## This is a Fork
  - Upstream: farion1231/cc-switch (currently 117+ commits ahead)
  - Before making changes: git fetch upstream && git merge upstream/main to stay current
- For upstream contributions: open issues/PRs on the upstream repo

## Git Workflow
- Always git pull origin main before starting
- Conventional commits: feat/fix/docs/chore(scope): description
- Scopes: provider, mcp, skills, proxy, session, ui, tauri, db
  - For fork-specific changes: prefix scope with "fork-" e.g. feat(fork-openclaw): ...

## Architecture
  - Frontend: src/ — React + TypeScript + Vite + TailwindCSS + TanStack Query
- Backend: src-tauri/ — Rust + Tauri 2 commands/services/DAO
  - Database: ~/.cc-switch/cc-switch.db (SQLite, SSOT)
  - Backups: ~/.cc-switch/backups/ (auto-rotated, 10 most recent)

## Development Commands
- Install deps: pnpm install
- Dev mode: pnpm dev
- Type check: pnpm typecheck
- Format: pnpm format
- Tests: pnpm test:unit
  - Build: pnpm build
- Rust format: cd src-tauri && cargo fmt
- Rust lint: cd src-tauri && cargo clippy

## Code Style
- Frontend: React functional components, TypeScript strict, TanStack Query for data fetching
- Backend: Layered architecture — Commands > Services > DAO > Database
  - Rust: use thiserror for errors, tokio for async, follow clippy suggestions
- Atomic writes: temp file + rename pattern for config safety
- All data flows through SQLite (SSOT) — never write config files directly

## Before Committing
1. pnpm typecheck (no type errors)
2. pnpm format:check (formatted)
  3. pnpm test:unit (all tests pass)
  4. cargo clippy (no warnings)

## Key Design Principles
- Minimal intrusion: even after uninstall, CLI tools continue working
- Atomic writes: prevent config corruption
- SSOT: all data in SQLite, JSON only for device-level settings
