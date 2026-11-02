<p align="center"><img src="dashboard/ballast-logo.svg" alt="Ballast" width="220"></p>

> **Draft v0.1.** Not legal advice. Not affiliated with, or endorsed by, any AI provider. Read [SAFETY.md](SAFETY.md) first.

Ballast is a set of plain-text instructions that your AI coding agent follows to find and clear the disk and memory
gunk that AI tools leave behind: Claude Code and Claude desktop (chat and Cowork), Codex, Gemini, Antigravity, local
models, MCP servers, headless browsers, and the scratch projects agents create.

There is **nothing to install and no program to run**. The instructions are Markdown. The repo also holds one
static dashboard page (HTML that runs only in your browser, makes no network requests, and cannot delete anything)
and a logo. Your own agent reads the instructions, runs read-only checks through its own tools, and **asks you before
every deletion**.

## What it does

1. **Scans, read-only.** Measures known AI leftovers and finds large unknown folders. Nothing is changed.
2. **Runs eight checks before judging** (last used, in use now, is it a program, anything depends on it, unsaved
   work, cloud or shared, protected name, how to get it back). A folder is never classified from its name or date.
3. **Sorts everything into tiers** (below) and shows you a dashboard.
4. **You choose** Keep, Clear or Check first per item, then paste a message with your choices to your agent.
5. **Asks again, per item,** with the full path, before anything is deleted. Your choice selects; your approval
   authorises.
6. **Deletes only what you approved,** to the Recycle Bin or Trash where that really works, and logs what happened.
7. **Never just says "I can't."** If something is locked or needs admin rights, the agent explains why, asks for the
   permission it needs, and shows the workaround. See [permissions.md](permissions.md).
8. **Tells you how to stop it coming back.**

**The rule above all others: if the agent is unsure about anything, it asks you.** It never decides for you.

## What it never does

- Deletes personal files, anything named backup, credentials, browser profile data, git history, or AI memory files.
  These are the Red tier and cannot be selected. See [catalog/_protected.md](catalog/_protected.md).
- Ships or runs installers, binaries or scripts.
- Sends file contents anywhere, or collects any data. See [PRIVACY.md](PRIVACY.md).
- Works around your agent's permission system, your operating system's protections, or your security software.
- Promises that your computer will be faster or that a deletion is "safe". Items are *classified*, and you decide.

## Tiers

| Tier | Meaning | Examples | In the dashboard |
|---|---|---|---|
| **Green** | Regenerable cache, no data loss | App caches, temp files, update downloads | Keep by default; you can choose Clear |
| **Yellow** | Regenerable at a cost, or an app is affected | Chat transcripts, `node_modules`, `.venv`, VM images, model files | Keep by default; the cost is shown |
| **Grey** | In use, unknown, or evidence incomplete | An item a server is running from | Keep or Check first, never Clear |
| **Red** | Personal or irreplaceable | Documents, backups, credentials, memory files, browser profiles | Shown, locked |

## Quick start

1. Clone this repo and **pin a version** (a release tag once available, otherwise a commit you have read).
   Do not let an agent fetch and follow instructions from a live URL.
2. Read [cleanup.md](cleanup.md) and [permissions.md](permissions.md) yourself. They are short.
3. Open your agent in the cloned folder and say: **"Read AGENTS.md and run cleanup.md."**
4. For a recurring check, say: **"Run weekly.md."** (Stay present: it never runs unattended.)

Per-tool notes: [Claude Code](providers/claude.md) · [Gemini CLI](providers/gemini.md) · [Codex CLI](providers/codex.md) ·
[Antigravity](providers/antigravity.md). Any other agent that can read files and run commands can follow the same
instructions if you tell it to read `AGENTS.md`.

## The dashboard

After a scan your agent fills the data block of [`dashboard/ballast-dashboard.html`](dashboard/ballast-dashboard.html)
and gives you a link to a local copy. Open the template directly to see it with example data. It has a folder view
with Keep / Clear / Check first choices, a free-space bar, charts, a breakdown table, light and dark themes, and a
"Scan again" button. See [dashboard.md](dashboard.md).

## What is in this repo

| Path | Purpose |
|---|---|
| [cleanup.md](cleanup.md) | The master prompt: rules and flow |
| [permissions.md](permissions.md) | Ask-first protocol and the blocked-item playbook |
| [weekly.md](weekly.md) | Recurring routine with growth tracking |
| [steps/](steps) | The eight steps, one file each |
| [catalog/](catalog) | Known AI leftovers by tool, with tier, evidence needed and status |
| [dashboard.md](dashboard.md) and [dashboard/](dashboard) | Spec, data contract, the static dashboard template and the logo |
| [providers/](providers) | Notes for each AI agent |
| [SAFETY.md](SAFETY.md) · [PRIVACY.md](PRIVACY.md) · [SECURITY.md](SECURITY.md) | The safety, privacy and security promises |
| [docs/](docs) | Comparison with similar tools, legal notes, claims register |

## Status

Windows 11 is the first supported system. The Claude Code, Claude desktop (Cowork) and orphan-process catalogs come
from observations on one real machine; rows marked `review` have not yet been confirmed across versions. macOS and
Linux rows are planned. Contributions are welcome: see [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

Ballast is provided "as is", without warranty of any kind, to the extent permitted by law. Back up what matters
before you clear anything. You are responsible for what you approve. Read [SAFETY.md](SAFETY.md).

Product and company names in this repo (for example Claude, Gemini, Codex, Antigravity, Windows, Chrome) belong to
their owners and are used only to identify the tools and folders they refer to.

## Licence

[Apache License 2.0](LICENSE). See [NOTICE](NOTICE).
