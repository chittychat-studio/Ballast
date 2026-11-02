# Attribution: did an AI tool make this?

Ballast is about AI-created leftovers, not the user's own files. Rate each candidate:

| Confidence | Signals | Effect |
|---|---|---|
| **High** | Inside a known AI-tool folder; session-ID (GUID) names; `.jsonl` transcripts; a tool's own temp, scratch or cache path; a vendor VM or model bundle | Normal tiering |
| **Medium** | The project contains `CLAUDE.md`, `AGENTS.md` or `GEMINI.md`; git history shows AI co-author trailers; timestamps fall inside known tool sessions; naming typical of agent scratch work | Tier at most Yellow; say what the signal was |
| **Low** | Generic names (`output`, `tmp`, `screenshots`, `test`), or only "it looks generated" | **Grey.** It could be the user's own work |

## Rules

- State the signal you relied on. "High, because it is a session-ID folder inside the tool's data folder".
- Do not infer attribution from file contents. Use names, locations, dates and neighbouring files only.
- An agent-made project that also contains the user's edits, or has no copy elsewhere, is not disposable:
  ask the user, and treat the untracked parts as Red (step 3, E5).
- When two tools could have made it, say so and ask.
