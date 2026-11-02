# Linux

**None of these rows has been observed on Linux.** They list where AI tools usually keep things, from public
documentation and from how the same tools lay out their data on Windows. That makes every row `planned` and **Grey**:
an agent may measure it, look inside it, and show it, but it may not treat it as Yellow or Green until someone has
observed it on a real Linux machine (see [SOURCES.md](SOURCES.md) for the method).

All the usual rules apply: complete the eight checks ([steps/03](../steps/03-evidence.md)), never touch the
[protected list](_protected.md), ask before every deletion. Use these commands instead of the Windows ones:

| Need | Linux command |
|---|---|
| Size of a folder | `du -sk <path>` |
| Newest file inside | `find <path> -type f -printf '%T@ %p\n' \| sort -rn \| head -1` |
| Processes with parent and start time | `ps -eo pid,ppid,lstart,comm` |
| What holds a path open | `lsof +D <path>` (slow on big folders; run it with a time limit) |
| Move to the Trash | `gio trash <path>` where available |

| ID | Path | What it is | Basis for the path | Status |
|---|---|---|---|---|
| LIN-001 | `~/.claude/projects/<project>/<session-id>.jsonl` and `<session-id>/` | Claude Code chat transcripts. Keep every `memory/` folder | Same layout as the Windows row CC-001. Not observed on Linux | `planned` |
| LIN-002 | The system temporary folder, under a `claude/<project>/<session-id>/` path | Claude Code per-session scratch folders | Windows row CC-006. The exact Linux location is unconfirmed | `planned` |
| LIN-003 | `~/.codex`, `~/.gemini`, `~/.continue` | Codex, Gemini CLI and Continue folders. Credentials and settings inside are Red | Documented default locations | `planned` |
| LIN-004 | `~/.ollama/models` | Downloaded local models for a user install. Use `ollama list` and `ollama rm <model>` first | Documented default for a user install | `planned` |
| LIN-005 | `~/.cache/ms-playwright` | Browsers downloaded for automation | Documented default | `planned` |
| LIN-006 | `~/.cache/huggingface/hub` | Downloaded model and dataset cache | Documented default | `planned` |
| LIN-007 | `~/.vscode/extensions/anthropic.claude-code-<version>-*` | Old versions of the Claude Code extension beside the newest | Same layout as the Windows row CC-007 | `planned` |
| LIN-008 | Folders named `Antigravity` under `~/.config` or `~/.antigravity` | Antigravity app data | Unconfirmed. Look for it; do not assume | `planned` |

## Not offered, ever

- **System-wide model stores.** An Ollama installed as a service keeps models under a system path such as
  `/usr/share/ollama/.ollama/models`. That is system data: it is Red here. Removal goes through `ollama rm` as the
  right user, on the user's request.
- Anything installed by the package manager (`/usr`, `/opt`, `/var/lib`), and any other user's home folder.

## Claude desktop

No official Claude desktop app is documented for Linux, so there are no desktop or Cowork rows here. Do not assume one
exists. If the user runs an unofficial build, treat its data as Grey and ask.

## Processes

The commands above list processes. There is no Windows-style virtual machine worker to consider; a leftover
virtual-machine or container process is something to show the user and ask about (H0), not to stop by name.

## Help wanted

If you run Ballast on Linux, please record what you actually find (path, size, newest file, what the tool did after
the removal) and send it as an issue or a pull request. A row only moves from `planned` to `review` with that
observation. See [CONTRIBUTING.md](../CONTRIBUTING.md).
