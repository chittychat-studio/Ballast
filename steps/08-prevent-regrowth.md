# Step 8: stop it coming back

Cleaning is temporary if the leftovers regrow. For each source that mattered, offer one prevention step. **Offer, do not
apply.** Settings belong to the user and to the tool's own documentation. Check that documentation for the
current setting names, because they change.

| Source | Prevention to suggest |
|---|---|
| Agent chat transcripts | Use the tool's transcript-retention setting if it has one; clear old sessions on a schedule |
| Virtual machine images (Cowork) | Close the app and its VM when you finish a Cowork session; expect the VM to be rebuilt on next use |
| Local model files | Keep only models you use; remove others with the tool's own command first; consider a larger drive or a different models folder |
| Headless browsers and test browsers | Close them in your scripts, set a time limit on automation, and check for stragglers after runs |
| Dev servers started by agents | Stop servers when the task ends; ask your agent to list what it started |
| Scratch projects and dependencies (`node_modules`, `.venv`) | Create scratch work in one disposable folder; delete it when done |
| Generated media and outputs | Keep final deliverables in a named folder you will recognise. Anything outside it may be listed for clearing later, and the agent will still ask first |

For [weekly.md](../weekly.md), tie the suggestion to the fastest-growing item in the growth table.

Never claim a prevention step "fixes" the problem; say it should slow regrowth.
