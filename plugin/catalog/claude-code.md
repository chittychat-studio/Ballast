# Claude Code

Windows paths. For macOS and Linux see [macos.md](macos.md) and [linux.md](linux.md) (starter rows, not yet observed).

Evidence for every row: complete [steps/03-evidence.md](../steps/03-evidence.md). Never touch the session you
are running in, and treat any other running session as in use.

| ID | Path | What it is | Tier | Evidence before delete | Cost / rebuild | Status |
|---|---|---|---|---|---|---|
| CC-001 | `%USERPROFILE%\.claude\projects\<project>\<session-id>.jsonl` and the matching `<session-id>\` folders (sub-agent logs, tool results) | Chat transcripts and their working files | Yellow | Session is not running now (no live agent process for it); the newest write time is shown, with a "Heads up" if recent; **leave `memory\` and anything that is not a session-ID folder or `.jsonl` file untouched** | Old chats can no longer be resumed or searched. No rebuild | `active` |
| CC-002 | `%USERPROFILE%\.claude\projects\<entry for a scratch or worktree folder>` | Project entries for temporary folders (names contain `Temp-claude` or `scratchpad`) | Yellow | The folder the entry names no longer exists | Chat history for that temporary folder | `review` |
| CC-003 | `%USERPROFILE%\.claude\plugins\.trash\*` and `%USERPROFILE%\.claude\removed-<date>\` | Leftovers from removed plugins and settings | Yellow | Plugin is not in use; user does not want it back | Removed plugins cannot be restored from here afterwards | `review` |
| CC-004 | `%USERPROFILE%\.claude\plugins\cache` | Downloaded copies of installed plugins | Yellow | No session running (plugins are read at start) | Plugins re-download when next needed | `review` |
| CC-005 | `%USERPROFILE%\.claude\file-history` | Undo history for file edits | Yellow | No session running | Cannot undo past edits | `review` |
| CC-006 | `%LOCALAPPDATA%\Temp\claude\<project>\<session-id>\` | Per-session scratch folder: scratchpad files, task output, images | Yellow when the session is finished; **Grey if it is live** | The `<session-id>` is not a running session. Never delete the folder of the session you are in. These folders can hold the only copy of something an agent made, so list what is inside and ask | Loses anything in it that was not saved elsewhere | `review` |
| CC-007 | `%USERPROFILE%\.vscode\extensions\anthropic.claude-code-<version>-*` (older versions beside the newest) | Old extension versions | Yellow | Not the version in the running process path | Re-installs from the marketplace if needed | `review` |

## Always protected here (Red)

`settings*.json`, `.claude.json`, `CLAUDE.md`, `skills\`, `agents\`, `commands\`, `hooks\`, credential and
login files, MCP configuration, and **`projects\<project>\memory\`**.

## Verified

- CC-001: 2026-11-02, Windows 11, Claude Code VS Code extension 2.1.314. 264 transcript items removed (about
  3.2 GB); the two live sessions, and every `memory\` folder, were kept; the sessions kept working.
- CC-002 to CC-007: items seen on the same machine and sizes measured; not yet removed or confirmed across versions.

## Prevention

Check the tool's documentation for a transcript-retention setting; clear old sessions on a schedule
([steps/08](../steps/08-prevent-regrowth.md)).
