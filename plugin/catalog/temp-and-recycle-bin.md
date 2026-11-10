# Temporary files and the Recycle Bin

AI tools, and everything they run (package installers, browsers, build tools), drop files in the user's Temp folder
and, when Ballast deletes something, the Recycle Bin holds it. Both can hold gigabytes. Same tiers and rules as the
rest of the catalog: read-only scan, evidence first, ask before every deletion.

**Temp is not just AI leftovers.** Any program may keep files there, and some of them are in use or hold work that
is not saved yet. So nothing in Temp is Green. It is Yellow when the evidence is complete, and Grey otherwise.

## The Temp folder

### Which folder

On Windows the user's Temp folder is `%LOCALAPPDATA%\Temp`. The variable `%TEMP%` points at the same place, but it can
be an 8.3 short name such as `C:\Users\USERNA~1\AppData\Local\Temp`, and the path guard in
[steps/06](../steps/06-approve-and-run.md) refuses short names. **Always use the long form.** Confirm it is the same
folder before you rely on it:

```powershell
$short = $env:TEMP; $long = Join-Path $env:LOCALAPPDATA 'Temp'
$a = Get-Item -LiteralPath $short -Force; $b = Get-Item -LiteralPath $long -Force
$same = ($a.CreationTimeUtc -eq $b.CreationTimeUtc) -and `
  ((Get-ChildItem -LiteralPath $short -Force | Select-Object -ExpandProperty Name | Sort-Object) -join '|') -eq `
  ((Get-ChildItem -LiteralPath $long  -Force | Select-Object -ExpandProperty Name | Sort-Object) -join '|')
```

If `$same` is false (or any command fails), say so and ask the user which folder they mean. **Never delete the Temp
folder itself, only things inside it.** Never use a wildcard such as `Temp\*` to delete: delete each approved path.

### How to look (read-only)

Measure with the commands in [steps/02-measure.md](../steps/02-measure.md): total size, file count, how the files
split by age, links, and the largest children. **Show every top-level item**, not only the largest: the user decides.
A first look can take about a minute for a thousand entries and ten thousand files. Say so, and run it with a time
limit.

### Rows

