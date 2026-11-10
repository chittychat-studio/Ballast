# Using Ballast with Gemini CLI

Check Gemini CLI's current documentation for exact option names; they change.

1. Clone this repo, pin a version, and read [cleanup.md](../plugin/cleanup.md) and [permissions.md](../plugin/permissions.md).
2. Start Gemini CLI in the cloned folder. It reads `GEMINI.md`, which points to `AGENTS.md`.
3. Say: **"Read AGENTS.md and run cleanup.md."** For the recurring routine: **"Run weekly.md."**

## Permissions

- Keep shell-command approval on during the delete phase. Do not use any "auto-approve" or "yolo"-style mode.
- If a command is denied, the agent should say what was denied and offer options
  ([permissions.md](../plugin/permissions.md)) rather than work around it.

## Things to know

- The agent is told never to stop its own process tree. Check the process IDs it proposes to stop.
- Gemini CLI uses your own account or API key under Google's terms. Ballast sends nothing on its own.
