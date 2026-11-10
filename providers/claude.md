# Using Ballast with Claude Code

Check Claude Code's current documentation for exact option names; they change.

1. Clone this repo, pin a version, and read [cleanup.md](../plugin/cleanup.md) and [permissions.md](../plugin/permissions.md).
2. Open Claude Code in the cloned folder. It reads `CLAUDE.md`, which points to `AGENTS.md`, which sends it to
   the instructions in the `plugin` folder.
3. Say: **"Read AGENTS.md and run cleanup.md."** For the recurring routine: **"Run weekly.md."**

## Or install it as a plugin

The repo's `plugin` folder is a Claude Code plugin, and the repo is its own marketplace. **Pin a release** so the instructions cannot change
under you:

```
/plugin marketplace add chittychat-studio/Ballast#v0.1.3
/plugin install ballast@ballast
```

Then run `/ballast:ballast`. The plugin carries the instructions and the catalog, and the skill reads them from the
plugin's own folder.

- The plugin does **not** carry the dashboard page: Claude's plugin directory accepts only text and pictures from
  publishers it has not verified. You get the same results as a table in the chat. For the page, clone the repo.

- Leave auto-update **off** for this marketplace (it is off by default for third-party marketplaces). Update on
  purpose: `/plugin marketplace update ballast`, after you have read what changed.
- A plugin install does not run the checksum and attestation check; that applies to the release zip. The pin is
  your protection, and git tags are not signed yet ([SECURITY.md](../SECURITY.md)). If you want the full check,
  clone and verify instead.
- Copying only `plugin/skills/ballast` into your skills folder also works. The skill then asks where your cloned repo is.
  It never fetches instructions from the web.

## Permissions

- During scanning, read-only commands are fine to allow.
- **During deletion, use a mode that prompts you for shell commands.** Do not use options that skip permission
  prompts (for example the flag named `--dangerously-skip-permissions`) or modes that auto-approve commands.
- If a command is denied, the agent should say exactly what was denied and offer options
  ([permissions.md](../plugin/permissions.md)), not look for another route to the same effect.

## Things to know

- The agent is told to avoid your own running Claude Code sessions. Check the process IDs it proposes to stop.
- Run it from a separate window from the work you care about, so closing apps does not interrupt it.
