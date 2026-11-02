# Claude desktop app: chat and Cowork

Windows (Store install) paths. `<package-family>` is the app's package family folder under
`%LOCALAPPDATA%\Claude-Data\` (observed: `claude_pzs8sxrjxfjjc`). macOS and Linux: `planned`.

Evidence for every row: complete [steps/03-evidence.md](../steps/03-evidence.md). The desktop app must be
closed (including its system-tray process) for most rows to be removable.

| ID | Path | What it is | Tier | Evidence before delete | Cost / rebuild | Status |
|---|---|---|---|---|---|---|
| CD-001 | `%LOCALAPPDATA%\Claude-Data\<package-family>\vm_bundles\claudevm.bundle\` (disk images, compressed originals, kernel and initrd files) | The Cowork virtual machine | Yellow | Desktop app is not running; the VM worker is not holding the files. Do not force-test by deleting: a lock means stop and follow [permissions.md](../permissions.md) | **Wipes Cowork session data stored in the VM.** The app rebuilds the VM (about 9 GB) the next time Cowork is used | `review` |
| CD-002 | `...\<package-family>\Cache`, `Code Cache`, `GPUCache`, `GrShaderCache` | Browser-style caches of the app | Green | Desktop app is not running | Rebuilt as you use the app | `review` |
| CD-003 | `...\<package-family>\claude-code`, `claude-code-vm` | Downloaded command-line binaries for the app | Yellow | Desktop app is not running | Re-downloaded when needed | `review` |
| CD-004 | `...\<package-family>\local-agent-mode-sessions`, `claude-code-sessions` | Small session records | Yellow | Desktop app is not running | Loses those session records | `review` |

## Always protected here (Red)

`Partitions\`, `Session Storage`, `Local Storage`, `IndexedDB`, `Network` and cookie files: they hold sign-in and app
state. Anything under the app's install folder (`WindowsApps`) is the program itself.

## RAM

While Cowork runs, a virtual machine worker and a `vmmem` process hold memory. See
[orphan-processes-ram.md](orphan-processes-ram.md).

## Verified

- CD-001: 2026-11-02, Windows 11, app 4.4212.0.0. Removed after the app's own process tree was stopped by exact
  process IDs (with the user's approval), and the VM worker was stopped from an administrator terminal. Freed
  about 10.7 GB. **Rebuild on next launch not yet observed by the author**, so the row stays `review`.
- CD-002: removed with the app closed (about 0.7 GB); relaunch not yet observed.
- CD-003, CD-004: sizes measured only.

## Prevention

Close the app and its VM when you finish a Cowork session; expect a rebuild on next use.
