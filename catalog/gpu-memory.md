# Graphics memory (VRAM) that AI tools leave in use

Local AI tools load models into the graphics card's own memory (dedicated memory, "VRAM"). Computers with
integrated graphics have none: they borrow system RAM instead ("shared" memory). A crashed or forgotten model runner
can keep gigabytes of either allocated, and the computer feels slow while nothing looks busy.

Same tiers and rules as the rest of the catalog. **Reading graphics memory is read-only. Stopping the process that
holds it is the same kind of action as in [orphan-processes-ram.md](orphan-processes-ram.md): ask first, name the exact
process ID, say what could be lost.** Nothing here is ever "deleted".

## How to look (read-only)

Windows, any make of graphics (no administrator rights needed):

```powershell
Get-CimInstance Win32_VideoController | Select-Object Name, AdapterRAM, DriverVersion, Status
Get-Counter '\GPU Adapter Memory(*)\Dedicated Usage','\GPU Adapter Memory(*)\Shared Usage'
Get-Counter '\GPU Process Memory(*)\Dedicated Usage','\GPU Process Memory(*)\Shared Usage'
```

- The counter instance names contain the process ID (`pid_1234_luid_...`). Take the number from there, then look the
  process up (`Get-Process -Id 1234`) before reporting it.
- Counters are a snapshot. Take it twice a few seconds apart if a number matters. The per-process figures may not add
  up to the adapter figure.
- `AdapterRAM` is a 32-bit field and is wrong for cards above 4 GB, and on integrated graphics it is not dedicated
  memory. **Do not use it as the card's memory size.** Use the vendor tool below, or leave the total unknown.
- NVIDIA, if `nvidia-smi` exists: `nvidia-smi --query-gpu=name,memory.total,memory.used --format=csv` and
  `nvidia-smi --query-compute-apps=pid,process_name,used_memory --format=csv`. Use these numbers in preference to the
  counters. AMD: `rocm-smi` on Linux. Apple silicon uses one pool of memory for everything, so there is no separate
  VRAM to read.
- If a command is missing or fails, say so and report "not measured" (H13). Do not estimate. Do not install a tool to
  get the number: show the user the one command and let them run it ([permissions.md](../permissions.md)).

## Rows

| ID | What | Tier | Evidence before stopping | Cost | Status |
|---|---|---|---|---|---|
| GPU-001 | A process holding dedicated graphics memory that is a local model runner or image generator (for example Ollama, a llama.cpp server, LM Studio, ComfyUI) | Grey (`planned` rows are always Grey) | Exact PID, owner (must be the current user), start time and path; no request or generation is running; prefer the tool's own stop command (Ollama: `ollama ps`, then `ollama stop <model>`); the user did not start it on purpose | The loaded model is unloaded and an unsaved generation is lost; the next request reloads the model | `planned` |
| GPU-002 | A process holding **shared** graphics memory on integrated graphics (this memory is system RAM) | Yellow | Same checks as GPU-001. Say which process it is and what it is for; many large holders are the user's browser or desktop and are not AI leftovers | The process closes; anything unsaved in it is lost | `review` |
| GPU-003 | A model runner that is idle but still holds a loaded model (nothing running, parent session gone) | Grey (`planned` rows are always Grey) | As GPU-001, plus the parent session has ended | As GPU-001 | `planned` |

## Never stop, without naming it and asking

- Your own process ancestry (step 1) and anything in the same IDE or terminal.
- **Other agent sessions.**
- The desktop compositor, the user's browser, games, video calls, screen recorders and any other program the user is
  using for work. They hold graphics memory too; holding it is normal.
- Anything an agent session is using for the work the user asked for.
- Security software and system processes.

## Rules

- Stop by **exact process ID**, never by name across the board. Immediately before stopping, re-match the ID, start
  time, path and owner. If anything differs, stop and ask.
- Do not reset, restart or reconfigure the graphics driver, change driver or registry settings (including timeout
  settings), or run a GPU reset command. Those can crash every program using the screen.
- Never say that stopping a process "frees VRAM" or "speeds things up" as a promise. Say what was measured before
  and after, and nothing more (H11, H13).
- Processes are never Green and never part of a group approval.
- If a stop needs administrator rights, follow [permissions.md](../permissions.md): show one exact command and let the
  user run it. Never relaunch yourself elevated.

## What the dashboard shows

The optional `gpu` block in [dashboard.md](../dashboard.md): the graphics name, dedicated memory used and total when
the total is known, and shared memory used. If the scan could not read the numbers, leave the block out and the bar is
hidden.

## Verified

- 2026-11-02, Windows 11, one laptop with **integrated** Intel Iris Xe graphics and no discrete card: the three
  commands above ran without administrator rights and returned numbers. Dedicated usage was 0; shared usage was about
  0.6 GB, and one process held about 1.5 GB of shared memory at that moment. `nvidia-smi` was not present. No process
  was stopped. This confirms the **reading** method (GPU-002, `review`).
- GPU-001 and GPU-003 were never observed (no discrete card, no model runner loaded) and stay `planned`: Grey for the
  agent until a maintainer records an observation.
