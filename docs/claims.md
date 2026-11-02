# Claims register

Every public claim in this repo must map to something that enforces or proves it. Before a release, a maintainer
walks this table. If a claim has no enforcement, remove the claim or mark it "planned".

| Claim (where made) | Enforced by | How to check |
|---|---|---|
| If the agent is unsure it asks; it never decides for the user (README, AGENTS) | cleanup.md H0; permissions.md | Read H0 and the approval request format |
| Nothing is deleted without approval for that item (README, SAFETY) | cleanup.md H0, H1, H9; permissions.md; steps/06 | Run the fixtures in `dev/` (planned). Read steps/06 |
| Personal files, backups, credentials, browser profiles and memory files are never deleted (README) | catalog/_protected.md; cleanup.md H3; steps/04 rules 1 and 2 | Check no catalog row's path matches a protected pattern |
| "Ballast collects nothing" (PRIVACY) | The repo has no servers; the dashboard page has a Content-Security-Policy with no network access | Search the repo for any URL the agent or page is told to fetch or post to |
| "Nothing to install and no program to run" (README) | CONTRIBUTING ground rules | List every file that is not `.md` and confirm only LICENSE, NOTICE, the dashboard page and the logo exist |
| The dashboard page cannot delete anything and runs no network requests (README, dashboard.md) | The page's code and its Content-Security-Policy | Open it and read it; run the hostile-data tests: injected markup, script tags, text-direction characters, invalid tier, missing data |
| Red items cannot be selected, whatever the data says (dashboard.md) | The page forces Grey and Red to "Not offered" and gives them no Clear control | Feed it a Red item marked `Permanent` and confirm there is no radio |
| Never works around the permission system (README) | cleanup.md H7; permissions.md "never" list | Read permissions.md; test with a denied command |
| Never just says "I can't" (README) | permissions.md blocker table | Every blocker row offers options and asks for the permission needed |
| Recycle Bin or Trash first where it really works (README) | cleanup.md H10; steps/06 section 5 | Read steps/06; the log must say what actually happened |
| Reads names, sizes, dates and extensions only (PRIVACY) | cleanup.md H8; steps/02; _attribution.md | Search for any instruction to open file contents |
| Items are "classified", never promised "safe" or "faster" (README) | cleanup.md H11 | Search the repo for banned words (below) |
| Rows are marked `active` only after confirmation (catalog) | catalog/README.md Status; SOURCES.md | Each `active` row has a Verified line |
| Signed release tags, published checksums, required reviews (SECURITY) | **Planned.** Not yet in place | SECURITY.md says "planned" next to each |
| "A cloned repository can be tampered with, so users pin and check a version" (comparison, SECURITY) | AGENTS.md integrity check (shows the version, refuses a dirty tree) | Read AGENTS.md section "Do this first" |

## Banned words check

Before a release, search user-facing files for these and justify or remove each hit: `safe to delete`, `safe to
remove`, `speed up`, `speeds up`, `boost`, `optimis`, `optimiz`, `guarantee`, `100%`, `no risk`. Negations in
policy text ("never promises it is safe") and quotations of other projects' wording are fine.

Also search for the phrases `Markdown only` and `nothing to run`, and confirm each use is still true.
