# Claude Code Prompt Playbook

Companion to `CLAUDE.md`. `CLAUDE.md` holds the standing rules Claude Code follows in every session; this playbook holds the prompts to give it, phase by phase, from an empty computer to a launched website and a tutorial about building it.

**Project at a glance**
- Builder: a beginner who wants the AI to do the heavy lifting, then use Claude to troubleshoot later.
- Where: Claude Code in the Claude desktop app (Code tab, **Local**), on the builder's own computer. Claude Code installs everything needed.
- Standard: professional, responsive, accessible, fast, SEO-friendly.
- GitHub: everything managed there. A few large milestones, one long-lived branch per milestone, branches kept after merging.
- Budget: zero. Free hosting (Netlify, Vercel) and free services only; a custom domain is the one optional paid item.
- Documentation: every step logged, because the project becomes a "from nothing to a finished website" tutorial.

## How to use this playbook

Copy each prompt into a Claude Code session in the desktop app (Code tab, **Local**), in order, one phase at a time. Replace anything in [square brackets] with your own details. Claude Code does the installing, building, committing and documenting; your job is to describe, approve and review.

Ground rules that make this work:

- **One project folder, always the same one.** Open the same folder in every session so Claude reads the same `CLAUDE.md` and history.
- **Start every session with the start-of-session prompt and end with the end-of-session prompt** (see Recurring prompts). This is what keeps the journal complete for your tutorial.
- **Use Plan mode for anything big.** Ask for a plan, read it, then say "go ahead." It costs a minute and saves hours.
- **Approve, don't rubber-stamp.** When Claude asks to run a command, read the one-line description. Say no to anything that deletes things you didn't ask to delete.
- **Be specific about what you want, not how to build it.** Describe the result ("a booking page that feels calm and premium"); let Claude choose the technology.
- **One branch per milestone, many sessions per branch.** Milestones are big and robust; inside them, Claude commits in small steps so the journal and history stay easy to follow.
- **You still handle your own logins and passwords.** Your computer password, GitHub sign-in and hosting sign-up are yours to type; Claude will tell you exactly when.

## Phase 0: Set up CLAUDE.md (once)

Before the first prompt, create an empty folder (for example `Documents/my-website`), put the `CLAUDE.md` file inside it, and open that folder in a Claude Code session. `CLAUDE.md` holds your standing rules: high quality standard, zero budget, automatic documentation, proper commits, and asking before anything irreversible.

First prompt, to confirm Claude has understood the rules:

```text
Read CLAUDE.md and summarize, in plain language, the rules you'll follow in this project. Then add one rule: at the start of every session, read docs/JOURNAL.md and the latest decision records before doing anything else. Save that change to CLAUDE.md.
```

If you ever want to change how Claude works (more explanation, fewer questions, a different commit style), edit `CLAUDE.md` through a prompt rather than repeating the instruction each session:

```text
Update CLAUDE.md so that from now on you [new rule]. Log the change in the journal.
```

## Phase 1: Set up your computer

Claude Code checks your machine, installs what's missing through your system's package manager (Homebrew on Mac, WinGet on Windows), and connects everything to GitHub. You approve each command, type your computer password when the system asks, and click Authorize when GitHub opens in your browser.

**1.1 Audit and install**

```text
I'm on [Mac / Windows] and I'm new to coding. Check what's already installed on this computer, then install everything needed to build, run and maintain a professional website: Git, Node.js (current LTS), a package manager if missing, VS Code, and the GitHub CLI. Add anything else you'd recommend and explain why in one line each. Everything must be free. Verify each install works. Show me the plan first. Log every command and result in docs/JOURNAL.md, written so a beginner could repeat it.
```

**1.2 Configure Git and GitHub**

```text
Configure Git with my name [Your Name] and email [you@example.com]. Then log me into GitHub with the GitHub CLI and tell me exactly what to click when the browser opens. Confirm the login worked. Log the steps.
```

**1.3 Create the repository**

```text
Initialize this folder as a Git repository with a sensible .gitignore, create a [private / public] GitHub repository named [my-website], connect it, and push the first commit containing CLAUDE.md and the docs folder. Set up the docs structure from CLAUDE.md (JOURNAL.md, decisions/, TROUBLESHOOTING.md, README.md, CHANGELOG.md). Give me the link to the repo.
```

**1.4 Check the setup**

```text
Run a final health check: list every tool you installed with its version, confirm I can push to GitHub, and write a "Setup from zero" section in the README that someone could follow on a brand-new computer.
```

## Phase 2: Define the website

The quality of the final site depends most on this phase. Let Claude interview you, then turn your answers into a written brief and a technical plan before any code exists.

