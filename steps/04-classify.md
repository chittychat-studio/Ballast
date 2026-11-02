# Step 4: classify

Turn evidence into a tier. Apply the rules **in order**; the first one that matches wins.

1. **Protected name (E7) matches → Red.** Done. Never selectable, and nothing the user says changes it.
2. **Unsaved work (E5) or cloud/shared (E6) → Red.** No exception. If the user says it is disposable, tell them how
   to remove it by hand.
3. **Is it a program (E3)? → not a cache.** Do not offer folder deletion. If the user wants the program removed,
   that is the vendor's own uninstaller, with their approval (H14). The program's data folders stay Red or Grey
   unless a catalog row says otherwise.
4. **Any check is unknown, errored, or incomplete → Grey.** This includes a process whose path you could not read.
5. **In use now (E2) → Grey.** Never selectable while in use, whatever the catalog row says. Explain what is using it.
6. **Anything depends on it (E4) → Yellow at best**, and name what would break. (An item that is also in use is Grey
   by rule 5 first.)
7. **A catalog row matches, nothing above applies, and "old enough" (see [cleanup.md](../cleanup.md)) →** the row's tier.
8. **No catalog row → Grey.**

**Attribution Low → Grey**, unless rules 1 to 3 already made it Red. A Low attribution never turns a Red item Grey.

## Rules of thumb

- Rebuildable and cheap (cache, build output, download) → Green or Yellow.
- Loses information (chat history, session data) → Yellow, with the loss named.
- Anything an app needs to sign in or remember you → Red.
- Items inside scratch or temporary folders may hold the only copy of something an agent made. Do not treat them as
  disposable without asking (H0).
- When in doubt, go one tier more cautious and ask.

## Output of this step

A list of items, each with: tier, size, maker and attribution, the plain-language checks with what you measured, the
cost to rebuild, and the method that will be used (Recycle Bin or permanent). That list feeds the dashboard.
