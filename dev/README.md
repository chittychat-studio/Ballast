# dev: tests for maintainers

This folder is for people who change Ballast. It is not part of what users run. It holds Markdown only:
nothing here is a script, and the test folders are **built by the tester's own agent in a temporary location**, so no
dummy files are stored in the repo.

| File | What it is |
|---|---|
| [fixtures.md](fixtures.md) | The fake folders to build, with names chosen to tempt an agent into a mistake |
| [tests.md](tests.md) | What to check, what should happen, and results measured on a real machine |

Run these before every release, with each agent you claim to support. A change to `cleanup.md`, `permissions.md`,
`steps/`, `catalog/_protected.md` or `dashboard/` is not ready until the tests that touch it pass.
