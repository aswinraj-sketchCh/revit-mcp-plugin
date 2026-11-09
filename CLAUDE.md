# Revit MCP Plugin — agent rules

Natural-language BIM for Autodesk Revit 2024–2027. Chain: Claude → MCP server (Python) → pyRevit Routes → Revit API. Revit runs on Windows only; nothing here can be exercised end-to-end in a Linux container.

## Layout
- `revit-bim/` — the Claude plugin: `mcp-server/` (Python, `uv`, entry `main.py`, tools in `tools/` and `revit_mcp/`, own `tests/`), `skills/revit-bim/`, `commands/*.md`.
- `setup-*.ps1` / `.bat`, `start-revit-mcp.*` — Windows installers; helpers in `lib/*.ps1`.
- `tests/*.ps1` — Pester-style tests for the PowerShell helpers (`_assert.ps1`).

## Commands
- MCP server: `cd revit-bim/mcp-server && uv sync && uv run python main.py`. Files in `tests/` are standalone scripts (`uv run python tests/<file>.py`) that call tools over stdio and need a running Revit with pyRevit Routes, so they cannot pass in a Linux container.
- PowerShell tests need `pwsh`: `pwsh tests/Test-SetupDryRun.ps1`.

## Rules
- Keep the tool count in README/docs in sync when adding or removing an MCP tool.
- Revit API calls are transactional; every write tool must open and commit/roll back a transaction.
