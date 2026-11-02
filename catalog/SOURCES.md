# Sources

Every catalog row must be traceable. Ballast does not copy rules from other cleaners or rule databases.

## Row provenance

| Files | Source | Date | Notes |
|---|---|---|---|
| claude-code.md, claude-desktop-cowork.md, orphan-processes-ram.md | The authors' own observations on one Windows 11 machine, while freeing disk space | 2026-11-02 | Claude Code VS Code extension 2.1.314; Claude desktop app 4.4212.0.0 (Store install). Sizes and behaviour are as observed, not guaranteed elsewhere |
| other-ai-tools.md | Folder names and sizes seen on the same machine; contents **not inspected**. Some rows are from general public knowledge and are labelled as unverified | 2026-11-02 | OT-001 to OT-008 `review`; OT-009 to OT-016 `planned` |
| temp-and-recycle-bin.md, windows-and-app-caches.md | Read-only measurements on the same machine (Temp, Recycle Bin, Windows Installer cache, Package Cache, browser and Office folders), and the owner's own weekly cleanup script for the browser and Office cache paths. Nothing was deleted to make these rows | 2026-11-02 | All `review` or `planned`; WIN-001 and WIN-002 are Red |
| gpu-memory.md | The reading commands were run on the same machine (integrated Intel Iris Xe, no discrete card, no `nvidia-smi`). The vendor-tool commands come from the tools' own documentation and were not run | 2026-11-02 | GPU-002 `review`; GPU-001 and GPU-003 `planned` |

## Further observations

| Area | Observation | Date |
|---|---|---|
| `%APPDATA%` (Roaming), `C:\ProgramData`, other drives | On the observed machine there was one drive (C:). AI-named folders in Roaming and ProgramData were tiny (about 0.01 GB each: an Antigravity folder, a "Claude Code" folder, a `Claude` folder). The large folders there belong to other, non-AI programs and are out of scope. No catalog rows were added | 2026-11-02 |

## Adding a source

When you add or change a row, add a line here: where the information came from (your own observation, a
tool's official documentation, or other), the date, and the versions. If it came from another project's
rule set, **do not copy it**: check its licence first and ask a maintainer. GPL rule sets cannot be copied
into this Apache-2.0 repository.

## Method for observations

A row is observed by (1) measuring the item, (2) completing the evidence checks, (3) removing it with the
user's approval, (4) confirming the tool still works afterwards. Steps 1 and 3 can be recorded the same day;
step 4 may need a relaunch. Until step 4 is recorded, the status stays `review`.
