# Legal notes

> **Not legal advice.** Written by a non-lawyer to prepare for a proper review. Nothing here guarantees
> that anyone will not make a claim; it records choices intended to reduce and weaken claims.

## How two comparable projects handle legal matters

Read on 2026-11-02 from public files only: READMEs, PRIVACY, SECURITY, CONTRIBUTING and LICENSE where present,
and docs listings. I did not read their source code, website terms or installer terms. "Not found" means not
found in the files I read.

| Area | sweepwise/sweepwise (macOS, MIT) | AlbertanCoder/sweepwise (Windows/Linux/Mac, GPL-3.0) |
|---|---|---|
| Licence and warranty | MIT licence. README points to it | GPL-3.0 with its warranty disclaimer and limitation of liability; README adds "absolutely no warranty, to the extent permitted by law" |
| Privacy document | Not found; README describes local behaviour | `PRIVACY.md`: "collects nothing"; a table of what can leave the machine and when; where keys are stored; a separate section on the website help chat |
| Security document | Not found in root; docs cover notarisation and App Store notes | `SECURITY.md`: private reporting, supported versions, design safeguards (fixed list of admin steps, Undo written before the next change) |
| Contribution terms | Not found | Contributions are licensed under the project's GPL licence. No sign-off or contributor agreement seen |
| Provider terms and the AI feature | Uses the user's own installed `claude`, `codex` or `gemini` CLI under their existing subscription; no keys stored. Its own App Store notes flag this as a likely review objection and a sandbox blocker | Optional AI with the user's own Anthropic or OpenAI key. Sends names, sizes and dates, "never what is inside a file"; private-looking names are removed by a word list |
| Safety design | Trash by default; permanent delete opt-in for items over 2 GB; risk classes A to D; consent before saving a learned rule | Restore point before changes; Undo; "changes you approve can be undone" with named exceptions |
| Affiliation and trademark wording | Not found for the AI providers it names | Not found for the providers it names |
| Marketing claims | Describes behaviour; calls items "safe or risky" | Promotes "speeds up your PC" and a "Speed Boost" feature. File names suggest an automated claims check (`check_claims.py`, `claims.json`); I did not read them |

## What Ballast does about each area

- **Licence:** Apache-2.0, with its disclaimer of warranty (section 7) and limitation of liability (section 8),
  repeated in plain language in [SAFETY.md](../SAFETY.md) and in the agent's first message every session.
- **Privacy:** [PRIVACY.md](../PRIVACY.md) with a "what can leave" table, adapted in structure only, plus the
  honest point that your AI provider sees what your agent reads.
- **Security:** [SECURITY.md](../SECURITY.md) lists threats and defences, and treats instruction files as code.
- **Contributions:** Developer Certificate of Origin sign-off, and a rule against copying rule sets.
- **Provider terms:** the user runs their own agent under their own account. Ballast never proxies, resells, or
  reuses anyone's login. Check each provider's current terms before launch.
- **Trademarks:** names appear only to identify tools and folders; a "not affiliated or endorsed" line is in
  the README and NOTICE; no logos; a neutral repository name.
- **Claims:** no speed or safety promises. Every public claim maps to an enforcing rule in [claims.md](claims.md).
- **No installers or binaries:** the repository is instructions plus one static dashboard page that runs only in the
  user's browser. That reduces malware-flag and tampered-installer exposure but does not remove it, because a cloned
  repository can be altered. See [SECURITY.md](../SECURITY.md).

## Known gaps

- No lawyer has reviewed any text. The disclaimers may not hold against gross negligence or consumer law in
  some places (for example parts of the EU and UK).
- Provider terms are not summarised here. Read the current terms of each AI provider you mention.
- There is no automated test yet proving the Red list holds against a prompt-injection fixture (planned in `dev/`).
- No entity or insurance is set up. Consider publishing through an organisation, and ask about tech E&O cover.

## Questions for a lawyer

1. Do the warranty disclaimer and limitation of liability hold up where you expect users (US, EU, UK, India)?
2. Is the "not affiliated" wording enough for the AI-provider names in the catalog and README?
3. Is a contributor agreement needed beyond a DCO sign-off?
4. Do you need an LLC or insurance, especially if you ever charge for any part of this?
5. Do any provider terms restrict a project of this kind?
