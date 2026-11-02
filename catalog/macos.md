# macOS

**None of these rows has been observed on a Mac.** They list where AI tools usually keep things, from public
documentation and from how the same tools lay out their data on Windows. That makes every row `planned` and **Grey**:
an agent may measure it, look inside it, and show it, but it may not treat it as Yellow or Green until someone has
observed it on a real Mac (see [SOURCES.md](SOURCES.md) for the method).

All the usual rules apply: complete the eight checks ([steps/03](../steps/03-evidence.md)), never touch the
[protected list](_protected.md), ask before every deletion. Use these commands instead of the Windows ones:

| Need | macOS command |
|---|---|
| Size of a folder | `du -sk <path>` |
| Newest file inside | `find <path> -type f -exec stat -f '%m %N' {} + \| sort -rn \| head -1` |
| Processes with parent and start time | `ps -eo pid,ppid,lstart,comm` |
| What holds a path open | `lsof +D <path>` (slow on big folders; run it with a time limit) |
| Move to the Trash | `osascript -e 'tell application "Finder" to delete POSIX file "<path>"'` |

| ID | Path | What it is | Basis for the path | Status |
|---|---|---|---|---|
| MAC-001 | `~/.claude/projects/<project>/<session-id>.jsonl` and `<session-id>/` | Claude Code chat transcripts. Keep every `memory/` folder | Same layout as the Windows row CC-001. Not observed on a Mac | `planned` |
| MAC-002 | The per-user temporary folder, under a `claude/<project>/<session-id>/` path | Claude Code per-session scratch folders | Windows row CC-006. The exact macOS location is unconfirmed: find the temporary folder with `getconf DARWIN_USER_TEMP_DIR` and look for `claude` | `planned` |
| MAC-003 | `~/Library/Application Support/Claude/` | Claude desktop app data. Sign-in and app state live here (Red). Look inside for a folder named `vm_bundles` (the Cowork virtual machine) and cache folders | The app's config folder is documented at this path. The rest is unconfirmed | `planned` |
| MAC-004 | `~/.codex`, `~/.gemini`, `~/.continue` | Codex, Gemini CLI and Continue folders. Credentials and settings inside are Red | Documented default locations | `planned` |
| MAC-005 | `~/.ollama/models` | Downloaded local models. Use `ollama list` and `ollama rm <model>` first | Documented default for a user install | `planned` |
| MAC-006 | `~/Library/Caches/ms-playwright` | Browsers downloaded for automation | Documented default | `planned` |
| MAC-007 | `~/.cache/huggingface/hub` | Downloaded model and dataset cache | Documented default | `planned` |
| MAC-008 | `~/.vscode/extensions/anthropic.claude-code-<version>-*` | Old versions of the Claude Code extension beside the newest | Same layout as the Windows row CC-007 | `planned` |
| MAC-009 | Folders named `Antigravity` under `~/Library/Application Support` or `~/.antigravity` | Antigravity app data | Unconfirmed. Look for it; do not assume | `planned` |

## Not offered, ever

`/Applications/<Tool>.app` is an installed program (see the protected list). Removing one goes through the vendor's
own uninstall steps, on the user's request. Anything under `~/Library/Keychains`, `~/Library/Mail`,
`~/Library/Messages`, `~/Library/Safari`, Photos libraries, and Time Machine data is Red.

## Processes

The commands above list processes. Which process hosts the Cowork virtual machine on a Mac is **unconfirmed**: do not
assume a name. Show the candidates to the user and ask (H0).

## Help wanted

If you run Ballast on a Mac, please record what you actually find (path, size, newest file, what the tool did after
the removal) and send it as an issue or a pull request. A row only moves from `planned` to `review` with that
observation. See [CONTRIBUTING.md](../CONTRIBUTING.md).
