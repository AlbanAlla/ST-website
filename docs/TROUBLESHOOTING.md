# Troubleshooting

Every error or confusing message we've hit, with its symptoms, cause and fix.
Search this page (Ctrl+F) for the words in your error message.

---

## Setup and tools

### "The term 'git' (or node, npm, code, gh) is not recognized"
- **Symptoms:** You just installed a tool, but the terminal says the command
  doesn't exist.
- **Cause:** A terminal reads the PATH (Windows' list of folders to search for
  programs) once, when it opens. A terminal opened before the install doesn't
  know about the new program.
- **Fix:** Close the terminal and open a new one. Or, in PowerShell, reload the
  PATH without closing:
  ```powershell
  $env:Path = [Environment]::GetEnvironmentVariable('Path','Machine') + ';' + [Environment]::GetEnvironmentVariable('Path','User')
  ```
  If it still fails, restart the computer. If it fails even after that, the
  install didn't finish: run the `winget install` command again.

### "Committer identity unknown" / "unable to auto-detect email address"
- **Symptoms:** Git refuses to commit and shows "Please tell me who you are".
- **Cause:** Git stamps every commit with a name and an email. If either is
  missing from Git's settings, it can't make a commit.
- **Fix:** Set both. To keep your real email private, use GitHub's noreply
  address. For this project it's:
  ```powershell
  git config --global user.name "N"
  git config --global user.email "25772264+AlbanAlla@users.noreply.github.com"
  ```
  Check with `git config --global --list`. For a new account, find your noreply
  address on github.com → Settings → Emails (tick "Keep my email addresses
  private").

### "DeprecationWarning: `url.parse()` behavior is not standardized..." when running `code --install-extension`
- **Symptoms:** This warning is printed when installing VS Code extensions from
  the terminal.
- **Cause:** VS Code uses an older built-in function internally, and Node.js
  warns about it. It isn't a problem with our setup.
- **Fix:** Nothing to do. It's harmless. Check that the next line says
  "Extension ... was successfully installed".
