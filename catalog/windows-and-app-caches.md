# Windows installer files, browser caches and Office caches

These are not made by AI tools, but they sit next to AI leftovers on the same disk, and an agent running Ballast will
meet them. Same tiers and rules as the rest of the catalog: read-only scan, evidence first, ask before every deletion.

## Windows installer files (shown, never offered)

| ID | Path | What it is | Tier | Why | Status |
|---|---|---|---|---|---|
| WIN-001 | `C:\Windows\Installer` | The Windows Installer cache: the original `.msi` and `.msp` files Windows needs to **repair, update or uninstall** installed programs | **Red** | Deleting files by hand can leave a program that cannot be repaired or removed, and Windows may not say so. The folder is also outside the user's profile, so the path guard refuses it. Report its size so the user understands where space goes; never offer it | `review` (size read: 3.14 GB in 1,488 files) |
| WIN-002 | `C:\ProgramData\Package Cache` | Setup bundles that installers keep so the program can be repaired or uninstalled later | **Red** | Same reason. Outside the profile | `review` (size read: 0.24 GB in 43 files) |
| WIN-003 | `C:\Windows\SoftwareDistribution\Download` | Windows Update downloads | **Grey** | Outside the profile and needs administrator rights, so an agent does not delete it. The supported way: Windows Settings, System, Storage, Temporary files, or Disk Cleanup, "Clean up system files", "Windows Update Cleanup". Tell the user and let them do it; do not elevate (H7) | `review` (read: 0 files at the time) |

**Do not use "installer cleaner" tools to prune `C:\Windows\Installer`.** They guess which files are orphaned, and a wrong
guess breaks uninstalling. If the user wants space from installed programs, offer the program's own uninstaller
(**Settings, Apps**), run by the user.

Installer files an installer **extracted into Temp** are different: see TMP-001 in
[temp-and-recycle-bin.md](temp-and-recycle-bin.md).

## Browser caches

Browser **profiles** are Red ([_protected.md](_protected.md)). Only the cache folders named here are ever offered, and
nothing else under `User Data`.

| ID | Path (under `%LOCALAPPDATA%\Google\Chrome\User Data` or `%LOCALAPPDATA%\Microsoft\Edge\User Data`) | What it is | Tier | Evidence before deleting | Cost / rebuild | Status |
|---|---|---|---|---|---|---|
| BR-001 | In each profile folder (`Default`, `Profile 1`, ...): `Cache`, `Code Cache`, `GPUCache`, `Service Worker\CacheStorage` | Chrome's cached web files and compiled code | Yellow | Chrome is not running (no `chrome` process). No links. Age is shown, not a gate | Pages load more slowly the first time. Offline data of some web apps lives in `CacheStorage` and has to download again | `review` |
| BR-002 | The same four names in each Edge profile folder | Edge's cached web files and compiled code | Yellow | Edge is not running (no `msedge` process; Edge also runs in the background and for embedded web views, so check the process list and ask) | As BR-001 | `review` |
| BR-003 | Directly under `User Data`: `ShaderCache`, `GrShaderCache`, `DawnGraphiteCache`, `DawnWebGPUCache`, `component_crx_cache`, `ProvenanceData` | Graphics shader caches and downloaded browser components | Yellow | As BR-001 or BR-002 for that browser | Rebuilt by the browser on next use | `review` |

Never offered, in any browser folder: `Cookies`, `Login Data`, `History`, `Bookmarks`, `Local Storage`, `IndexedDB`,
`Extensions`, `Preferences`, `Sessions`, or any file you have not been told is a cache. If a path is not in the table,
it is Red.

*Observed:* on one Windows 11 laptop on 2026-11-02, about 3.2 GB of Chrome caches and about 0.8 GB of Edge caches were
removed with the owner's approval, and the same steps are repeated by the owner's own weekly script. Whether the
browsers kept working afterwards was **not recorded**, so these rows stay Yellow and `review`.

## Office add-in caches

| ID | Path | What it is | Tier | Evidence before deleting | Cost / rebuild | Status |
|---|---|---|---|---|---|---|
| OFC-001 | `%LOCALAPPDATA%\Microsoft\Office\16.0\Wef` and `%LOCALAPPDATA%\Microsoft\Office\SolutionPackages` | Caches of Office add-ins (web extensions and solution packages) | Yellow | No Office program is running (Word, Excel, PowerPoint, Outlook, OneNote, Access, new Outlook). No links. Age is shown, not a gate | Add-ins reload from their source the next time Office opens | `review` |

The rest of `%LOCALAPPDATA%\Microsoft\Office` can hold Office's own settings and unsent or recovered work: it is Grey,
not Yellow. *Observed:* a 2.9 GB `Office` folder was removed whole on the owner's own request on the same laptop (they
do not use Office). That does not make the whole folder a Yellow row.

## How this relates to the owner's weekly script

The script has four steps. Two are Ballast rows already; two are added above.

| Script step | In Ballast |
|---|---|
| Cowork VM bundle | [CD-001](claude-desktop-cowork.md), with the stop-the-VM-worker case as RAM-003 |
| Claude Code chat history (`.claude\projects`, keeping each project's `memory` folder) | [CC-001](claude-code.md) |
| Office add-in caches | OFC-001 |
| Chrome and Edge caches | BR-001 to BR-003 |

Differences, on purpose: the script runs without asking per item and elevates itself with the Windows administrator
prompt. **Ballast does neither.** It asks per item, and it never relaunches itself elevated (H7). The script's habit of
skipping a step while the app is open is the same as Ballast's *In use now* check.

## Verified

- 2026-11-02, Windows 11, one laptop, read-only: `C:\Windows\Installer` 3.14 GB (1,488 files, no read errors),
  `C:\ProgramData\Package Cache` 0.24 GB (43 files), `C:\Windows\SoftwareDistribution\Download` empty. The Office
  add-in folders were empty (0.00 GB). Chrome `User Data` 2.78 GB and Edge `User Data` 0.45 GB in total (mostly
  profile data, since the caches had been cleared earlier the same day). Nothing was deleted by these rows.
