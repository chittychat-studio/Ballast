# Changelog

All notable changes to Ballast are listed here, newest first. The format follows
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/). A catalog row that caused harm and was switched to
`disabled` is noted here too (see [SAFETY.md](SAFETY.md)).

## [Unreleased]

Nothing yet.

## [0.1.3] - 2026-11-10

Version 0.1.2 was merged but never tagged, so 0.1.3 is the first release after 0.1.1.

### Changed

- **The instructions moved into the [`plugin`](plugin) folder**, which is now the whole Claude Code plugin:
  `AGENTS.md`, `cleanup.md`, `permissions.md`, `weekly.md`, `dashboard.md`, `steps/`, `catalog/`, the skill and
  the plugin manifest. The root [AGENTS.md](AGENTS.md) is now a short pointer to
  [plugin/AGENTS.md](plugin/AGENTS.md), so "Read AGENTS.md and run cleanup.md" still works in a clone. The rules
  for what an agent may delete have not changed.
- **A plugin install no longer includes the dashboard page.** Claude's plugin directory refused 0.1.2 because it
  accepts only text and picture files from publishers it has not verified, and the page is HTML. A plugin install
  now shows the results as a table in the chat ([dashboard.md](plugin/dashboard.md)); the agent is told never to
  search for, download or write a page itself. A clone still has the page.
- The plugin's icon is now a PNG inside the plugin folder (`plugin/ballast-icon.png`); the SVG icon added in
  0.1.2 is removed.
- The install instructions and the plugin manifest point at `v0.1.3`.

### Added

- `plugin/README.md` (what the plugin is, for its directory listing) and copies of the licence and notice in
  `plugin/`.
- After a cleanup, the table in the chat shows the results (space before and after, items cleared, skipped and
  failed), as the page's Results view does.

## [0.1.2] - 2026-11-10

### Changed

- The install instructions and the plugin manifest now point at `v0.1.2`.

### Added

- Listing details in the plugin manifest for Claude's plugin directory: a display name, an icon, and links to the
  documentation, support and privacy pages, and a contact email. Nothing about what the plugin does has changed.
- A square icon, `dashboard/ballast-icon.svg` (the mark from the logo, without the word).
- Three example prompts and a Support section in the README.

## [0.1.1] - 2026-11-03

### Notice about the v0.1.0 tag

The `v0.1.0` tag was moved to a newer commit several times on 2 November 2026, while the first release was still
being finished. That is the opposite of what pinning a release is meant to give you. Anyone who pinned `v0.1.0`
on that day may hold different files from someone who pinned it later. If you need to know what you have, check
the release checksum and attestation ([how](SECURITY.md#verifying-a-release)), or wait for the next release.

**From the next release onwards, tags are never moved or deleted.** A fix ships as a new version. The repository
now has a tag ruleset that blocks updating or deleting any `v*` tag.

### Changed

- The install instructions and the plugin manifest now point at `v0.1.1`, the first tag that is covered by the
  tag ruleset. `v0.1.0` stays in place and is never moved again.
- Catalog row CD-002 (Claude desktop browser-style caches) is now Yellow instead of Green. Its status is still
  `review`, and `review` rows must be Yellow or Grey ([catalog/README.md](plugin/catalog/README.md)). The example item in
  [dashboard.md](plugin/dashboard.md) that cites CD-002 uses the same tier.
- README and the claims register list the new non-Markdown files, so the claim "no program to install or run"
  stays checkable.

### Added

- This changelog.
- [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) (Contributor Covenant 2.1).
- Issue forms for a bug report, a harmful or wrong catalog row, and a new catalog row proposal, and a link to
  private vulnerability reporting for security problems (`.github/ISSUE_TEMPLATE/`).
- A pull request template with the DCO sign-off, code-owner review, no-scripts and dashboard-test reminders.
- Dependabot updates for the GitHub Actions the release workflow uses (they are pinned to commit SHAs).
- `.gitignore` and `.editorconfig`.
- "Tags are never moved" in [SECURITY.md](SECURITY.md).

## [0.1.0] - 2026-11-02

First release.

### Added

- The instruction set: [cleanup.md](plugin/cleanup.md) (rules and flow), [permissions.md](plugin/permissions.md) (ask-first
  protocol and the blocked-item playbook), [weekly.md](plugin/weekly.md), and the eight steps in [steps/](plugin/steps).
- The catalog of known AI leftovers: Claude Code, the Claude desktop app and Cowork, orphan processes and the memory
  they hold, graphics memory (VRAM), the Temp folder and Recycle Bin, browser, Office and Windows caches, Codex,
  Gemini, local models and image tools. Starter rows for macOS and Linux are all `planned` and Grey. The Red list
  of never-deletable items is in [catalog/_protected.md](plugin/catalog/_protected.md).
- A static dashboard template ([dashboard/ballast-dashboard.html](dashboard/ballast-dashboard.html)) and its spec
  ([dashboard.md](plugin/dashboard.md)): Overview, tabs by tier, a Results view, a free-space gauge and light and dark
  themes. It makes no network requests and cannot delete anything.
- Sample pictures of the dashboard and the logo.
- Notes for Claude Code, Gemini CLI, Codex CLI and Antigravity ([providers/](providers)), and the Claude Code plugin
  packaging (`.claude-plugin/` and the `ballast` skill).
- Safety, privacy and security documents, a claims register, a comparison with similar tools, and the maintainer
  tests with real results ([dev/](dev)).
- A release workflow that builds a zip, a SHA-256 checksum file and a signed build attestation when a version tag
  is pushed.

### Notes

- Windows 11 is the first supported system. Rows from one real machine are marked `review`.
