# Step 2: measure (read-only)

Goal: sizes for known AI leftovers, plus a short list of large unknown folders. Change nothing.

## 1. Known targets

For each catalog row that applies, measure its size and newest file date. Windows example:

```powershell
$path = "$env:LOCALAPPDATA\<the row's path>"
if ([string]::IsNullOrWhiteSpace($path) -or -not (Test-Path -LiteralPath $path)) { return }
$files = Get-ChildItem -LiteralPath $path -Recurse -Force -File -ErrorAction SilentlyContinue -ErrorVariable measureErrors
($files | Measure-Object Length -Sum).Sum / 1GB
$files | Sort-Object LastWriteTime -Descending | Select-Object -First 1 LastWriteTime, Name
```

**Check `$measureErrors`.** If any subfolder could not be read, the size and the newest date are incomplete:
report them as "at least" and mark the dates **unknown** (H2). Do not treat hidden errors as "nothing there".

(macOS and Linux: `du -sk <path>`; for the newest file use `find <path> -type f -exec stat -f '%m %N' {} +` on
macOS or `find <path> -type f -printf '%T@ %p\n'` on Linux, then sort. These are different on each system, so
check which one you are on first.)

**Links and junctions.** Do not follow them. If a folder contains a symbolic link or junction (reparse point),
note it. Measuring through one can report the size and dates of somewhere else entirely:

```powershell
Get-ChildItem -LiteralPath $path -Recurse -Force -Attributes ReparsePoint -ErrorAction SilentlyContinue | Select-Object FullName, LinkType, Target
```

Rows with no matching path are simply absent: skip them quietly.

## 2. Unknown space (AI-related roots first)

Measure the immediate children of the places where AI tools commonly leave things, largest first, top 15 each:

- the home folder's dot-folders (`%USERPROFILE%\.*`, `~/.*`)
- `%LOCALAPPDATA%` and `%APPDATA%` (Linux: `~/.local/share`, `~/.cache`, `~/.config`)
- the user's projects or code folders, one level down

Then list the largest individual files over 200 MB in the user's profile, **excluding** Red locations
([catalog/_protected.md](../catalog/_protected.md)). For Red locations you may report a total size so the user
understands where space goes, but never list their contents for deletion.

## 3. Report totals, not conclusions

Show a short table: item, size, newest file date, which catalog row it matched (or "unknown"). Do not classify
yet. Unknown large folders go to step 3 for evidence.

## 4. Mind the cost

If a scan is slow, say so, run it in the background with a time limit, and tell the user. Stop anything you
started when done (H12).
