# Processes AI tools leave running (memory)

Same tiers and rules as the rest of the catalog. **Stopping a process is a deletion-class action: ask first,
name the exact process ID, say what it is and what could be lost.**

## How to look (Windows; macOS and Linux: `ps -eo pid,ppid,comm,args`)

```powershell
Get-CimInstance Win32_Process | Select-Object ProcessId, ParentProcessId, Name, ExecutablePath, CommandLine, CreationDate
```

Work out for each candidate: who started it (the parent), is the parent still alive, which project folder it runs
from, when it started, and whether the user started it deliberately.

| ID | What | Tier | Evidence before stopping | Cost | Status |
|---|---|---|---|---|---|
| RAM-001 | Dev servers an agent started (for example `uvicorn`, `node`, `vite`, `next`, simple HTTP servers) | Yellow | Command line and working folder; whether the user started it or relies on it; parent session ended | In-memory state is lost; anything using that server stops | `review` |
| RAM-002 | Headless or automation browsers (headless Chrome, test browsers) | Yellow | No visible window; parent is gone or finished; not the user's own browser | Loses that automation run | `review` |
| RAM-003 | Cowork VM worker (`vmwp`) and `vmmem` | Yellow | The desktop app has been closed. The VM worker also serves other tools (WSL, Docker, sandboxes), so **prefer a reboot**. Stop one only if exactly one candidate matches the Claude VM, nothing else shares it, and the user approves | Stops the Cowork VM and its session, and a forced stop can corrupt the VM disk. Needs administrator rights, since it is a system process | `review` |
| RAM-004 | MCP servers started by agents (processes whose command line names an MCP server) | Yellow | The agent session that started them has ended | The server stops; it restarts with its agent | `review` |
| RAM-005 | Local model runners that keep a model loaded in memory | Yellow | Prefer the tool's own stop command if it has one; no request is running | Next request reloads the model | `review` |

## Never stop, without naming it and asking

- Your own process ancestry (step 1) and anything in the same IDE or terminal.
- **Other agent sessions** (each is a separate process under the IDE or terminal).
- The user's browser, IDE, editor, and any server the user says they rely on.
- Security software and system processes.

## Rules

- Stop by **exact process ID**, never by name across the board. IDs get reused: immediately before stopping,
  re-match the ID, **start time, path and owner** (it must belong to the current user). If anything differs, stop
  and ask.
- Match command lines locally and report only yes or no. Do not print a whole command line (it can contain secrets).
- If a stop needs administrator rights, follow [permissions.md](../permissions.md): show **one** exact command and let
  the user run it. Never relaunch yourself elevated.
- Processes are never Green and are never part of a group approval.

## Verified

- RAM-003 (2026-11-02, Windows 11): the Cowork VM worker was not releasable by closing the app; it needed an
  administrator command. A live `uvicorn` server running from a project's virtual environment (RAM-001) was the
  user's own and was left running.
- RAM-001 to RAM-005 otherwise: not removed or confirmed across versions.
