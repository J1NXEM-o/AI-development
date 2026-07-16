# Havoc Project Memory

## Project Overview
Havoc is a post-exploitation / adversary simulation framework with three components: teamserver (Go), client (C++/Qt), and Demon payload (C).

## Key Findings (2026-07-16)

### Remote File Management Feature Removed
Full remote FS management was identified and removed across all three components:

**Files modified:**
- `teamserver/pkg/agent/demons.go` — Removed COMMAND_FS cases from TaskBuild and CommandOutput handlers
- `teamserver/pkg/agent/commands.go` — Removed DEMON_COMMAND_FS_* constants (DIR=1 through CAT=10)
- `payloads/Demon/src/core/Command.c` — Removed ~380-line orphaned FS function body
- Client UI files (done earlier in session)

**Remaining reference:** `payloads/Demon/src/core/Download.c` still uses `DEMON_COMMAND_FS` as a package type for download chunks — this is expected and functional.

## Build Notes
- `go build ./...` in teamserver produces only a system-level `.sframe` linker warning (pre-existing, unrelated)
- No Go or C compilation errors from our edits
