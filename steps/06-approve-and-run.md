# Step 6: approve and run

Only now may anything be deleted, and only what the user approved (H0, H9).

## 1. Build the manifest

Take the user's choices (see "When the user sends their choices back" in [dashboard.md](../dashboard.md)) and match
them against **your own** scan results. Drop anything not in your results. Build a numbered manifest of full,
unshortened paths with sizes and tiers, and show it to the user.

## 2. Get approval per item

Use the request format in [permissions.md](../permissions.md). The user's click on the dashboard **selects**; the
approval here **authorises**. A general "yes to everything" is not enough for Yellow items: confirm them
individually. For a large item, say whether the Recycle Bin can hold it (see section 5).

## 3. Order

Green first, then Yellow. Within a group, smallest cost first. Stop on the first surprising result and re-assess.

## 4. Check right before each delete

Immediately before deleting each item, repeat the checks that could have changed: In use now, Last used, and links.
If the item changed or became active since the scan, skip it and tell the user.

### Path guard

Do not run a delete unless **all** hold:

- The path is on the approved manifest, exactly, in full.
- **Resolve it first:** get its full canonical path (expand `..`, 8.3 short names such as `PROGRA~1`, and links).
  Compare the resolved path, case-insensitively, with the approved one. If they differ, stop.
- It is on a **local fixed drive** and lies inside the **current user's profile folder**. Refuse network paths
  (`\\server\share`, mapped drives), removable drives, other users' profiles, and the profile folder itself or its
  standard folders (Desktop, Documents, Downloads, Pictures, Videos, Music, OneDrive, AppData).
- The path has no trailing dot or space and no `..` segment.
- **It contains no symbolic link or junction** (reparse point), at the top or anywhere inside. Windows PowerShell 5.1
  can follow a link when deleting recursively and remove what it points at. Check first:

  ```powershell
  $full = (Get-Item -LiteralPath $path -Force).FullName
  $links = Get-ChildItem -LiteralPath $full -Recurse -Force -Attributes ReparsePoint -ErrorAction Stop
  if ((Get-Item -LiteralPath $full -Force).Attributes -band [IO.FileAttributes]::ReparsePoint -or $links) { 'STOP: contains a link or junction' }
  ```

  If a link is present, do not delete recursively. Tell the user; offer to remove only the link itself, or skip.
  If the check errors, treat it as "contains a link".
- No wildcard reaches outside the approved folder.

## 5. Methods (Windows examples)

**Recycle Bin (default for Yellow, and for Green when the user prefers).** It does not work for everything. An item
bigger than the Bin's limit, or on a drive without a Bin, can be deleted **permanently with no warning**. So:

1. Before: if the item is larger than 4 GB, or the Bin's capacity or the drive type is unclear, tell the user it may
   be permanent, treat the method as **Permanent**, and ask.
2. Run:

   ```powershell
   Add-Type -AssemblyName Microsoft.VisualBasic
   [Microsoft.VisualBasic.FileIO.FileSystem]::DeleteDirectory($path, 'OnlyErrorDialogs', 'SendToRecycleBin')   # folder
   [Microsoft.VisualBasic.FileIO.FileSystem]::DeleteFile($path, 'OnlyErrorDialogs', 'SendToRecycleBin')       # file
   ```

3. After: check the item really is in the Bin (for example, look for its name in the Recycle Bin with the shell
   object). **If you cannot confirm it, report the item as permanently deleted**, not as "moved".

Free space does not return until the Recycle Bin is emptied. Offer that **after** step 7 has verified that the
user's tools still work, and warn that emptying removes everything in the Bin, not only what Ballast moved.

**Permanent (Green caches the user approved, or an item the user chose to remove for good):**

```powershell
Remove-Item -LiteralPath $path -Recurse -Force -ErrorAction Stop
```

Use `-LiteralPath`. Never use shell tricks to bypass a refusal (H7). If a long path or lock stops it, report and
follow [permissions.md](../permissions.md).

**macOS and Linux:** use the system Trash (`osascript` or `trash` on macOS, `gio trash` on Linux). For a permanent
delete, never run `rm -r` with a variable you have not checked: the variable must be non-empty, absolute, resolved,
and on the manifest. Print the exact command to the user first.

## 6. Log as you go

Keep a running log: time, item, tier, size, method **as it actually happened**, result (deleted, moved, skipped,
blocked, failed) and the user's approval. Keep it in the conversation and, if the user agrees, in a report file
(step 7).

## 7. Handle blockers

Locked, needs admin, denied, partial: follow [permissions.md](../permissions.md). Never end a blocked item with only
"I can't". Ask for the permission you need and show the workaround.
