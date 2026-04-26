# Vibecoding Journey

> My vibecoding journey on building a working app using AI as my developer, starting from an idea with no prior coding experience.

---

## What Is Vibecoding?

Vibecoding is building software by describing what you want in plain English and letting an AI write the code. You direct; the AI builds. This guide covers the full process from first idea to a working, deployed app.

---

## The Phases at a Glance

| Phase | What Happens |
|-------|-------------|
| 1. Define Your Idea | Describe the problem and what the app needs to do |
| 2. Feature Discovery | AI asks clarifying questions until both of you understand the full scope |
| 3. Architecture and Planning | Decide how the system is built and in what order |
| 4. Architecture Review | Pressure-test the design before writing any code |
| 5. Choose Your Tools | Evaluate and commit to your tech stack |
| 6. Initialize Your Project | Set up git, branches, issue tracker, and docs structure |
| 7. Scaffold | Deploy the blank app skeleton end-to-end |
| 8. Build | Implement features phase by phase |
| 9. Test | Verify each phase before moving to the next |

---

> **First time vibecoding with Claude Code on a Mac?** Before starting, you will need to install a set of terminal tools (CLI tools) to use Claude Code and manage your project. See [Prerequisites for First-Time Vibecoders](#prerequisites-for-first-time-vibecoders) at the end of this document.

---

## Phase 1: Define Your Idea

Describe the problem your app solves and who it is for.

- Write 3 to 4 paragraphs covering the problem, who uses the app, and what it needs to do
- Include detail on data (what does the system need to remember?), users (who logs in, and what can each person do?), and workflows (what is the main action a user takes, step by step?)
- Do not worry about technical terms; describe it as you would to a colleague
- If you have existing materials such as slides, spreadsheets, or documents, prepare them to share in Phase 2
- Create AGENT.md: the rulebook for how the project is built — naming conventions, how Claude should behave, and any decisions that must stay consistent across every session. Start it now and keep it updated throughout.
- Create CHANGELOG.md: a running log of every meaningful change. Start it from the very first session so nothing is lost.

**Your goal at this stage:** A clear enough description that Claude understands the problem, the users, and the shape of the solution — and two documents in place to track everything from day one.

---

## Phase 2: Feature Discovery

Let Claude ask questions until there is enough detail to build from.

- Share your description with Claude and ask it to begin asking clarifying questions by typing: `"Ask me 5 more questions"`
- Expect 30 to 40 rounds of 5 questions each; this is normal and necessary (expect to spend 2 to 4 hours on this)
- Answer each question as specifically as you can; vague answers will need to be revisited later
- When the questions start to feel repetitive or the scope feels fully covered, ask Claude: `"Do you need any more information?"` Claude will tell you honestly if it does
- Share any existing materials; Claude will read them and flag any contradictions with what was already discussed
- At the end of this phase, ask Claude to create FEATURES.md, a plain-English list of every feature

Types of questions Claude will ask:
- Who performs each action, and how? (manual vs. automatic)
- What happens when something goes wrong? (errors, edge cases, unexpected inputs)
- What does each type of user need to see vs. do?
- What data does the system need to store, and for how long?
- What happens at scale?

As Claude learns more about the app, its questions will get more detailed and specific. The more thoroughly you answer, the more solid the foundation and the better Claude will build it.

**Your goal at this stage:** A complete feature list where every item has been discussed, decided, and written in plain English that a non-technical reader can understand.

---

## Phase 3: Architecture and Planning

Turn the feature list into a build plan.

- Ask Claude to create ARCHITECTURE.md; this records every technical decision and why it was made
- Ask Claude to create RISK_REGISTER.md; this lists every way the system could fail and what happens in each case
- Run a feature prioritization session: which features are needed for launch, which can wait, and which depend on other features being built first
- Assign each feature to a milestone (Alpha, Beta, Launch, V2, etc.): work with Claude to do this. Ask it to propose an initial milestone assignment based on feature prioritization, then review the result and make changes as needed. You decide the final order.
- Ask Claude to create ROADMAP.md; this is a numbered, ordered list of every build step across all milestones
- If your app sends emails or notifications, draft and approve all templates before any code is written; this prevents inconsistent messaging later

**Your goal at this stage:** A full build plan where every feature has a milestone, every step has an order, and every technical decision has a written reason behind it.

---

## Phase 4: Architecture Review

Pressure-test the design before a single line of code is written.

- Start a new session and switch to the most capable Claude model available (Claude Opus); this is important so Opus comes in clean with no prior context
- Open by typing: `"You are my principal technical architect"`
- Ask Opus to read all of your planning documents
- Once it has read them, provide 1 to 2 paragraphs of scope context that is not in the documents: how many users, how often the system will be used, who will maintain it, budget constraints, and any other real-world constraints that shaped your decisions
- Run question iterations with Opus the same way as Phase 2: `"Ask me 5 more questions"` until Opus has everything it needs
- Once the questions are done, ask Opus to provide a critique of the full plan: architecture, roadmap, risks, and any gaps it identified during the session
- Opus will produce the critique in chat as a discussion; work through each point together
- For each critique point: understand why Claude initially recommended the original approach, weigh the pros and cons, fix what is genuinely wrong, and note and set aside what is an acceptable trade-off
- Once the discussion is complete, ask Opus to save the full critique and discussion outcome as `ARCHITECTURE_REVIEW_YYYYMMDD.md` in your `docs/` folder
- Switch back to Claude Sonnet and update your planning documents to reflect any changes agreed during the review

**Your goal at this stage:** Confirm the design is sound before spending time building on top of it. Every gap caught here costs nothing to fix; the same gap caught mid-build costs significant rework.

---

## Phase 5: Choose Your Tools

Evaluate and commit to your tech stack before building.

Most tool choices emerge naturally during Phases 2 and 3. For any tool that requires a deliberate decision, work through these questions before committing:

- What options exist for this?
- What do most projects like this use?
- What are the pros and cons of each option?
- What does each option cost?
- How hard would it be to switch to a different option later?

| Category | What to Decide | Tool Selected |
|----------|----------------|---------------|
| Hosting | Where the app runs (frontend and backend separately) | Cloudflare Pages (frontend) + Cloudflare Workers (backend) |
| Database | Where data is stored | Cloudflare D1 |
| Authentication | How users log in | Google OAuth |
| File storage | Where uploaded files are kept | Google Drive |
| Email | How the system sends notifications | Gmail API |
| AI | Which model powers intelligent features | Claude API (Anthropic) |
| Error tracking | How production errors are caught and reported | Sentry (free tier) |
| Testing | How automated tests run | Vitest |
| CI/CD | How code is deployed automatically | GitHub Actions (frontend) + Wrangler (backend) |

**Your goal at this stage:** Every tool committed and documented in ARCHITECTURE.md before any code is written.

---

## Phase 6: Initialize Your Project

Set up the infrastructure for managing your code before any code exists.

This phase happens before Scaffold. Getting this right at the start costs 30 minutes; fixing it later costs hours.

- Create a GitHub repository for the project. During setup, GitHub offers to initialize it with a README.md — check this option if you do not have one yet. If you already have a README.md locally, skip this option and push your own file instead.
- Create two branches: `main` (production only; nothing is pushed here directly) and `dev` (all active work goes here)
- Set the workflow: all work goes to `dev`; when ready, open a pull request from `dev` to `main` on GitHub; merge; pull `main` locally. `main` only ever receives reviewed, ready code
- Initialize the GitHub Issues tracker; create a placeholder Issue #1 to confirm it is active and ready to use
- Use GitHub Issues for: deferred features, open design decisions, implementation blockers, and technical debt. Not for fixed bugs (those go in TROUBLESHOOTING.md) and not for general planning (that goes in ROADMAP.md)
- Set up the docs folder structure:
  - `README.md` at the project root (GitHub displays this automatically)
  - `CHANGELOG.md` at the project root (already created in Phase 1)
  - `AGENT.md` inside `docs/` (already created in Phase 1)
  - All other documents inside `docs/`
- Create TROUBLESHOOTING.md inside `docs/`: a log of every problem encountered and how it was fixed. Starts here when the build infrastructure goes in and issues begin to surface.

**Your goal at this stage:** A repository with two branches, an active issue tracker, a clean docs structure, and TROUBLESHOOTING.md ready before any code is written.

**Watch for:** Skipping branch setup and the issue tracker because you are eager to start building. Projects started without them are harder to track, harder to collaborate on, and harder to reverse if something goes wrong.

> **Note:** Claude handles all of the setup work in this phase. You do not need to run commands, configure tools, or troubleshoot anything manually. Your role is to review what Claude plans to do and approve each step before it acts.

---

## Phase 7: Scaffold

Deploy a blank app skeleton before building any features.

- Ask Claude to handle all setup: installing tools, configuring the environment, connecting each service, and running connectivity tests
- You should not need to run any commands or troubleshoot configuration manually at this stage
- The goal is a deployed, end-to-end skeleton: the app is live, login works, and you see a blank page after signing in
- No features, no data, no AI; just the connected skeleton

Create these two tracking documents during Scaffold; they only make sense once something is deployed and testable:

- TESTING.md: automated test results after every milestone
- USER-TESTING.md: manual verification checklist per milestone

**Your goal at this stage:** A live, deployed blank app where every service is connected and you can log in. Nothing is built yet, and that is the point.

---

## Phase 8: Build

Implement features in milestone order, one step at a time.

- Follow the ROADMAP.md step sequence; do not skip steps or build out of order
- Before starting any step, read the relevant section of ARCHITECTURE.md to confirm the design intent
- If a step cannot be implemented exactly as the architecture describes, stop and ask Claude before writing any code; do not resolve the mismatch silently
- After each step, update CHANGELOG.md
- After each milestone, update ROADMAP.md to mark completed steps

What to expect during the build:
- Earlier decisions will be tested against reality; some will hold, some will need adjustment
- Data models will evolve as implementation reveals edge cases the planning phase did not anticipate
- New features will be identified; new decisions will arise; this is normal
- When a new unresolved decision or deferred feature comes up, create a GitHub Issue immediately rather than leaving it unresolved in conversation

Before asking Claude to make any non-trivial change, ask it to explain the full scope of what it plans to do. Review and approve before it acts. The cost of pausing is low; the cost of an unwanted change can be high.

**Your goal at this stage:** Features built in order, every step tested before the next one starts, every change logged, every new decision tracked in GitHub Issues.

---

## Phase 9: Test

Verify each phase before moving to the next.

There are two types of testing, and both are required:

**Automated tests** are written alongside the code by Claude, run automatically, and confirmed passing before any phase is marked complete. Results are recorded in TESTING.md. They verify that the logic works correctly under the hood.

**Manual user testing** is done by you, following the USER-TESTING.md checklist, after every phase. It verifies that the app works correctly as a real user would experience it.

- After completing each build phase, ask Claude to run the full automated test suite and confirm all tests pass before marking anything done
- After automated tests pass, work through the USER-TESTING.md checklist yourself
- Record any issues found in TROUBLESHOOTING.md with the root cause and how it was fixed

**Your goal at this stage:** Both automated and manual testing passing before calling any phase complete. Never mark a phase done based on automated tests alone.

---

## Documents Reference

Every document produced during the process, what it is for, and when it is created.

| Document | Purpose | Phase |
|----------|---------|-------|
| AGENT.md | The rulebook for the project: naming conventions, how Claude should behave, and decisions that must stay consistent across every session | 1: Define Your Idea |
| CHANGELOG.md | A running log of every meaningful change, newest at the top | 1: Define Your Idea |
| FEATURES.md | A plain-English list of every feature, written so a non-technical reader can understand it | 2: Feature Discovery |
| ARCHITECTURE.md | Every technical decision and the reason behind it | 3: Architecture and Planning |
| RISK_REGISTER.md | Every way the system could fail and what happens in each case | 3: Architecture and Planning |
| ROADMAP.md | A numbered, ordered list of every build step across all milestones | 3: Architecture and Planning |
| EMAIL_TEMPLATES.md | Canonical reference for all email and notification templates, approved before any code is written | 3: Architecture and Planning |
| ARCHITECTURE_REVIEW_YYYYMMDD.md | The written critique produced by Opus during the architecture review, including what was fixed and what was set aside | 4: Architecture Review |
| README.md | The front door of the project: what it is, who it is for, and how to get started | 6: Initialize Your Project |
| TROUBLESHOOTING.md | Every problem encountered during the build and how it was fixed; prevents the same issue from being debugged twice | 6: Initialize Your Project |
| TESTING.md | Automated test results after every milestone | 7: Scaffold |
| USER-TESTING.md | Manual verification checklist per milestone; what to test yourself after the automated tests pass | 7: Scaffold |

---

## What Makes This Process Work

- **Plan before you build.** The more complete your planning, the faster and smoother the build. Every decision made during planning is one you do not have to make mid-build.

- **Pressure-test before you commit.** The architecture review (Phase 4) is the highest-leverage step in the process. Every issue caught there costs nothing to fix; the same issue caught mid-build costs rework.

- **Set up your project infrastructure first.** Branches, issue tracking, and docs structure belong in Phase 6, before any code is written. Adding them later is possible but painful.

- **Follow the roadmap.** When scope changes, update the roadmap first and then build. Do not build things that are not in the roadmap without updating it first.

- **Track everything.** CHANGELOG.md, TROUBLESHOOTING.md, TESTING.md, and GitHub Issues mean you never lose context between sessions, and neither does the AI.

- **Confirm before the AI acts.** Before Claude makes any non-trivial change, ask it to present the full scope of what it plans to do. The cost of pausing is low; the cost of an unwanted change can be high.

---

## Tips

**1. Starting a new session mid-project**

Claude does not retain memory between sessions. If you restart your computer or close the CLI, the context is gone. To get back up to speed efficiently:

- First, try running `/compact` in Claude Code. This compresses the conversation history and frees up context without losing the session.
- If you are starting a completely new session, always begin by asking Claude to read your project documentation before doing anything else. Your docs are the shared memory that keeps every session consistent.

**2. Folder organization**

Keep your projects organized from the start. A clean structure makes it easier for both you and Claude to navigate.

All projects live under `~/projects/`. Use this naming convention:
- Local-only project: just the name — `projectname`
- GitHub-hosted project: prefix with `gh-` — `gh-projectname`

This makes it immediately clear from the directory listing which projects have a remote. `notes/` and `scripts/` are examples of personal, standalone local folders not tied to any specific project. If scripts are specific to a project, they belong inside that project folder instead.

Every project gets two branches:
- `main` — stable and deployable; for hosted projects, Cloudflare watches this branch and deploys from it
- `dev` — all active development; work here first, then merge into `main` when ready to ship

Do not build features directly on `main`. Work on `dev`, review the result, merge to `main`, then push to trigger deployment.

Example top-level structure:

```
~/projects/
├── notes/                    # local only
├── your-project-name/        # local only
├── gh-your-project-name1/    # hosted on GitHub
└── gh-your-project-name2/    # hosted on GitHub
```

Inside each project:

```
projects/
└── your-project-name/
    ├── README.md
    ├── CHANGELOG.md
    ├── docs/
    │   ├── AGENT.md
    │   ├── ARCHITECTURE.md
    │   └── (all other docs)
    ├── frontend/
    └── worker/
```

**3. When Claude gives you options and you are not a subject matter expert**

Do not guess. Ask Claude to walk you through:

- What are the pros and cons of each option?
- What is the complexity and cost of each?
- What does the industry typically use for this?
- What makes the most sense for this specific project?
- How hard would it be to switch to a different option later?

When you are still unsure after the discussion, do not force a decision. Create a GitHub Issue to revisit it and add a task in ROADMAP.md as a reminder. A deferred decision that is tracked is better than a hasty decision that needs to be undone.

**4. Context limits**

Claude has a memory limit per session. If responses start to feel confused, repeat things already covered, or lose track of earlier decisions, the session context is likely full. Run `/compact` first to compress the history. If the session is too far gone, start a fresh session and ask Claude to re-read the project docs before continuing.

**5. One step at a time**

Do not ask Claude to build multiple features in a single message. Give one instruction, review the result, approve it, then move to the next step. Batching instructions feels faster but makes it much harder to identify what went wrong when something does not work as expected.

**6. Git is your safety net**

Every committed version is preserved in git history. If Claude accidentally changes a file or something breaks, nothing is permanently lost. You can always recover a previous version. This means you can approve changes confidently knowing there is always a way back.

**7. Approving changes**

Before Claude makes any non-trivial change, ask it to describe the full scope of what it plans to do. A useful habit: ask `"What are you about to change?"` before saying yes. The cost of pausing is low; the cost of undoing an unexpected change is high.

**8. Always open Claude Code from your project folder**

Always open Claude Code from inside your specific project folder, not from the root `projects/` folder. Claude Code's context is scoped to the folder you open it from — it can only read and modify files within that folder. Opening from the correct project folder keeps Claude focused on the right project and prevents it from accidentally reading or changing files that belong to a different project.

**9. Run /simplify before user testing or after a large build phase**

After building several features or making many code changes across multiple files, run `/simplify` in Claude Code. This instructs Claude to review the entire codebase for duplication, unnecessary complexity, and inefficiency, and refactor it without changing any behaviour. The benefit: the codebase stays clean and easy to extend, technical debt does not accumulate, and you go into user testing with code that is easier to debug if something goes wrong. Think of it as tidying up between phases rather than letting clutter build up over the entire project. Add a `/simplify` step explicitly in ROADMAP.md before each user testing checkpoint so it is never skipped. Note that `/simplify` reads the entire codebase and can consume a significant number of tokens; run it at natural pauses rather than after every small change to keep costs reasonable.

**10. Secrets and Environment Variables**

- Never commit secrets (API keys, tokens, passwords) to git

A secret is any value that gives access to an external service: an API key, a database password, an OAuth client secret. If a secret is committed to git and pushed to GitHub, it is permanently exposed — even if you delete it in a later commit, it remains visible in the git history.

Instead, store secrets in two places depending on the context:

- **Locally:** create a `.env` file in your project folder and put secrets there. Tell Claude to add `.env` to `.gitignore` so it is never accidentally committed.
- **In production:** use the secret management tool provided by your hosting platform. Claude will give you the command to run — for example, `wrangler secret put SECRET_NAME` for Cloudflare Workers. Run it in your own terminal (Ghostty), not inside Claude Code. That way Claude never sees the value you type.

If you accidentally commit a secret, treat it as compromised immediately: rotate the key (generate a new one and delete the old one) before trying to remove it from git history.

---

## Prerequisites for First-Time Vibecoders

If this is your first time vibecoding with Claude Code on a Mac, install the following terminal tools (CLI tools) before starting Phase 1. Each tool is listed in the order it should be installed.

---

### 1. Xcode Command Line Tools

**What:** A set of developer utilities that enables your Mac to run programming tools in the terminal. Required before anything else can be installed. Includes git and other essentials.

```
xcode-select --install
```

A popup will appear asking you to install. Click Install and wait for it to complete.

**Open:** Xcode Command Line Tools runs in the background — there is no app to open. It is ready the moment the installation completes.

**Verify:** Type the following in your terminal and press Enter. If you see a version number printed, it is working.

```
git --version
```

---

### 2. Homebrew

**What:** Mac's package manager. Think of it as an app store for developer tools — instead of downloading installers from websites, you install most tools with a single `brew install` command.

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the prompts. At the end, Homebrew will print a "Next steps" section — run those commands to add Homebrew to your path.

**Open:** Homebrew runs in the background — there is no app to open. You use it by typing `brew install [toolname]` in your terminal whenever you need to install something.

**Verify:** Type the following and press Enter. A version number means it is working.

```
brew --version
```

---

### 3. Ghostty *(optional but recommended)*

**What:** A fast, modern terminal app that replaces the default Mac Terminal. The terminal is the window where you type all your commands. Ghostty is smoother, more configurable, and more pleasant to work in day-to-day. Install it early so you can use it for the rest of the setup.

```
brew install --cask ghostty
```

**Open:** Press Cmd+Space, type "Ghostty", and press Enter. Or find it in your Applications folder. Use it as your terminal from this point forward — close the default Terminal and work in Ghostty instead.

**Verify:** If Ghostty opens and shows a blinking cursor where you can type commands, it is working correctly.

---

### 4. Fish Shell *(optional but recommended)*

**What:** The shell is the environment that runs inside your terminal window. It controls how commands look, how autocomplete works, and how errors are displayed. Fish is a modern shell that is friendlier for new users than the Mac default. Works inside Ghostty or the default Terminal.

```
brew install fish
```

To set Fish as your default shell:

```
echo /opt/homebrew/bin/fish | sudo tee -a /etc/shells
chsh -s /opt/homebrew/bin/fish
```

Restart your terminal after running these commands.

**Open:** Fish Shell runs automatically inside your terminal every time you open it. There is no separate app to launch.

**Verify:** Open a new terminal window. If the prompt looks different from before (Fish shows a colourful, friendly prompt), it is working. You can also type:

```
fish --version
```

---

### 5. Zoxide *(optional but recommended)*

**What:** A smarter navigation tool that replaces the standard `cd` command. Instead of typing out full folder paths, zoxide learns which directories you visit most often and lets you jump to them by typing just part of the name. Saves significant time when moving between projects. Requires Fish Shell to be installed first.

```
brew install zoxide
```

Add zoxide to your Fish configuration so it loads automatically:

```
echo 'zoxide init fish | source' >> ~/.config/fish/config.fish
```

Restart your terminal. From now on, use `z` instead of `cd` to navigate.

**Open:** Zoxide runs in the background — there is no app to open. You use it by typing `z` followed by part of a folder name in your terminal.

**Verify:** Type the following and press Enter. A version number means it is working.

```
zoxide --version
```

---

### 6. Node.js and npm

**What:** Node.js is the engine that runs JavaScript code outside of a browser. npm (Node Package Manager) is the tool that downloads and manages the code libraries your project depends on. Both are required to run Claude Code and most modern web projects.

```
brew install node
```

**Open:** Node.js and npm run in the background — there is no app to open. Claude uses them automatically when building your project.

**Verify:** Type the following and press Enter. Both should print a version number.

```
node --version
npm --version
```

---

### 7. Visual Studio Code *(optional but recommended)*

**What:** A free code editor for browsing and reading the files Claude builds. You will not write code manually — Claude does that — but VS Code lets you open the project folder and see what exists, which helps you stay oriented as the codebase grows.

```
brew install --cask visual-studio-code
```

Or download directly from: https://code.visualstudio.com

**Open:** Press Cmd+Space, type "Visual Studio Code", and press Enter. Or find it in your Applications folder.

**Verify:** VS Code opens and shows a welcome screen with a file explorer on the left. To open your project folder, click File, then Open Folder, and select your project directory.

---

### 8. Typora *(optional but recommended — not free)*

**What:** A clean, distraction-free Markdown editor for reading and editing your project documents. Unlike VS Code which shows raw Markdown text, Typora renders it as formatted text in real time. The key advantage: you can edit your documents directly in the formatted view — no need to understand Markdown syntax. One-time purchase required.

```
brew install --cask typora
```

Or download directly from: https://typora.io

**Open:** Press Cmd+Space, type "Typora", and press Enter. Or find it in your Applications folder.

**Verify:** Typora opens and shows a blank document. Open any `.md` file from your project and it should display as formatted text, not raw code.

---

### 9. Claude Code

**What:** The AI coding assistant CLI. You type instructions in plain English and Claude writes, edits, and runs code on your behalf. This is the primary tool you will use for everything in this guide.

```
npm install -g @anthropic-ai/claude-code
```

You will need an Anthropic account and API key to use Claude Code. Sign up at https://console.anthropic.com.

**Open:** In your terminal, navigate to your project folder and type `claude`. This starts a Claude Code session in that folder. You can then type instructions in plain English.

**Verify:** Type the following and press Enter. A version number means it installed correctly.

```
claude --version
```

---

### 10. GitHub CLI

**What:** A terminal tool for managing your GitHub repository. Used to create issues, open pull requests, and check repository status without leaving the terminal. GitHub is where your code is stored and tracked online.

```
brew install gh
```

Authenticate with your GitHub account:

```
gh auth login
```

Follow the prompts. Choose GitHub.com and authenticate via browser.

**Open:** GitHub CLI runs in your terminal — there is no separate app. Type `gh` followed by a command to use it. For example, `gh issue list` shows your open issues.

**Verify:** Type the following and press Enter. A version number means it is working.

```
gh --version
```

---

### 11. Wrangler

**What:** Cloudflare's CLI for deploying the backend, running database migrations, and managing secrets. Only needed if you are using Cloudflare as your hosting platform.

```
npm install -g wrangler
```

You will need a Cloudflare account. Sign up at https://cloudflare.com.

**Open:** Wrangler runs in your terminal — there is no separate app. Claude uses it on your behalf to deploy code and run database commands. You will rarely need to type Wrangler commands yourself.

**Verify:** Type the following and press Enter. A version number means it is working.

```
wrangler --version
```

---

### Try It Out: Create Your Project Folder, Open Claude Code, and Set Up Your GitHub Identity

This is not a prerequisite — it is a practice run to confirm your tools are working together before you begin Phase 1.

1. Open Ghostty: press Cmd+Space, type "Ghostty", and press Enter
2. You are now in your home directory. Create a Projects folder:
```
mkdir projects
```
3. Navigate into it:
```
cd projects
```
4. Create your first project folder (replace `my-first-project` with your project name):
```
mkdir my-first-project
```
5. Navigate into it:
```
cd my-first-project
```
6. Zoxide has now learned this path. Next time you can skip steps 2 to 5 and jump directly here from anywhere by typing:
```
z my-first-project
```
7. Open Claude Code from inside this folder:
```
claude
```
8. Claude Code is now scoped to your project folder. You are ready to begin.

**Set up your GitHub identity (one-time only)**

Before your first commit, tell git who you are. This name and email will appear on every commit you make:

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Use the same email address linked to your GitHub account.

Then confirm your GitHub connection is working:

```
gh auth status
```

You should see your GitHub username and the account you authenticated with. If you see an error, run `gh auth login` and follow the prompts.

---

Once all tools are installed, return to [Phase 1: Define Your Idea](#phase-1-define-your-idea) and begin.