| ID | What | Tier | Evidence before deleting | Cost / rebuild | Status |
|---|---|---|---|---|---|
| TMP-001 | A folder or file directly inside `%LOCALAPPDATA%\Temp` that no other row names | Yellow when all of this holds, else Grey | **Last used:** shown, never a gate (a "Heads up" if it changed in the last day, since it may hold unsaved work; the user decides). **In use:** no file inside can be opened exclusively (test below), and no running process is started from inside it. **No links or junctions** inside. **Not a document's recovery file:** names starting `~$` or `~WRL` are Grey | Whatever program left it loses that leftover. A half-finished installer cannot resume. Permanent: the Recycle Bin is not used (see the method below) | `review` |
| TMP-002 | `pip-unpack-*` and other `pip-*` folders (pip's own unpacking folders) | Yellow when no pip is running and nothing inside is open | A local yes/no match that no running process has `pip` in its command line (never print the command line); nothing inside can be opened exclusively; no links | pip re-downloads and re-unpacks if it needs them again | `review` |
| TMP-003 | `claude\<project>\<session-id>\` (Claude Code session scratch) | As [CC-006](claude-code.md): Yellow when the session is finished, Grey if live | As CC-006. Never the folder of the session you are in | As CC-006 | `review` |
| TMP-004 | Anything in Temp that is in use, locked, unreadable, contains a link, or has a document-recovery name | **Grey** | Not selectable. Report the total and what is holding each one; it can be re-checked after the program closes. Recent changes alone do **not** make an item Grey | Not applicable | `review` |
| TMP-005 | `C:\Windows\Temp` (system Temp) | Grey | It is outside the user's profile, so the path guard refuses it, and clearing it needs administrator rights. Do not elevate. Show the user how to clear it themselves (Windows Settings, System, Storage, Temporary files) | Not applicable | `planned` |
| TMP-006 | `remotion-webpack-bundle-*`, `remotion-v*-assets*` and `puppeteer_dev_chrome_profile-*` (video-rendering and headless-browser tools that AI coding agents often drive) | Yellow when nothing is open and no render or browser process is running; **a render in progress makes them Grey** | Process list (yes/no match for `node`, `remotion` or a headless browser started from inside the folder); nothing inside can be opened exclusively; no links. Bundles can be about 1.9 GB each and are created again for every render | The next render rebuilds the bundle, which takes time | `review` (seen: two to three 1.9 GB bundles appeared during one render; nothing was deleted) |

### Many small files: the group rule

Temp usually holds thousands of files. Do not ask the user to approve ten thousand lines one by one, and do not drop
the manifest either. Instead:

1. **Show the biggest ones as their own items:** each top-level child of 50 MB or more (the 30 largest), each with its
   full path.
2. **Everything else that qualifies becomes one group item** ("Everything else in Temp that qualifies"). For a group,
   write the **full manifest, one full path per line, to a text file in your own temporary folder**, and tell the user
   its path so they can open it. The dashboard item lists the 50 largest paths, and its *why* line states the total
   number of paths, the total size, the rule it was built from, and the manifest file's path.
3. **The approval request names** the count, the total size, the rule (which row, which checks) and the manifest
   file. The user's approval covers **exactly the lines in that file**, nothing added later.
4. **Re-check each path right before deleting it** (the checks above and the path guard). Skip anything that changed,
   became in use, or is no longer on the manifest, and count it as skipped.
5. **Log counts and reasons:** deleted, skipped (and why), locked, failed. Delete the manifest file at the end
   (H12), unless the user asks to keep it.

### In-use test

A file is "in use" when it cannot be opened exclusively. Do this on each file inside the item before deleting. It
changes nothing:

```powershell
function InUse([string]$p) { try { $s = [IO.File]::Open($p, 'Open', 'ReadWrite', 'None'); $s.Close(); $false } catch { $true } }
```

An error other than "in use" (for example access denied) also counts as in use, because the answer is unknown (H2).

### Method

**Permanent**, with the user's approval, because moving temporary files to the Recycle Bin only fills it. Say plainly in
the approval request that Temp deletions cannot be undone. Use the delete in [steps/06](../steps/06-approve-and-run.md)
section 5, one path at a time.

## The Recycle Bin

| ID | What | Tier | Evidence before emptying | Cost | Status |
|---|---|---|---|---|---|
| BIN-001 | The Recycle Bin on the system drive, for the current user | **Grey** until the user confirms they have looked, then **Yellow** | **Unsaved or needed work:** the user opens the Recycle Bin themselves and confirms nothing in it is needed (their answer, this session). **How to get it back:** it cannot be restored once emptied | **Everything in the Bin is lost for good**: files that were there before this session, files from other programs, and files Ballast moved there. Free space returns only when the Bin is emptied | `review` (reading observed; emptying not tested) |

### How to look (read-only)

```powershell
$bin = (New-Object -ComObject Shell.Application).NameSpace(0xA)
$bin.Items().Count
```

For each item's name, original folder, size and date deleted, read the shell view's detail columns
(`$bin.GetDetailsOf($item, <column>)`; find the column numbers by listing `0..20 | % { $bin.GetDetailsOf($null, $_) }`; on the author's Windows 11 laptop that gave Name 0, Original Location 1, Date Deleted 2, Size 3, but the numbers can differ, so list them first. Reading an item's values was not tested because the Bin was empty).
Read names, sizes and dates only (H8). Report: how many items, the total size, the oldest and newest deletion dates, and
the 20 largest items (name and original folder). If you moved items to the Bin during this session, say how many of the
Bin's items those are, from your own log, so the user sees how much of it Ballast put there.

### Emptying it

1. **Show the summary above and ask the user to open the Recycle Bin and look.** Do not empty it for them.
2. **After they confirm they have looked**, ask a separate question: *"Empty the Recycle Bin on C: now? Everything in
   it is lost for good, including files that were there before today."* A general "yes" to cleaning up does not count.
3. Only then:

   ```powershell
   Clear-RecycleBin -DriveLetter C -Force
   ```

4. Re-measure free space and report the actual change.

Never delete anything inside the hidden `$Recycle.Bin` folder by path: it is system structure, and other users' items
live there. Use the command above only. Other drives' Bins are out of scope, as the path guard allows only the system
drive's profile.

## macOS and Linux (starter rows, never observed)

| ID | Path | What it is | Tier | Notes | Status |
|---|---|---|---|---|---|
| TMP-M1 | `$TMPDIR` (macOS, per-user temp under `/var/folders/...`) | User temp | Grey | Same checks as TMP-001; find the path with `echo $TMPDIR`; do not guess | `planned` |
| TMP-L1 | `$TMPDIR` or `/tmp` entries **owned by the current user** (Linux) | User temp | Grey | `/tmp` is shared: never touch entries owned by anyone else | `planned` |
| BIN-M1 | `~/.Trash` (macOS) | Trash | Grey | Same two-step rule as BIN-001; empty with the Finder, not `rm` | `planned` |
| BIN-L1 | `~/.local/share/Trash` (Linux) | Trash | Grey | Same two-step rule; prefer `gio trash --empty` after the user confirms | `planned` |

## Verified

- 2026-11-02, Windows 11, Windows PowerShell 5.1, one laptop. **Temp, read-only:** 1.45 GB in 9,405 files; 48 files
  (0.01 GB) older than 7 days; no links; no read errors; about 20 seconds. The largest children were `claude`
  (0.23 GB) and seven `pip-unpack-*` folders (0.06 to 0.15 GB each). `%TEMP%` was an 8.3 short name; the long form
  `%LOCALAPPDATA%\Temp` was confirmed as the same folder (same creation time and child names). The in-use test
  correctly reported a dummy file as free, then in use while it was held open, then free again.
- A fuller read-only scan on the same laptop later that day listed **every** top-level entry: 1,487 entries, 1.75 GB,
  about 54 seconds. 1,452 were `pip-*` folders (1.47 GB), 1 was the Claude Code scratch folder (0.23 GB), 28 were in
  use, unreadable or held a link (under 0.01 GB together), and the other 6 were small. With age shown but not used
  as a gate, 1,458 entries were Yellow and 29 were Grey.
- **First real deletion** (2026-11-02, author's laptop): see C14 in [dev/tests.md](https://github.com/chittychat-studio/Ballast/blob/main/dev/tests.md). 1,771 Temp entries, 2.09 GB, were
  deleted from an approved manifest; 100 were skipped and 1 failed because another process held it open. During the same
  hour a video render kept adding about 1.9 GB bundles, so free space fell although Ballast freed space.
- **Recycle Bin, read-only (the author's laptop; always measure your own):** the shell view read it and reported 0
  items (it had been emptied earlier). Nothing was
  deleted by these rows, and `Clear-RecycleBin` was **not** run, so BIN-001 emptying is untested.
