# Claims register

Every public claim in this repo must map to something that enforces or proves it. Before a release, a maintainer
walks this table. If a claim has no enforcement, remove the claim or mark it "planned".

| Claim (where made) | Enforced by | How to check |
|---|---|---|
| If the agent is unsure it asks; it never decides for the user (README, AGENTS) | cleanup.md H0; permissions.md | Read H0 and the approval request format |
| Nothing is deleted without approval for that item (README, SAFETY) | cleanup.md H0, H1, H9; permissions.md; steps/06 | Run the fixtures in `dev/` (planned). Read steps/06 |
| Personal files, backups, credentials, browser profiles and memory files are never deleted (README) | catalog/_protected.md; cleanup.md H3; steps/04 rules 1 and 2 | Check no catalog row's path matches a protected pattern |
| "Ballast collects nothing" (PRIVACY) | The repo has no servers; the dashboard page has a Content-Security-Policy with no network access | Search the repo for any URL the agent or page is told to fetch or post to |
| "No program to install or run" (README) | CONTRIBUTING ground rules | List every file that is not `.md` and confirm only LICENSE, NOTICE, the dashboard page, the logo, the two sample pictures, the plugin's PNG icon, the JSON files `.claude-plugin/marketplace.json` and `plugin/.claude-plugin/plugin.json`, the copies of LICENSE and NOTICE in `plugin/`, `.gitignore`, `.editorconfig`, and under `.github/` only `CODEOWNERS`, `dependabot.yml`, `workflows/release.yml`, `PULL_REQUEST_TEMPLATE.md` and the YAML files in `ISSUE_TEMPLATE/` exist (the plugin manifests are metadata, and the rest are repository, editor and issue-form settings; none is something users run). `CHANGELOG.md` and `CODE_OF_CONDUCT.md` are Markdown |
| The plugin install is pinned to a release and never fetches instructions from the web (README, providers/claude.md) | The documented `#<tag>` form of `/plugin marketplace add`; SKILL.md reads only the plugin's own folder | Read SKILL.md; `claude plugin validate .` and `claude plugin validate plugin --strict` pass. List the files in `plugin/` and confirm each is Markdown, plain text, JSON or PNG, and that no link in them leaves the folder. A plugin install is **not** covered by the checksum or attestation, and README says so |
| The dashboard page cannot delete anything and runs no network requests (README, dashboard.md) | The page's code and its Content-Security-Policy | Open it and read it; run the hostile-data tests: injected markup, script tags, text-direction characters, invalid tier, missing data |
| Red items cannot be selected, whatever the data says (dashboard.md) | The page forces Grey and Red to "Not offered" and gives them no Clear control | Feed it a Red item marked `Permanent` and confirm there is no radio |
| Never works around the permission system (README) | cleanup.md H7; permissions.md "never" list | Read permissions.md; test with a denied command |
| Never just says "I can't" (README) | permissions.md blocker table | Every blocker row offers options and asks for the permission needed |
| Recycle Bin or Trash first where it really works (README) | cleanup.md H10; steps/06 section 5 | Read steps/06; the log must say what actually happened |
| Reads names, sizes, dates and extensions only (PRIVACY) | cleanup.md H8; steps/02; _attribution.md | Search for any instruction to open file contents |
| Items are "classified", never promised "safe" or "faster" (README) | cleanup.md H11 | Search the repo for banned words (below) |
| Rows are marked `active` only after confirmation (catalog) | catalog/README.md Status; SOURCES.md | Each `active` row has a Verified line |
| Changes to instruction files and the dashboard need a pull request and a code-owner review (SECURITY) | Branch protection on `main` plus [.github/CODEOWNERS](../.github/CODEOWNERS). A maintainer with admin rights can bypass it, and SECURITY.md says so | `gh api repos/chittychat-studio/Ballast/branches/main/protection` |
| Every release has a SHA-256 checksum file and a build attestation (SECURITY) | [.github/workflows/release.yml](../.github/workflows/release.yml), actions pinned to commit SHAs | `gh release view <tag>` lists the zip and `SHA256SUMS`; `gh attestation verify <zip> --repo chittychat-studio/Ballast` passes |
| Release tags are never moved or deleted, from the next release (SECURITY, CHANGELOG) | A repository ruleset on `refs/tags/v*` that blocks update and deletion, with no bypass. `v0.1.0` was moved before it existed, and CHANGELOG.md says so | `gh api repos/chittychat-studio/Ballast/rulesets` lists "Protect release tags" as `active` |
| Signed git tags (SECURITY) | **Planned.** Needs a maintainer signing key | SECURITY.md says "planned" |
| macOS and Linux rows (README, catalog) | catalog/macos.md and catalog/linux.md say every row is `planned` and Grey because none was observed | Check no row there is Yellow or Green or `active` |
| Graphics memory (VRAM) is read, never changed, and only measured numbers are shown (README, catalog/gpu-memory.md) | gpu-memory.md rules; cleanup.md H0, H13; the page hides the graphics line when numbers are missing | Read gpu-memory.md; run dev/tests.md D5; confirm no command there stops a process or resets a driver without approval |
| Temp, the Recycle Bin and browser caches are covered with the same ask-first rules; the Windows Installer cache is shown but never offered (README, catalog) | catalog/temp-and-recycle-bin.md (group rule, two-step Bin emptying); catalog/windows-and-app-caches.md; _protected.md; steps/06 | Read those files; C10 to C13 in dev/tests.md. Emptying the Recycle Bin and deleting Temp through Ballast are **not yet tested** (A12, A13) |
| The safety tests are written down with real results (dev) | [dev/tests.md](../dev/tests.md) | Each "Result" is either a measured outcome with a date and machine, or "Not yet run" |
| "A cloned repository can be tampered with, so users pin and check a version" (comparison, SECURITY) | AGENTS.md integrity check (shows the version, refuses a dirty tree) | Read AGENTS.md section "Do this first" |

## Banned words check

Before a release, search user-facing files for these and justify or remove each hit: `safe to delete`, `safe to
remove`, `speed up`, `speeds up`, `boost`, `optimis`, `optimiz`, `guarantee`, `100%`, `no risk`. Negations in
policy text ("never promises it is safe") and quotations of other projects' wording are fine.

Also search for the phrases `Markdown only` and `nothing to run`, and confirm each use is still true.
