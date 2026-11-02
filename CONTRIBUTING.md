# Contributing

Thanks for helping. Ballast only works if its rules are accurate and cautious.

## Ground rules

- **Instructions in Markdown, plus one dashboard template, a logo and the two plugin manifests in
  `.claude-plugin/` (plain JSON metadata), plus repository settings files (`.github/` issue forms, pull request
  template, Dependabot and workflow files, `.gitignore`, `.editorconfig`).** No scripts, binaries, installers or build steps in the user-facing repo. Example commands inside `.md` files must be short and clearly labelled, and
  destructive ones must sit behind the approval steps.
- **The dashboard page is code.** Changes to `dashboard/ballast-dashboard.html` need a maintainer review. It must stay
  dependency-free, make no network requests, keep its Content-Security-Policy, build everything with text nodes (never
  `innerHTML`), and validate and sanitise every field. Re-run the dashboard tests D1 to D9 in
  [dev/tests.md](dev/tests.md) (injected markup, script tags, text-direction characters, invalid tiers) before
  submitting.
- **Write your own rules.** Do not copy rules from other cleaners or rule databases without checking
  their licence. GPL-licensed lists in particular cannot be copied into this Apache-2.0 repo.
  Record where every rule came from in [catalog/SOURCES.md](catalog/SOURCES.md).
- **Sign off your commits** (`git commit -s`). That certifies the
  [Developer Certificate of Origin](https://developercertificate.org/): you wrote the contribution or
  have the right to submit it under this repo's licence.
- **Evidence over assumption.** A rule must say what to check before deleting, not just where the folder is.

## Adding or changing a catalog row

1. Copy the row format from [catalog/README.md](catalog/README.md).
2. Fill every column, including *Verified* (date, OS, tool version) and *Rebuild/cost*.
3. New rows start with status `review` and tier **Yellow or Grey**. A row becomes `active` or Green only after
   it has been observed to work, with the tool still functioning afterwards, and a maintainer has recorded that.
4. Never add anything to the Red list's contents as deletable. Additions to [catalog/_protected.md](catalog/_protected.md) are welcome.
5. Remove usernames and personal paths. Use `%USERPROFILE%`, `%LOCALAPPDATA%`, `~`.

## Changing core instructions

Changes to `AGENTS.md`, `cleanup.md`, `permissions.md`, `steps/` or the safety files need a maintainer
review and an explanation of how the change affects what an agent may delete.

## Reporting a harmful rule

Open an issue with the row ID (there is a form for it). See [SAFETY.md](SAFETY.md).

## Conduct

Everyone taking part follows the [Code of Conduct](CODE_OF_CONDUCT.md). Changes are listed in
[CHANGELOG.md](CHANGELOG.md); add a line under Unreleased when your change is user-visible.
