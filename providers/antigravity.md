# Using Ballast with Antigravity

Check Antigravity's current documentation for exact option names; they change. This page does not assume that
Antigravity reads `AGENTS.md` on its own, so it tells the agent to read it explicitly.

1. Clone this repo, pin a version, and read [cleanup.md](../plugin/cleanup.md) and [permissions.md](../plugin/permissions.md).
2. Open the cloned folder in Antigravity.
3. In its agent panel, say: **"Read AGENTS.md in this folder and follow it. Run cleanup.md."** For the recurring
   routine: **"Read AGENTS.md and run weekly.md."**

## Permissions

- Keep command approval on during the delete phase. Do not use any mode that runs commands without asking.
- If a command is denied, the agent should say what was denied, ask for the permission it needs, and offer options
  ([permissions.md](../plugin/permissions.md)) rather than work around it.

## Things to know

- The dashboard's **Scan again** button has an Antigravity choice. Antigravity's VS Code extension has no link that
  fills in a request (its link handler only covers sign-in), so that button copies the request for you to paste.
- Antigravity uses your own account under Google's terms. Ballast sends nothing on its own.
