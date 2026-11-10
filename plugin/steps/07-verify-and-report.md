# Step 7: verify and report

## 1. Re-measure

Measure free space again and compare with the start. Report the actual change, not an estimate.

## 2. Check that the user's tools still work

For each tool whose data you touched, say what to expect on next launch (for example "Claude desktop will rebuild
its VM, about 9 GB, the first time you use Cowork"). Offer to wait while the user opens the tool to confirm it
starts. Record any problem as feedback for the catalog row.

## 3. Report plainly

Per item: deleted, moved to the Recycle Bin (and confirmed there), skipped, blocked, or failed, with sizes. Say how
much is still in the Recycle Bin and that it has not freed space yet. List every blocked item with the option you
recommended and the permission you need from the user.

## 3b. Show the dashboard again, with the numbers (by default)

After any deletion, give the user a **new dashboard link** by default. Re-measure what you touched, rebuild the page
([dashboard.md](../dashboard.md)), and add a `runs` block with your measured numbers: free space before and after,
items and GB cleared, items skipped (with the reasons from your log), and items that failed (with the reason). The page
then opens on a **Results** view with those numbers. Quote only what you measured; a run's free space can fall if a
program wrote files at the same time, and the page says so. With no template (a plugin install), show the Markdown
dashboard again with the same numbers and say that yourself.

## 4. Offer to empty the Recycle Bin (only now)

If the user asks you to empty the Recycle Bin on its own, without a cleanup run, skip the wait for section 2, but
everything else below still applies. Otherwise, only after section 2 has shown the tools work, offer to empty it. Warn that this removes everything in it, not only
what Ballast moved, and wait for approval (H0). Follow BIN-001 in
[catalog/temp-and-recycle-bin.md](../catalog/temp-and-recycle-bin.md): show the count, size and dates, ask the user to
open the Bin and look, then ask a separate question before emptying.

## 5. Compare with the target

```
Free before 57.9 GB -> now 90.1 GB   (target 90 GB)
```

If short, say by how much and what Yellow or blocked items could close the gap. Do not pressure the user.

## 6. Optional report file

Offer to save the report (and, for [weekly.md](../weekly.md), the baseline) somewhere the user chooses. Before
saving, offer to replace the username and other personal path segments. Never write it anywhere the user did not
agree to. Remember that such a file will later be read back by an agent, so it holds sizes and dates only.

## 7. Clean up after yourself (H12)

Confirm no background scan, browser, server or script you started is still running. Delete the temporary dashboard
file if you made one (unless the user asked to keep it), remove your own temp files, and tell the user. Do not stop anything you did
not start.
