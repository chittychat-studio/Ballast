# Other AI tools

All rows are `review`: folder names and sizes were seen on one Windows 11 machine on 2026-11-02, and **contents
were not inspected**. Treat as Grey until step 3 evidence says otherwise. Rows marked *unverified* come from
general public knowledge and were not seen on any machine.

Prefer the tool's own cleanup or uninstall command when it has one.

| ID | Path | What it is | Tier | Evidence before delete | Cost / rebuild | Notes |
|---|---|---|---|---|---|---|
| OT-001 | `%LOCALAPPDATA%\OpenAI\Codex` | Codex app data (0.67 GB seen) | Grey | Inspect children; none in use | Unknown until inspected | Contents not inspected |
| OT-002 | `%USERPROFILE%\.codex` | Codex CLI folder (0.09 GB seen) | Grey | Inspect; credentials inside are Red | Unknown | Contents not inspected |
| OT-003 | `%USERPROFILE%\.gemini` | Gemini CLI folder (0.23 GB seen) | Grey | Inspect; credentials and settings inside are Red | Unknown | Contents not inspected |
| OT-004 | `%USERPROFILE%\.continue` | Continue extension data (0.12 GB seen) | Grey | Inspect | Unknown | Contents not inspected |
| OT-005 | `%LOCALAPPDATA%\Programs\Ollama` | Ollama application files (3.1 GB seen) | Grey (it is an installed program) | Not running; the user asks for it to be removed | Re-install to use again | Offered only as "run the vendor's own uninstaller", on the user's request and with approval. Never delete the folder |
| OT-006 | `%USERPROFILE%\.ollama\models` | Downloaded local model files | Yellow | Prefer the tool's own list and remove commands; model not loaded | Re-download per model | Models can be tens of GB; ask per model, show last-used |
| OT-007 | `%LOCALAPPDATA%\ms-playwright` | Browsers downloaded for automation | Yellow | No automation running | Re-download on next run | *Unverified:* folder was present but empty here |
| OT-008 | `%USERPROFILE%\.cache` and its children | Generic user cache (0.14 GB seen). May include model hubs and tool caches | Grey | Inspect each child; classify separately | Varies | *Unverified:* children not inspected |

## Evidence from the author's machine

- OT-005: the application was uninstalled with its own uninstaller after the user had already removed the models
  (3.1 GB freed). The user's models folder was already empty (`.ollama`).

## Adding a tool

Add a row only after you have seen the folder yourself, measured it, and listed its children. Start at `review`
and Grey or Yellow. See [CONTRIBUTING.md](../CONTRIBUTING.md).