**2.1 Interview**

```text
Before we build anything, interview me about the website. Ask one group of questions at a time: purpose and audience, pages and content, features (forms, booking, shop, blog, accounts), look and feel, websites I admire, and whether I have a domain name. My budget is zero: everything must be free. When you're done, write everything into docs/BRIEF.md and show me a summary.
```

**2.2 Technical plan**

```text
Based on docs/BRIEF.md, propose the tech stack, hosting and project structure for a professional, fast, accessible, SEO-friendly site that I can maintain with your help. Everything must be free: prioritize free hosting such as Netlify or Vercel, and free services for anything else (forms, analytics, images). Check each option's current free-tier limits and terms, including whether commercial use is allowed. Compare two or three options in a short table and recommend one. Record the choice in docs/decisions/0001-tech-stack.md. Don't install anything yet.
```

**2.3 Roadmap**

```text
Break the build into a small number of large, robust milestones (around 4 to 6 for the whole site), each one a complete, shippable chunk such as "foundation and design system", "all core pages", "forms and features", "quality pass" and "launch". Each milestone will get one long-lived branch and may take several sessions. List them in order with what "done" means for each, and the smaller tasks inside each one. Save it as docs/ROADMAP.md with checkboxes, and create a matching GitHub issue for each milestone.
```

**2.4 Visual direction**

```text
Propose a visual direction: color palette, fonts, spacing, button and card styles, with reasoning tied to the brief. Build a single preview page I can open in my browser so I can approve it before we build the real pages. Record the decision in docs/decisions/.
```

## Phase 3: Build

Work through the roadmap one milestone at a time; a milestone usually takes several sessions on the same branch. Each milestone gets its own branch and pull request, so `main` always works and your Git history reads like chapters.

**3.1 Scaffold the project**

```text
Start milestone 1 from docs/ROADMAP.md. Create the project with the stack from decision 0001 on a new branch. Set up linting, formatting, type-checking and a test runner, and make them run automatically before each commit. Start the site locally and tell me the address to open in my browser. Commit, push, and update the journal.
```

**3.2 Build a milestone (reuse for every milestone)**

```text
Start the next unchecked milestone in docs/ROADMAP.md. Show me the plan first. Build it on its own branch (if that branch already exists, continue on it), matching the visual direction and the brief. Make it responsive and accessible. Run all checks, fix any failures, then commit in small logical steps and push at the end of every session. Only when the whole milestone is done, open a pull request with a description and screenshots or a preview link, tick the milestone and close its GitHub issue. Every session, update the journal, README and changelog.
```

**3.3 Review what was built**

```text
Walk me through what you just built as if I were a non-technical client: what each page does, where to look, and anything I should test by hand. List anything you weren't sure about or had to assume.
```

**3.4 Request changes**

```text
On [page/section], change [what you see] to [what you want]. Keep everything else as it is. Same branch, then update the pull request.
```

**3.5 Merge**

```text
The pull request looks good. Merge it into main, keep the branch for the record, pull the latest main, and confirm the site still runs. Log it.
```

## Phase 4: Quality pass

This is what separates a "works" site from a high-standard one. Treat the whole quality pass as one milestone on one branch, then save the results in `docs/QUALITY.md` so you can show them in the tutorial.

**4.1 Full audit**

```text
Audit the whole site as a senior reviewer would: accessibility (WCAG AA), performance (page speed, image sizes, Lighthouse scores), SEO (titles, descriptions, sitemap, social previews), mobile layout, broken links, and code quality. Give me a prioritized list of findings with severity. Don't fix anything yet.
```

**4.2 Fix the findings**

```text
Fix every high and medium finding from the audit on the quality-pass branch, one commit per fix. Re-run the audit and record before-and-after scores in docs/QUALITY.md. Open a pull request.
```

**4.3 Security and privacy**

```text
Review the project for security and privacy issues: secrets in code or Git history, outdated or vulnerable dependencies, form spam protection, security headers, and whether I need a privacy policy or cookie notice for my audience. Fix what you can and list what needs my decision.
```

**4.4 Automated checks on GitHub**

```text
Set up GitHub Actions so every pull request automatically runs linting, type-checking, tests and a build. Protect the main branch so nothing merges unless those checks pass. Stay within GitHub's free limits. Explain in the README what the checks do.
```

**4.5 Cross-device test**

```text
Test the site at phone, tablet and desktop widths and in light and dark system settings. Take screenshots of each page at each size, save them in docs/screenshots/, and fix anything that looks wrong.
```

## Phase 5: Launch

