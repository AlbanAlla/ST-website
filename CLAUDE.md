# Project instructions for Claude Code

## About me and this project
- I'm new to coding. You are doing most of the building; I direct and review.
- Goal: a production-quality website built to a professional standard.
- Everything is managed on GitHub, and every step is documented, because I will turn
  this project's history into a "from nothing to a finished website" tutorial.
- After launch I'll rely on the docs in this repo (and on Claude) to troubleshoot,
  so the documentation must make sense to someone who didn't write the code.

## Quality standard
- Choose a modern, well-supported stack and explain the choice in a decision record
  (see below). Prefer TypeScript over plain JavaScript.
- The site must be responsive (phone, tablet, desktop), accessible (semantic HTML,
  keyboard navigation, alt text, good contrast), fast, and SEO-friendly.
- Keep code clean and organized; no dead code, no unexplained hacks.
- Add automated checks (linting, formatting, type-checking, tests where useful) and
  run them before every commit. Fix failures rather than skipping them.
- Budget is zero. Use only free tools, plans and services (free hosting such as
  Netlify or Vercel, free form and analytics services). Before relying on a free
  tier, check its current limits and terms, and warn me before anything that
  would cost money.
- Never put secrets, API keys or passwords in code or commits. Use environment
  variables and keep `.env` files out of Git.

## Documentation rules (do these automatically, every session)
1. **docs/JOURNAL.md**: append an entry at the end of every session with:
   - date and a one-line summary
   - what I asked for, in my words
   - what you did, step by step, including every command you ran
   - problems you hit and how you fixed them
   - what's next
   Write it in plain language a beginner can follow.
2. **docs/decisions/**: one short file per significant decision (stack, hosting,
   libraries, structure), numbered `0001-title.md`, covering: the decision, the
   options considered, why this one, and trade-offs.
3. **docs/TROUBLESHOOTING.md**: every error we encounter, its symptoms, the cause,
   and the fix. This is my manual for after launch.
4. **README.md**: keep current with what the project is, how to run it locally,
   how to deploy it, and the project structure explained folder by folder.
5. **CHANGELOG.md**: user-visible changes, grouped by version/date.
6. When you finish a feature, add a short "How this works" section to the README
   or a file in docs/ explaining it in plain language.

## Git and GitHub rules
- Commit after each logical step, not in one big batch at the end.
- Use Conventional Commit messages: `feat:`, `fix:`, `docs:`, `style:`,
  `refactor:`, `test:`, `chore:`, with a clear description and a body explaining
  why when it isn't obvious.
- Milestones in docs/ROADMAP.md are few, large and robust (roughly 4 to 6 for the
  whole site). Each milestone gets ONE long-lived branch (`milestone/short-name`)
  that may span many sessions; continue on it if it already exists. Don't create
  extra branches for small tasks inside a milestone.
- Open a pull request only when the whole milestone is done, with a description
  of what changed and how to check it. Merge to `main` once checks pass.
- Never delete branches after merging; keep them for the project record.
- `main` must always be in a working, deployable state.
- Push to GitHub at the end of every session.
- Ask me before anything destructive or irreversible (force-pushing, deleting
  branches or files, rewriting history, changing hosting or domain settings).

## How to work with me
- At the start of every session, before doing anything else, read docs/JOURNAL.md
  and the latest decision records in docs/decisions/ so you know where we left off.
- Before a large change, show me a short plan and wait for my go-ahead.
- After each task, give me a brief summary: what changed, how to see it, and
  anything I need to do myself (e.g. create an account, click a button).
- If something needs my action outside the code (GitHub settings, hosting
  sign-up, a domain), give me exact click-by-click steps and log them in the
  journal too.
