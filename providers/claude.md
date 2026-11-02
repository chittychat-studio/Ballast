# Using Ballast with Claude Code

Check Claude Code's current documentation for exact option names; they change.

1. Clone this repo, pin a version, and read [cleanup.md](../cleanup.md) and [permissions.md](../permissions.md).
2. Open Claude Code in the cloned folder. It reads `CLAUDE.md`, which points to `AGENTS.md`.
3. Say: **"Read AGENTS.md and run cleanup.md."** For the recurring routine: **"Run weekly.md."**

Alternatively copy `skills/ballast` into your Claude Code skills folder. The skill still needs the cloned repo
to exist; it will ask you where it is. It never fetches instructions from the web.

## Permissions

- During scanning, read-only commands are fine to allow.
- **During deletion, use a mode that prompts you for shell commands.** Do not use options that skip permission
  prompts (for example the flag named `--dangerously-skip-permissions`) or modes that auto-approve commands.
- If a command is denied, the agent should say exactly what was denied and offer options
  ([permissions.md](../permissions.md)), not look for another route to the same effect.

## Things to know

- The agent is told to avoid your own running Claude Code sessions. Check the process IDs it proposes to stop.
- Run it from a separate window from the work you care about, so closing apps does not interrupt it.
