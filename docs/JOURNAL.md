# Project Journal

A session-by-session log of how this website was built: what was asked, what was
done (including every command), what went wrong, and what comes next.

---

## 2026-10-08 — Session 1: Project rules confirmed and computer set up

**Summary:** Confirmed the project rules and installed every tool needed to build the website.

### What I asked for (in my words)
1. "Can you see the two MD files I have?"
2. "Can we just start with the first prompt, since you already have access to it?"
   (Phase 0 of `PROMPT-PLAYBOOK.md`: summarize the rules in `CLAUDE.md` and add a
   rule about reading the journal at the start of every session.)
3. "Go ahead" (Phase 1.1: check what's installed and install what's missing).
4. "Where exactly would those programs be installed on my machine?"
5. "Go ahead with the install, and also include the three VS Code addons you
   recommended afterwards."
6. "Would there be a way for me to do step 1.2 manually, and log into Github by
   myself instead?"
7. "I logged myself in, but decided to omit setting my email address - I don't
   think it's necessary to add on the commits. Could you check if it worked?"
8. "Check again to see if it works now, with the correct noreply email."
9. "For the repository name, let's use ST-website. Let's keep the repo as public
   for now."

### What was done

**Step 1: Read the starting files.**
The folder `C:\Users\alban\CCProjects` contained two files:
- `CLAUDE.md`: the standing rules Claude Code follows in every session.
- `PROMPT-PLAYBOOK.md`: the list of prompts to use, phase by phase.

**Step 2: Confirmed the rules (Phase 0).**
Claude summarized `CLAUDE.md` in plain language, then added this rule under
"How to work with me":

> At the start of every session, before doing anything else, read docs/JOURNAL.md
> and the latest decision records in docs/decisions/ so you know where we left off.

**Step 3: Checked what was already installed (Phase 1.1).**
In PowerShell, Claude checked for each tool:

```powershell
foreach ($t in 'winget','git','node','npm','code','gh','pnpm') { $c = Get-Command $t -ErrorAction SilentlyContinue; if ($c) { "$t : FOUND at $($c.Source)" } else { "$t : not found" } }
winget --version
```

