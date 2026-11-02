# Protected (Red): never offered for deletion

An agent must never offer, select or run a deletion for anything below. **There are no exceptions**, whatever the
user says (including "it is disposable"). If the user asks, say you will not delete it and explain how they can do it
themselves if they are sure.

A catalog row can name a specific item below Red only where this list says "unless a catalog row names it".

## Personal files and folders

- Documents, Desktop, Pictures, Videos, Music, and the **contents** of Downloads (stale downloads may be *pointed
  out* as large, but never selected).
- Any folder or file whose name suggests it matters: `backup`, `bak`, `archive`, `originals`, `masters`, `photos`,
  `family`, `tax`, `invoices`, `final`, `do not delete`, and similar, in any language you can recognise.
- Cloud-synced or shared locations: OneDrive, Dropbox, Google Drive, iCloud, network shares, mapped drives.
- Other users' profiles, and anything on removable or network drives.

## Identity, secrets and accounts

- SSH, GPG and signing keys (`.ssh`, `.gnupg`), password-manager data, wallets and keystores.
- Recovery codes, two-factor backup codes, and licence keys.
- Credentials and tokens: files named like `credentials`, `auth`, `oauth`, `token`, `.env`, `.netrc`, key files.
- Browser profile data: logins, cookies, history, bookmarks, extensions, local storage. (Browser **caches** may be
  Green in a catalog row; the profile itself is Red.)
- Anything an app needs in order to keep you signed in.

## Work, data and AI memory

- Source code, `.git` folders, and any untracked or modified files in a git repository.
- Databases (`*.db`, `*.sqlite`) and vector stores (for example Chroma, LanceDB, FAISS folders), unless a catalog row
  names that exact item.
- Notebooks (`*.ipynb`) and documents outside a git repository, mail stores (`*.pst`, `*.ost`), and game saves.
- **Virtual disks:** `*.vhd`, `*.vhdx`, `*.vmdk`, `*.qcow2`, including WSL (`ext4.vhdx`) and Docker (`docker_data.vhdx`)
  disks, unless a catalog row names that exact bundle (for example the Cowork VM bundle).
- **Models the user trained or fine-tuned:** checkpoints, LoRA and adapter files. (Models merely *downloaded* are
  Yellow rows, and are removed with the tool's own command first.)
- **AI memory and instruction files:** `memory/` folders, `CLAUDE.md`, `AGENTS.md`, `GEMINI.md`, and their equivalents.
- AI tool configuration: settings files, skills, plugins' configuration, hooks, custom commands and agents, MCP
  server configuration.
- Deliverables the user has named, or the only copy of anything an agent generated.

## System and programs

- Installed programs and their folders (Program Files, `Local\Programs`, package-manager `Packages` folders).
  Removal, if wanted, goes through the vendor's own uninstaller, on the user's request and approval.
- Windows, system and boot folders; the pagefile, hibernation and swap files; the registry.
- Security software and its data.

## Rules for this list

- A folder that *contains* a protected item is not deletable as a whole. Offer only the unprotected children, and
  name what stays (for example the transcripts in a tool folder, but not its `memory/` folder).
- If you cannot tell whether something is protected, treat it as Red.
- Additions to this list are always welcome. Removals need a maintainer's review.
