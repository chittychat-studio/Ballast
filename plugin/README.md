# Ballast

> Not legal advice. Not affiliated with, or endorsed by, any AI provider.

Ballast is a set of plain-text instructions that your AI agent follows to find and clear the disk and memory
leftovers that AI tools leave behind: Claude Code and Claude desktop (chat and Cowork), Codex, Gemini, Antigravity,
local models (their files on disk, and the GPU memory they keep loaded), MCP servers, headless browsers, and the
scratch projects agents create.

This folder is the whole plugin. It holds Markdown instructions, a catalog of known leftovers, one skill, a
manifest and an icon. **There is no program, script, MCP server or hook in it, and it fetches nothing from the
web.** Your agent reads the instructions and uses its own tools, behind its own permission prompts.

## What it does

1. **Shows the version and asks two consent questions** before it looks at anything.
2. **Scans, read-only.** It measures known AI leftovers, your Temp folder and the Recycle Bin, browser and Office
   caches, large unknown folders, and the memory and GPU memory held by leftover processes. It reads names, sizes
   and dates only, never file contents.
3. **Sorts what it found into tiers** (Green, Yellow, Grey, Red) after eight checks per item, and shows you a
   table in the chat.
4. **You choose** what to clear. It then **asks again, per item, with the full path**, before anything is deleted.
5. **Deletes only what you approved**, to the Recycle Bin where that really works, and reports the measured result.

It never deletes personal files, backups, credentials, browser profiles, git history or AI memory files, and it
never works around your agent's permission prompts.

## How to use it

Install it from Claude's plugin directory, or from its own marketplace, pinned to a release:

```
/plugin marketplace add chittychat-studio/Ballast#v0.1.3
/plugin install ballast@ballast
```

Then run `/ballast:ballast`, or just ask:

- "I'm low on disk space. Find what my AI tools have left behind."
- "My laptop is struggling. What is holding memory and GPU memory right now?"
- "Run the weekly Ballast check and show me what has grown since last time."

For deletions, use a mode in which your agent asks you before it runs shell commands.

## What this install does not include

The cloned repository also has a static dashboard page that shows the same results in your browser. A plugin
install has no page, so you get the results as a table in the chat. To use the page, clone the repository:
<https://github.com/chittychat-studio/Ballast>.

## Your data

Ballast collects nothing and has no servers. Your agent reads folder names, paths, sizes and dates on your
computer, and whatever your agent reads reaches your AI provider under your own account. Details:
[privacy](https://github.com/chittychat-studio/Ballast/blob/main/PRIVACY.md) ·
[safety](https://github.com/chittychat-studio/Ballast/blob/main/SAFETY.md) ·
[security](https://github.com/chittychat-studio/Ballast/blob/main/SECURITY.md).

## Status and support

Windows 11 is the first supported system. macOS and Linux rows are starters that have not been confirmed on a
real machine. Questions and bugs: <https://github.com/chittychat-studio/Ballast/issues>.

Provided "as is", without warranty. Back up what matters before you clear anything.
[Apache License 2.0](LICENSE). See [NOTICE](NOTICE).