Result: only **WinGet v1.29.380** (Windows' built-in app installer) was present.
Git, Node.js, VS Code and the GitHub CLI were all missing.

**Step 4: Installed the four tools with WinGet.**
I approved accepting WinGet's source and package agreements, so these flags were
added to skip the "do you agree?" questions:
`--accept-source-agreements --accept-package-agreements`.
`-e` means "match this exact ID" and `--source winget` means "use Microsoft's
official catalogue".

```powershell
winget install --id Git.Git -e --source winget --accept-source-agreements --accept-package-agreements
winget install --id OpenJS.NodeJS.LTS -e --source winget --accept-source-agreements --accept-package-agreements
winget install --id Microsoft.VisualStudioCode -e --source winget --accept-source-agreements --accept-package-agreements
winget install --id GitHub.cli -e --source winget --accept-source-agreements --accept-package-agreements
```

Git and Node.js showed a Windows "allow this app to make changes?" pop-up, and I
clicked **Yes**. Every installer reported "Successfully verified installer hash"
(the download wasn't tampered with) and "Successfully installed".

**Step 5: Checked each tool works.**
The terminal that was already open didn't know about the new programs yet (see
Problems below), so Claude first reloaded the PATH, then printed each version:

```powershell
$env:Path = [Environment]::GetEnvironmentVariable('Path','Machine') + ';' + [Environment]::GetEnvironmentVariable('Path','User')
git --version; node --version; npm --version; code --version; gh --version
```

| Tool | What it's for | Version | Installed at |
|---|---|---|---|
| Git | Records the history of every change; needed for GitHub | 2.55.0 | `C:\Program Files\Git` |
| Node.js (LTS) | Runs modern website tools | 24.20.0 | `C:\Program Files\nodejs` |
| npm | Installs code libraries (comes with Node.js) | 11.19.0 | `C:\Program Files\nodejs` |
| VS Code | Code editor for looking at and editing files | 1.140.0 | `C:\Users\alban\AppData\Local\Programs\Microsoft VS Code` |
| GitHub CLI (`gh`) | Controls GitHub from the terminal (repos, pull requests, issues) | 2.102.0 | `C:\Program Files\GitHub CLI` |

**Step 6: Installed three VS Code add-ons (extensions).**

```powershell
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension EditorConfig.EditorConfig
code --list-extensions --show-versions
```

| Extension | What it does | Version |
|---|---|---|
| ESLint | Underlines likely code mistakes in the editor | 3.0.34 |
| Prettier | Formats code automatically so it looks consistent | 12.4.0 |
| EditorConfig | Keeps spacing and line-ending settings the same across tools | 0.18.2 |

Extensions are stored in `C:\Users\alban\.vscode\extensions`.

**Step 7: Set up Git and logged in to GitHub myself (Phase 1.2).**
I chose to do this step by hand so my login never went through Claude. In a new
terminal I ran:

```powershell
git config --global user.name "N"
gh auth login
```

For `gh auth login` I chose: **GitHub.com** → **HTTPS** → **Yes** (authenticate
Git with my GitHub credentials) → **Login with a web browser**. Then I copied the
one-time code, pasted it in the browser and clicked **Authorize github**.

At first I left out the email, thinking commits didn't need it. Claude checked:

```powershell
gh auth status
git config --global --list
git var GIT_COMMITTER_IDENT
```

The GitHub login worked, but Git refused to make commits without an email (see
Problems below). To keep my real email private, I used GitHub's private
"noreply" address. Claude looked up its exact form from my account details:

```powershell
$u = gh api user | ConvertFrom-Json; "$($u.id)+$($u.login)@users.noreply.github.com"
```

Then I set it myself:

```powershell
git config --global user.email "25772264+AlbanAlla@users.noreply.github.com"
```

Claude re-ran the three checks, and everything passed:
- Logged in to GitHub as **AlbanAlla**, using HTTPS.
- Git's commit identity is `N <25772264+AlbanAlla@users.noreply.github.com>`.
- These settings live in `C:\Users\alban\.gitconfig`. The GitHub login token is
  stored securely in the Windows Credential Manager, not in any project file.

**Step 8: Created the repository and pushed the first commits (Phase 1.3).**
First Claude checked that the name was free on GitHub and looked at Git's
defaults:

```powershell
gh repo view AlbanAlla/ST-website --json name   # failed = name is free
git config --system --get core.autocrlf         # "true": Windows converts line endings
```

Then it turned the folder into a Git repository, with the main branch called
`main`:

```powershell
git init -b main
```

Claude created these files:

| File | Why |
|---|---|
| `.gitignore` | Tells Git never to track secrets (`.env`), installed libraries (`node_modules/`), build output or OS clutter. |
| `.gitattributes` | Stores text files with LF line endings, so Windows and Mac/Linux produce identical history and Git doesn't print line-ending warnings. |
| `README.md` | What the project is, how to run and deploy it (later), and every folder explained. |
| `CHANGELOG.md` | List of visible changes, by version. |
| `docs/decisions/README.md` | How decision records are named, plus a template. (Git can't store an empty folder, so this file also keeps `docs/decisions/` in the repo.) |

Next it created the **public** GitHub repository and connected it as `origin`
(Git's standard name for "the copy on GitHub"):

```powershell
gh repo create ST-website --public --description "A professional website built step by step with Claude Code, with every step documented."
git remote add origin https://github.com/AlbanAlla/ST-website.git
```

Then it made one commit per logical step and pushed them to GitHub:

```powershell
git add .gitignore .gitattributes
git commit -m "chore: add .gitignore and .gitattributes"
git add CLAUDE.md PROMPT-PLAYBOOK.md
git commit -m "docs: add project rules and prompt playbook"
git add README.md CHANGELOG.md docs
git commit -m "docs: add journal, troubleshooting guide, README, changelog and decisions folder"
git push -u origin main
```

`-u` links the local `main` to GitHub's `main`, so later a plain `git push` is
enough.

Repository: https://github.com/AlbanAlla/ST-website

Because the repository is public, anyone can read these files. They contain no
passwords or tokens. The only email in them is the GitHub noreply address.

### Problems and fixes
- **New commands weren't found in the terminal that was already open.**
  A terminal reads the PATH (Windows' list of places to look for programs) once,
  when it opens. Fix: reload the PATH (the `$env:Path = ...` line above), or just
  close the terminal and open a new one. Details in `docs/TROUBLESHOOTING.md`.
- **A "DeprecationWarning: url.parse()" message appeared while installing the
  extensions.** It's a harmless internal notice from VS Code, not an error, and
  every extension installed successfully. Details in `docs/TROUBLESHOOTING.md`.
- **Git said "Committer identity unknown… unable to auto-detect email address".**
  Git stamps every commit with a name and an email, and won't commit without
  both. Fix: set the email, using GitHub's private noreply address to keep my
  real one hidden. Details in `docs/TROUBLESHOOTING.md`.

### What's next
- Phase 1.4: final health check of every tool, confirm pushing to GitHub works,
  and write a "Setup from zero" section in the README.
- Then Phase 2: the interview about what the website should be.