Everything here stays free: the site goes live on the host's free address (for example yoursite.netlify.app). A custom domain is the one optional cost, so step 5.3 is only if you decide you want one. Hosting sign-ups involve your accounts, so Claude prepares everything and gives you click-by-click steps for the parts only you can do.

**5.1 Deployment plan**

```text
Prepare the site for deployment with the hosting option from our decisions. Use only free plans. Tell me exactly what accounts I need, confirm each is free, warn me about any free-tier limits we might hit, and give me the click-by-click steps I must do myself. Do everything else from here, including connecting it to GitHub so every merge to main redeploys automatically. Log it all in the journal.
```

**5.2 Preview deployments**

```text
Make sure every pull request gets its own preview link so I can check changes on a real URL before merging. Add the preview link to the pull request description template.
```

**5.3 Custom domain (optional, the only paid step)**

```text
I [own / want to buy] the domain [example.com]. Walk me through connecting it to the hosting, including the exact DNS records to enter, and verify HTTPS works once it's live. Record the settings in docs/decisions/ (without any passwords).
```

**5.4 Launch checklist**

```text
Run a final pre-launch checklist on the live URL: every page loads, forms work and reach me, 404 page exists, favicon and social previews show, free privacy-friendly analytics are working, and the sitemap is submitted to search engines. Tag the release v1.0.0 on GitHub with release notes from the changelog.
```

## Phase 6: After launch — troubleshooting and maintenance

Because Claude documented every decision and error, a future session can understand the project quickly. Always point it at the docs first.

**6.1 Something is broken**

```text
Something is wrong: [what you see, on which page, on which device, since when]. Read docs/JOURNAL.md, docs/TROUBLESHOOTING.md and recent commits first. Find the cause, explain it in plain language, fix it on a branch with a test so it can't come back, and add the issue to TROUBLESHOOTING.md.
```

**6.2 Understand a part of the site**

```text
Explain how [feature, page or file] works, step by step, as if I'm new to coding. Then add or update a plain-language explanation of it in docs/.
```

**6.3 Monthly maintenance**

```text
Run monthly maintenance: update dependencies safely, check for security alerts, check we're still within free-tier limits, re-run the quality audit and compare with docs/QUALITY.md, check the live site for broken links, and summarize anything that needs my attention. One pull request, logged in the journal.
```

**6.4 Add a new feature later**

```text
I want to add [feature]. Read the brief, roadmap and decision records, then propose how it fits (using only free services). Add it to the roadmap as a new milestone and build it the same way as before.
```

## Recurring prompts (every session)

These bookend every session and keep GitHub and the documentation complete without you thinking about it.

**Start of session**

```text
Read CLAUDE.md, the last three entries in docs/JOURNAL.md and docs/ROADMAP.md. Pull the latest from GitHub and switch to the current milestone's branch. Tell me where we left off and what you suggest doing today.
```

**End of session**

```text
We're stopping for today. Commit and push everything with clear messages. Update docs/JOURNAL.md with today's full entry (what I asked, every step and command, problems and fixes, what's next), plus the README, changelog and roadmap if they changed. Confirm GitHub is up to date and give me a three-line summary.
```

**Commit check (anytime)**

```text
Show me the commits from this session with their messages. Are they clear enough for someone reading the history to follow what happened? Improve any unpushed ones that aren't.
```

**Documentation check (weekly)**

```text
Audit the docs folder against the actual code and Git history. Fill any gaps in the journal, decision records and troubleshooting guide, and fix anything out of date. List what you changed.
```

**When you're lost**

```text
Stop. Explain in plain language what state the project is in, what you were trying to do, and what my options are. Don't change anything until I choose.
```

## Phase 7: Turn it into the tutorial

By now the repo holds your whole story: the journal, decisions, commits, pull requests, screenshots and quality scores. Claude can turn that into a tutorial script.

**7.1 Outline**

```text
Read the entire journal, decision records, roadmap and Git history. Draft a tutorial outline titled "From nothing to a finished website with Claude Code," organized by chapter, with the exact prompts I used, what happened, and the mistakes worth showing. Save it as docs/TUTORIAL-OUTLINE.md.
```

**7.2 Script a chapter**

```text
Write chapter [N] of the tutorial as a script I can read on camera: what to show on screen, what to say, which prompt to paste, and what the viewer should see happen. Keep it beginner-friendly.
```

**7.3 Reproducibility check**

```text
Check that someone following the tutorial on a fresh computer would get the same result. List any steps that relied on something specific to my machine or account, and add notes to cover them.
```

Tip for filming: screen-record the Phase 1 setup live the first time. A fresh computer is the one moment you can't recreate later.
