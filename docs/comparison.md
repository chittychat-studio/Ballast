# Comparison with similar tools

Project details for the two Sweepwise repositories were read from their public READMEs, PRIVACY, SECURITY,
CONTRIBUTING and LICENSE files and docs listings on **2026-11-02**. Entries for other tools are from general
knowledge and should be re-checked before you quote them. Neither Sweepwise project is affiliated with Ballast.

| Tool | Type | Licence | What it does well | Where Ballast differs |
|---|---|---|---|---|
| **sweepwise/sweepwise** | macOS menu-bar app (Swift) | MIT | Risk classes A to D with "why" and restore notes; Trash by default; optional explanations from your own local AI CLI; asks before saving a learned rule; signed and notarized releases | Ballast is instructions plus one static dashboard page, runs inside your own agent, covers Windows first, focuses on AI-tool leftovers, and has an explicit ask-and-workaround protocol |
| **AlbertanCoder/sweepwise** | Desktop app for Windows, Linux, Mac | GPL-3.0 | Undo records, restore points before changes, clear PRIVACY and SECURITY files, optional AI with your own key, claims-checking tooling | Ballast ships no installer or program (one static page that runs only in your browser); the AI is the interface; never makes speed claims |
| BleachBit | Open-source cleaner | GPL | Rule-based cleaners, preview before delete | No evidence checks or tiers; Ballast adds both and is AI-tool specific |
| CCleaner | Commercial cleaner | Proprietary | One-click flow | A 2017 compromised release and later privacy controversies; Ballast has no installer, but a cloned repository can be tampered with too, so users pin and check a version |
| Windows Storage Sense, Disk Cleanup | Built in | n/a | Conservative, trusted | Does not reach AI-tool folders, projects or VM images |
| WinDirStat, WizTree, TreeSize | Space visualisers | various | Fast, clear treemaps | Show where space goes, not what can be removed |
| Czkawka, dupeGuru | Duplicate finders | various | Duplicates | Different problem |

## What Ballast borrows

- **Show why, and how to rebuild, before any delete** (Sweepwise, macOS).
- **Trash or Recycle Bin by default** (Sweepwise, macOS).
- **Ask every time before remembering a rule** (Sweepwise, macOS).
- **A privacy table of exactly what can leave the machine** (Sweepwise, Windows/Linux/Mac).
- **A security file that lists design safeguards** (Sweepwise, Windows/Linux/Mac).
- **A claims check**: every public claim maps to something that enforces it ([claims.md](claims.md)).

Nothing is copied from either project's text or code.

## What is different on purpose

- **Instructions plus one static page.** No installer, no binary, no auto-update. The attack surface is the
  instruction files and the dashboard page, so both are reviewed like code.
- **Evidence before judgement.** Newest file inside, running processes, package manifests, git state.
- **A hard-locked Red tier.** Personal files and backups cannot be selected, even by asking.
- **"I can't" is never the end.** See [permissions.md](../plugin/permissions.md).
- **Focus.** AI-tool leftovers, including memory held by processes the tools leave running.
