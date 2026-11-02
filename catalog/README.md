# Catalog

The catalog lists known AI-tool leftovers: where they live, what they are, which tier they belong to, what to
check before deleting, and what deleting costs. Agents read these tables in [steps 2 to 4](../steps).

## Files

| File | Covers |
|---|---|
| [_protected.md](_protected.md) | Red list: never deletable, applies to everything |
| [_attribution.md](_attribution.md) | How confident we are that an AI tool made something |
| [claude-code.md](claude-code.md) | Claude Code: transcripts, plugin leftovers, scratch folders |
| [claude-desktop-cowork.md](claude-desktop-cowork.md) | Claude desktop app: chat caches and the Cowork virtual machine |
| [orphan-processes-ram.md](orphan-processes-ram.md) | Processes AI tools leave running and the memory they hold |
| [gpu-memory.md](gpu-memory.md) | Graphics memory (VRAM and shared) held by local AI tools, and how to read it |
| [temp-and-recycle-bin.md](temp-and-recycle-bin.md) | The user's Temp folder (with a group rule for thousands of small files) and the Recycle Bin |
| [windows-and-app-caches.md](windows-and-app-caches.md) | Windows Installer cache (shown, never offered), Windows Update downloads, Chrome and Edge caches, Office add-in caches |
| [other-ai-tools.md](other-ai-tools.md) | Codex, Gemini, local models, image tools, shader caches, browser automation |
| [macos.md](macos.md) | macOS starter rows and commands (all `planned`, none observed yet) |
| [linux.md](linux.md) | Linux starter rows and commands (all `planned`, none observed yet) |
| [SOURCES.md](SOURCES.md) | Where each rule came from |

## Row format

| ID | Path | What it is | Tier | Evidence before delete | Cost / rebuild | Status |
|---|---|---|---|---|---|---|

Paths use `%USERPROFILE%`, `%LOCALAPPDATA%`, `%APPDATA%` (Windows) or `~` (macOS, Linux). Never write a real
username into a row.

## Status

| Status | Meaning |
|---|---|
| `active` | Observed to work: the item was removed and the tool kept working afterwards. A maintainer recorded it |
| `review` | Seen to exist, or removed once, but not yet confirmed across versions or after relaunch. Treat with extra care and say so |
| `disabled` | Known harmful or wrong. Agents must not use it |
| `planned` | Listed from documentation or from another system's layout, but **never observed**. Always Grey. See [macos.md](macos.md) and [linux.md](linux.md) |

New rows start as `review`, in tier Yellow or Grey. Promoting to Green or `active` needs evidence in the row's
*Verified* line.

## Tools change their folders

These paths are internal details of other people's products and can change in any release. Always run the
evidence checks in [steps/03-evidence.md](../steps/03-evidence.md) and prefer a tool's own cleanup or
uninstall command when it has one.
