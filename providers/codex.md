# Using Ballast with Codex CLI

Check Codex CLI's current documentation for exact option names; they change.

1. Clone this repo, pin a version, and read [cleanup.md](../plugin/cleanup.md) and [permissions.md](../plugin/permissions.md).
2. Start Codex in the cloned folder. It reads `AGENTS.md`.
3. Say: **"Read AGENTS.md and run cleanup.md."** For the recurring routine: **"Run weekly.md."**

## Or install it as a plugin

The repo's `plugin` folder is also a Codex plugin, and the repo is its own marketplace. **Pin a release** so the
instructions cannot change under you:

```
codex plugin marketplace add chittychat-studio/Ballast --ref v0.1.4
```

Then start Codex, open `/plugins`, install Ballast, and ask it to clean up after your AI tools.

- The plugin carries the instructions and the catalog, not the dashboard page. You get the results as a table in
  the chat. For the page, clone the repo.
- Update on purpose, after you have read what changed: `codex plugin marketplace upgrade`.
- A plugin install does not run the checksum and attestation check. If you want that, clone and verify instead
  ([SECURITY.md](../SECURITY.md)).
- This install route was written from Codex's documentation and has **not yet been run** by the maintainers
  (test P4 in [dev/tests.md](../dev/tests.md)). If a step does not work as written, please open an issue.

## Permissions

- Choose an approval mode that **asks before running shell commands** during the delete phase. Avoid modes that
  run commands without asking, or that disable the sandbox.
- If a command is denied or the sandbox blocks it, the agent should say what was blocked and offer options
  ([permissions.md](../plugin/permissions.md)), not look for another route.

## Things to know

- A sandboxed mode may block access to folders outside the project. The agent should explain this and ask you
  to allow access or run the command yourself.
- Codex uses your own account or API key under OpenAI's terms. Ballast sends nothing on its own.
