# Safety

> **Draft v0.1. Not legal advice.** Have a qualified lawyer review this file before relying on it.

Deleting files can cause permanent loss. Ballast is built to make that unlikely, but it cannot make it impossible.

## Before you start

- **Use it only on a computer you own or are authorised to manage.** Do not run it on a work, school or
  shared machine without permission from whoever administers it.
- **Have a backup or restore point** for anything you cannot afford to lose. Your agent will ask you to
  confirm this before any deletion step.
- **Read [cleanup.md](cleanup.md) and [permissions.md](permissions.md).** They are the whole behaviour of
  the tool. Pin the version you read.

## What Ballast does to protect you

1. Read-only until you approve. Scanning never changes anything.
2. Evidence before judgement. Folder names and dates are never enough.
3. Red items (personal files, backups, credentials, browser profiles, memory files, git history) cannot be
   selected. If you want one gone, the agent tells you to do it by hand.
4. Per-item approval, with what it is, why it got its tier, and what it costs to rebuild.
5. Recycle Bin or Trash first where practical. A log of every action.
6. Re-check immediately before each delete, so something that became active since the scan is skipped.
7. The agent protects itself and your other sessions: it never stops its own process tree or another
   agent session without naming it and asking.
8. No bypassing. The agent does not circumvent its permission system, administrator prompts or security software.

## What can still go wrong

- The catalog describes folders that vendors can change at any time. A row can be wrong or out of date.
  Each row carries a status (`active`, `review`, `disabled`); treat `review` rows with extra care.
- Your AI agent can make mistakes. Read each approval request before you say yes.
- Deleted items may not be recoverable, especially permanent deletes of caches and anything on a drive
  where the Recycle Bin is disabled or the item is too large for it.
- Removing an app's data can make that app re-download things, sign you out, or lose session data inside it.
  Yellow items say so.

## No warranty

Ballast is provided "as is", without warranties or conditions of any kind, and the authors are not liable
for loss or damage from its use, to the extent permitted by law (see sections 7 and 8 of the
[Apache License 2.0](LICENSE)). Some places do not allow these limits for consumers; where that is the case,
your local law applies.

## Work and shared computers

A work, school or shared computer may be under retention, legal-hold or administrator policies that forbid
deleting some files, including AI-tool data. Ballast does not know about them. Check with whoever manages the
computer before you clear anything on one.

## Reporting a loss or a bad rule

Open an issue (remove personal paths first). A rule that caused harm is switched to `disabled` in the next
change and noted in the changelog. For security problems, use [SECURITY.md](SECURITY.md) instead.
