# ST-website

A professional website built step by step with [Claude Code](https://claude.com/claude-code),
with every step documented. The project's history will become a
"from nothing to a finished website" tutorial.

**Status:** Phase 1 (setup) complete. The website itself hasn't been
planned or built yet. See [docs/JOURNAL.md](docs/JOURNAL.md) for progress.

## Setup from zero

How to get a brand-new Windows computer ready to work on this project. Every tool
is free. Type each command into **PowerShell** (Start menu → "PowerShell").

### 1. Install the tools

WinGet, Windows' built-in app installer, comes with Windows 10 and 11. Check it
with `winget --version`. If it's missing, install **App Installer** from the
Microsoft Store.

```powershell
winget install --id Git.Git -e --source winget
winget install --id OpenJS.NodeJS.LTS -e --source winget
winget install --id Microsoft.VisualStudioCode -e --source winget
winget install --id GitHub.cli -e --source winget
```

Click **Yes** if Windows asks "allow this app to make changes?". Type **Y** if
WinGet asks you to accept its terms. Then **close PowerShell and open a new one**,
so it can find the new programs.

### 2. Install the VS Code extensions

```powershell
code --install-extension dbaeumer.vscode-eslint
code --install-extension esbenp.prettier-vscode
code --install-extension EditorConfig.EditorConfig
```

### 3. Tell Git who you are

Use GitHub's private "noreply" email to keep your real email out of the public
history. To find it, go to github.com → **Settings → Emails** and tick **Keep my
email addresses private**.

```powershell
git config --global user.name "Your Name"
git config --global user.email "ID+username@users.noreply.github.com"
```

### 4. Log in to GitHub

```powershell
gh auth login
```

Choose **GitHub.com** → **HTTPS** → **Yes** → **Login with a web browser**. Copy the
one-time code, press Enter, paste the code in the browser and click **Authorize**.

### 5. Download this project

```powershell
gh repo clone AlbanAlla/ST-website
cd ST-website
```

### 6. Check everything works

```powershell
git --version; node --version; npm --version; code --version; gh --version
gh auth status
git config --global --list
```

Each command should print a version or your details, with no errors. If
something fails, look it up in [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md).

**Versions this project was set up with (2026-10-08):**

| Tool | Version |
|---|---|
| WinGet | 1.29.380 |
| Git | 2.55.0 |
| Node.js (LTS) | 24.20.0 |
| npm | 11.19.0 |
| VS Code | 1.140.0 |
| GitHub CLI | 2.102.0 |
| ESLint / Prettier / EditorConfig extensions | 3.0.34 / 12.4.0 / 0.18.2 |

Newer versions are fine. For Node.js, use the current **LTS** (long-term support) release.

**On a Mac:** install [Homebrew](https://brew.sh), then run
`brew install git gh` and `brew install --cask visual-studio-code`, and get the
Node.js LTS installer from [nodejs.org](https://nodejs.org). Steps 2 to 6 are the
same.

## Run it locally

Not available yet. Instructions will be added here when the site is scaffolded (Phase 3).

## Deploy it

Not available yet. Instructions will be added here at launch (Phase 5).

## Project structure

| Path | What it is |
|---|---|
| `CLAUDE.md` | Standing rules Claude Code follows in every session (quality, budget, docs, Git). |
| `PROMPT-PLAYBOOK.md` | The prompts used to build the site, phase by phase. |
| `README.md` | This file: what the project is and how to work with it. |
| `CHANGELOG.md` | Visible changes to the site, grouped by version and date. |
| `.gitignore` | Files Git must never track (secrets, installed libraries, build output). |
| `.gitattributes` | Keeps line endings consistent between Windows and Mac/Linux. |
| `docs/JOURNAL.md` | Session-by-session log: what was asked, every command, problems, next steps. |
| `docs/TROUBLESHOOTING.md` | Every error encountered, with its symptoms, cause and fix. |
| `docs/decisions/` | One file per significant decision, explaining why it was made. |
