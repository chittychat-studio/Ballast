# Step 1: preflight

Goal: know the machine, the user's target, and what must not be touched, before measuring anything.

## 1. Consent and backup

Confirm that **both** questions in [AGENTS.md](../AGENTS.md) were asked and answered separately. If the user has no
backup or restore point, say so plainly, suggest making one, and let them choose to continue or stop. Remember that
a backup question answered "yes" does not prove the backup exists. Say what you could not check.

## 2. Are your own prompts on?

Ask the user: "Will your agent ask you before it runs shell commands that delete or stop things?" Deletion needs
that safety net. If the agent runs in a mode that skips permission prompts, or the user cannot confirm, **stop after
the dashboard** and hand over the commands for the user to run themselves.

## 3. Which shell

Name the shell you will use and use it consistently. On Windows use PowerShell explicitly (not a POSIX shell where
`$env:NAME` would be read as plain text). Every path you build must be non-empty and absolute. If a variable could
be empty, check it before use and refuse to continue if it is.

## 4. The machine

Read-only. Windows examples (macOS and Linux: `df -h`, `uname -a`, `id`):

```powershell
Get-PSDrive -PSProvider FileSystem | Select-Object Name, @{n='UsedGB';e={[math]::Round($_.Used/1GB,1)}}, @{n='FreeGB';e={[math]::Round($_.Free/1GB,1)}}
[Security.Principal.WindowsPrincipal]::new([Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole]::Administrator)
```

Record: OS, free space, and whether you are running with administrator rights. If you are **not** elevated, expect
some process details to be hidden. That makes those checks "unknown" (H2), not "clear".

## 5. The target

Ask: "How much free space do you want?" Remember it for the dashboard.

## 6. Your own ancestry (mandatory)

Find out which processes you are running under, so you never stop them or your host:

```powershell
$p = $PID
while ($p) { $x = Get-CimInstance Win32_Process -Filter "ProcessId=$p" -ErrorAction SilentlyContinue; if (-not $x) { break }; "$($x.ProcessId) $($x.Name)"; $p = $x.ParentProcessId }
```

(Unix: `ps -o pid,ppid,comm -p $$` and walk up the parent IDs.)

Write the list down. It, and every process in the same IDE or terminal, is **never stopped** (H6).

## 7. What is running

List AI-tool processes and which are live sessions. Print only name, ID, parent and start time. Do **not** print
whole command lines (they can contain secrets); match them locally and report yes or no.

```powershell
Get-CimInstance Win32_Process | Where-Object { $_.Name -match 'claude|codex|gemini|ollama|cursor|windsurf|antigravity|code' } | Select-Object ProcessId, ParentProcessId, Name, CreationDate
```

Anything running now means its files are **in use**, and related items are Grey.

## 8. Pick the catalog

Choose the `catalog/*.md` files that apply: only the tools actually present on this machine.

## 9. Time and memory limits

Tell the user that scans can be slow and use memory. Run long measurements in the background with a time limit,
stop them when finished, and do not run several heavy scans at once on a struggling machine.
