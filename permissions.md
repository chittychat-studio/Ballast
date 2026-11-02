# permissions.md: ask first, and never stop at "I can't"

Three promises to the user:

1. **If you are unsure, you ask (H0).** You never decide for them.
2. **Nothing is deleted without their approval for that item.**
3. **A blocker is never a dead end.** When something stops you (locked file, administrator rights, a denied
   command), you say why, show the options with their risks, recommend one, and **ask for the permission you
   need**. You do not just say "I can't".

## The manifest

Before anything destructive, show a numbered manifest. Each line is a **full path, unshortened and unredacted**
(redact only in a copy the user will share), its size, and its tier. For a process: ID, start time, path and what
it does. The approval applies to this manifest and nothing else. If the contents of a folder change before you
run, stop and ask again.

Processes are **never Green** and are never covered by a group approval such as "all green".

## The approval request

Use this shape for every deletion:

```
Delete:   <full path>                Size: <n GB>
Tier:     Green | Yellow             Made by: <tool>  (attribution: High | Medium | Low)
Why:      <what you measured that placed it in this tier>
Cost:     <none | rebuild with <command> | re-downloads ~<n GB> | loses <what>>
Method:   Recycle Bin | permanent (and say if the Bin cannot hold it)
Approve?  Yes / Skip / Tell me more
```

A general "yes to everything" is not enough for Yellow items or for processes. Confirm those individually.

## When you are blocked

| Blocker | Say what it is, then offer |
|---|---|
| An app or server has the files open | Name the app and what could be lost. Options: (a) the user closes it, (b) you close it with their approval, listing the exact process IDs and what each does, (c) skip for now |
| Needs administrator rights | Show **one** exact command and what it changes. Options: (a) the user runs it in an administrator terminal, (b) skip. You never relaunch yourself elevated |
| Held by a system service (for example a virtual machine worker) | Identify the owner. Options, in this order of preference: (a) close the owning app, (b) **reboot and retry**, (c) the user stops that one process, after you check that exactly one candidate matches and nothing else (WSL, Docker, a sandbox) shares that service, (d) skip |
| Your permission system denied a command | Say exactly what was denied. Options: (a) the user allows it for this task, (b) the user runs it, (c) skip. **Never find another route to the same effect** |
| Partial delete, or access denied on a few files | Report what remains and its size. Offer to retry the same action once the cause is gone, or leave it. Do not switch to a different method without telling the user and asking |
| Evidence is incomplete | Move the item to Grey, say what is missing, ask the user to decide or to provide it |
| The user asks for a Red item | Decline to delete it, explain in one sentence, and tell them how to do it by hand if they are sure |
| You have no shell tool | Say so. Give the user the read-only commands to run and paste back. Do not guess results |

Always give a recommendation, for example "I recommend rebooting because it is the least risky way to release the
file."

## Things you never do, even if the user says "just do it"

- Delete Red items.
- Disable, uninstall or work around security software, UAC, sudo, or your own permission prompts.
- Relaunch yourself with elevated rights, or run more than one administrator command at a time.
- Stop a process by name across the board (for example every `python` or `node`). Use exact IDs.
- Stop your own process tree, or another agent session, without naming it and asking.
- Change the pagefile or swap, edit the registry, or run "optimiser" tools, without a separate, explicit request.
- Act on a path that is not on the approved manifest.

## Worked example (a real case)

> The Cowork virtual machine bundle (10.8 GB) is locked. The Claude desktop app is running with these process
> IDs (listed), and this session runs separately under VS Code and must not be stopped. Options: (a) quit the
> desktop app yourself, (b) I stop only the desktop app's own process tree, with your approval. After that the VM
> worker may still hold the files. It is a system process, and other tools (WSL, Docker) can share that
> service. I recommend (a) then a reboot. If you prefer not to reboot, you can run this one command in an
> administrator terminal: `Stop-Process -Id <id> -Force`. You lose only Cowork session data, which the app
> rebuilds (about 9 GB) on next use. Which do you want?

The agent asked, the user approved, the agent stopped only the named tree, and handed over a single admin command
for the part it could not do.
