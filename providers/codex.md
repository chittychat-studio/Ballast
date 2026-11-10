# Using Ballast with Codex CLI

Check Codex CLI's current documentation for exact option names; they change.

1. Clone this repo, pin a version, and read [cleanup.md](../plugin/cleanup.md) and [permissions.md](../plugin/permissions.md).
2. Start Codex in the cloned folder. It reads `AGENTS.md`.
3. Say: **"Read AGENTS.md and run cleanup.md."** For the recurring routine: **"Run weekly.md."**

## Permissions

- Choose an approval mode that **asks before running shell commands** during the delete phase. Avoid modes that
  run commands without asking, or that disable the sandbox.
- If a command is denied or the sandbox blocks it, the agent should say what was blocked and offer options
  ([permissions.md](../plugin/permissions.md)), not look for another route.

## Things to know

- A sandboxed mode may block access to folders outside the project. The agent should explain this and ask you
  to allow access or run the command yourself.
- Codex uses your own account or API key under OpenAI's terms. Ballast sends nothing on its own.
