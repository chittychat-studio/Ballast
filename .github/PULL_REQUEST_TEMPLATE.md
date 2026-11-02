## What this changes

<!-- One or two sentences. For a catalog row, give the row ID. -->

## Checklist

- [ ] Every commit is signed off (`git commit -s`), which certifies the [Developer Certificate of Origin](https://developercertificate.org/) ([CONTRIBUTING.md](../CONTRIBUTING.md)).
- [ ] If this touches `AGENTS.md`, `cleanup.md`, `permissions.md`, `steps/`, `catalog/`, `dashboard/` or the safety files, I understand it needs a review from a code owner ([CODEOWNERS](CODEOWNERS)). I have explained how it changes what an agent may delete.
- [ ] No scripts, binaries or installers are added.
- [ ] New catalog rows start as `review` and Yellow or Grey, and use `%USERPROFILE%`-style placeholders with no usernames or personal paths. The source is recorded in `catalog/SOURCES.md`.
- [ ] If this changes `dashboard/ballast-dashboard.html`, I re-ran tests D1 to D9 in [dev/tests.md](../dev/tests.md) and the page still makes no network requests.
- [ ] Wording stays plain: no promises that something is "safe" or makes a computer faster.
