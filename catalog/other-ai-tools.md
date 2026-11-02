# Other AI tools

Rows OT-001 to OT-008 are `review`: folder names and sizes were seen on one Windows 11 machine on 2026-11-02, and
**contents were not inspected**. Treat as Grey until step 3 evidence says otherwise. Rows marked *unverified* come from
general public knowledge and were not seen on any machine. Rows OT-009 to OT-016 (local model, image and graphics-cache
tools) are `planned` and Grey: none of them has been observed or removed.

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

### Local model and image tools, and graphics caches

Paths below come from the tools' public documentation or general knowledge and **were not seen on any machine**,
except where the Notes say so. They stay Grey until a maintainer observes them. Model files are the user's own
downloads: list them with the tool, show size and last-used, and ask **per model**. Never delete by extension alone
(`.gguf`, `.safetensors`, `.ckpt` and `.bin` files are listed by the large-files scan, but a file is only a candidate
when it sits under a row below or the user points to it). For where graphics memory is held by a running model, see
[gpu-memory.md](gpu-memory.md).

| ID | Path | What it is | Tier | Evidence before delete | Cost / rebuild | Notes |
|---|---|---|---|---|---|---|
| OT-009 | `%USERPROFILE%\.lmstudio\models` | LM Studio downloaded models (older versions: `%USERPROFILE%\.cache\lm-studio\models`) | Grey | Prefer LM Studio's own model list and delete; app closed; ask per model | Re-download per model | *Unverified:* not seen |
| OT-010 | `%LOCALAPPDATA%\nomic.ai\GPT4All` | GPT4All downloaded models | Grey | Prefer the app's own model manager; app closed; ask per model | Re-download per model | *Unverified:* not seen |
| OT-011 | The user's ComfyUI or Stable Diffusion install: `models\checkpoints`, `models\loras`, `models\vae` and the `output` folder | Image-model files and generated images | Grey | Ask the user where it is installed; **do not search the disk**. Checkpoints: ask per file. `output` holds the user's own images: Red unless the user says otherwise per file | Re-download checkpoints; generated images cannot be regenerated exactly | *Unverified:* location differs per install |
| OT-012 | `%LOCALAPPDATA%\llama.cpp` | llama.cpp download cache for models fetched by name | Grey | No llama.cpp process running; ask per model | Re-download per model | *Unverified:* not seen |
| OT-013 | `%USERPROFILE%\.cache\huggingface\hub` | Hugging Face model and dataset cache | Grey | Prefer `huggingface-cli scan-cache` to list, then ask per repo; no process using it | Re-download per repo | *Unverified:* the same folder is `planned` on macOS and Linux |
| OT-014 | `%LOCALAPPDATA%\D3DSCache` | DirectX shader cache | Grey | No game or graphics program running | First launches of games and graphics programs are slower while it rebuilds | Folder seen (0.00 GB); never removed. A candidate for Green once a removal is observed |
| OT-015 | `%LOCALAPPDATA%\NVIDIA\DXCache`, `%LOCALAPPDATA%\NVIDIA\GLCache`, `%LOCALAPPDATA%\NVIDIA\ComputeCache` | NVIDIA shader and CUDA compile caches | Grey | No game or CUDA program running | Rebuilt on next use, with slower first runs | *Unverified:* the machine observed has no NVIDIA card |
| OT-016 | `%LOCALAPPDATA%\AMD\DxCache` | AMD shader cache | Grey | No game or graphics program running | Rebuilt on next use | *Unverified:* the machine observed has no AMD card |

## Evidence from the author's machine

- OT-005: the application was uninstalled with its own uninstaller after the user had already removed the models
  (3.1 GB freed). The user's models folder was already empty (`.ollama`).

## Adding a tool

Add a row only after you have seen the folder yourself, measured it, and listed its children. Start at `review`
and Grey or Yellow. See [CONTRIBUTING.md](../CONTRIBUTING.md).
