**English** &nbsp;|&nbsp; [中文](learn-notes-zh.md)

<br>

<div align="center">

# Git Learning Notes

### *From zero to Git/GitHub. One question at a time.*

</div>

<br>

<p align="center">
  <a href="https://andyttc05.github.io"><img src="https://img.shields.io/badge/Live_Site-andyttc05.github.io-brightgreen?style=flat-square" alt="GitHub Pages"></a>
  <a href="https://github.com/andyttc05/my-first-repo/blob/main/learn-notes-zh.md"><img src="https://img.shields.io/badge/Notes-中文-%233498db?style=flat-square" alt="中文"></a>
  <img src="https://img.shields.io/badge/Teacher-Momo-ff69b4?style=flat-square" alt="Helper">
  <img src="https://img.shields.io/badge/Est.-2026.08-orange?style=flat-square" alt="Est.">
</p>

<br>

> "The best way to learn something is to write down every 'ohhh' moment before it fades."

---

## Core Git Concepts

### What is Git?

You know how you take a photo so you can look back at it later? Git is that, but for your code. You type `git commit` and it takes a snapshot of everything. Tomorrow you can flip back and see exactly what your code looked like. That's it. That's Git.

### The four zones

```
Working Directory        ✍️ where I write code
       ↓  git add        📋 "I want this one in the album"
Staging Area             📸 lined up for the photo
       ↓  git commit     📷 click! saved to the album
Local Repository         📚 the photo album on my computer
       ↓  git push       ☁️ uploaded to the cloud
GitHub (Remote)          🌐 a backup that never gets lost
```

### My account

| Field | Value |
| :--- | :--- |
| GitHub | [andyttc05](https://github.com/andyttc05) |
| Email | andyttc2463@gmail.com |
| Config | `~/.config/git/config` |

---

## Installing Git

Before anything else, you need Git. Nothing works without it.

### macOS (my setup)

```bash
brew install git
```

Check it worked:

```bash
git --version
# → git version 2.50.1
```

If you see a version number, you're good.

### Windows

Go to [git-scm.com](https://git-scm.com), grab the installer, keep clicking Next. Open **Git Bash** afterwards and run `git --version`.

### First thing: tell Git who you are

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Make sure the email matches your GitHub account. Otherwise your commits show up with no avatar, like a ghost.

---

<a id="first-push"></a>

## Your First Push: Step by Step

This one tripped me up on day one. Writing this down for the version of me that'll forget it in a week.

### ① Sign up for GitHub

Go to [github.com](https://github.com), click **Sign up**. Pick a username you actually like. It's going to show up on every commit forever.

### ② Create a repo on GitHub

Click the **+** in the top right → **New repository**. Give it a name. Pick Public or Private. Do *not* check "Add a README file". We'll make one ourselves.

After clicking **Create repository**, copy the URL. It'll look like `https://github.com/your-username/your-repo.git`.

### ③ Connect your local folder to GitHub

```bash
cd your-project-folder
git init
git add .
git commit -m "first commit"
git remote add origin <the-url-you-copied>
git push -u origin main
```

### ④ Tokens

GitHub stopped accepting passwords for push back in 2021. You need a Personal Access Token now.

GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic). Generate a new one, check `repo`, copy it. When pushing from the terminal, use your GitHub username and paste the token as the password.

The good news: install GitHub Desktop and you never touch tokens again. Browser auth handles it.

### ⑤ Check if it worked

Open `https://github.com/your-username/your-repo`. Your code should be sitting there. 🎉

---

## The Daily Three

```bash
git add .
git commit -m "what I did"
git push
```

Or skip the terminal. All three are one click each in GitHub Desktop.

---

<a id="branches"></a>

## Git Branches

A branch is a parallel timeline. You fork off from `main`, experiment freely, and when it works — merge it back. `main` stays clean the whole time.

### The concept

```
main    o---o---o-------o---o   never broken
            |               |
feature     o---o---o-------+   playground → merged
```

The feature branch starts as a copy of `main` at that point. Whatever you break there stays there. `main` doesn't even know it exists until you merge.

### In GitHub Desktop (no terminal)

**Create a branch**:

`Current Branch` → type a name → `New Branch` (based on `main`)

You're now on the new branch. The top bar shows its name.

**Work on the branch**:

Make changes in your editor. Commit like normal. The commits go to the branch, not `main`.

**Push & create a Pull Request**:

Click `Publish branch` → `Create Pull Request` → GitHub opens in your browser. Review the diff, add a description, click `Create pull request`.

**Merge**:

On the PR page, click `Merge pull request` → `Confirm merge`. The branch's changes are now part of `main`.

**Switch back to main**:

`Current Branch` → pick `main`. Click `Fetch origin` to pull in the merged changes.

### The whole flow at a glance

```
branch → changes → commit → push → PR → merge
   ↑                                       │
   └─────────── back to main ──────────────┘
```

### Merge a branch (without PR, locally)

Sometimes you don't need a Pull Request — just merge straight into `main`:

1. Switch to `main`: `Current Branch` → pick `main`
2. Menu bar: **Branch** → **Merge into Current Branch…**
3. Pick your feature branch from the list → click **Merge**

Done. The branch's commits are now on `main`. Push `main` to sync with GitHub.

### Delete a branch (after merge)

Once merged, the branch is dead weight. Clean it up:

1. `Current Branch` → right-click the branch name
2. Click **Delete…**
3. Confirm

Or from the menu: **Branch** → **Delete…** → pick the branch.

> 💡 GitHub Desktop will warn you if the branch hasn't been merged yet. That's a safety net — double-check before deleting.

### Discard a branch (abandon without merging)

Started something, realized it's the wrong direction, don't want to merge?

1. Switch back to `main`: `Current Branch` → pick `main`
2. `Current Branch` → right-click the unwanted branch → **Delete…**
3. Confirm

All commits on that branch are gone. The files on `main` never changed — it's like the branch never happened.

> ⚠️ If you already pushed the branch to GitHub, deleting it locally leaves the remote copy. Go to GitHub → the branch page → delete it there too.

| Scenario | Action |
| :--- | :--- |
| Branch done, merged via PR | Delete it — local and remote |
| Branch done, merged locally | Delete it |
| Branch abandoned, not merged | Delete it — `main` was never touched |
| Branch pushed but not merged | Delete local + remote |

---

<a id="github-desktop"></a>

## GitHub Desktop

This is my favorite tool. Everything is clicking buttons. Zero terminal.

### Setting it up

Go to [desktop.github.com](https://desktop.github.com), download, open the dmg, drag to Applications.

Launch it → **Sign in to GitHub.com** → browser opens → **Authorize**. That's it. No token, no password.

### The daily workflow

Open your editor, write some code. Switch back to GitHub Desktop. The **Changes** tab already lists everything. Write a summary, click **Commit to main**. Top bar now says **Push origin**. Click it and you're done.

No `git add`, no `git push`. Everything is auto-staged. One click to upload.

### Adding an existing repo

**File → Add local repository** → pick your folder. It shows up in the sidebar. Click to switch between repos anytime.

### Desktop and terminal get along fine

Commit in the terminal, GitHub Desktop sees it. Commit in Desktop, the terminal sees it. They share the same `.git` folder. No drama.

### Reverting to the cloud version

Sometimes you mess around, things get worse, and you just want a clean reset — back to what's on GitHub. Two ways to do this in GitHub Desktop.

#### Case 1: you haven't committed yet

Most common. You've edited files, the Changes tab is full, but you never hit Commit.

**How**: In the Changes tab, **right-click the file** → **Discard Changes…** → confirm. The file snaps back to the last commit.

To nuke everything at once: right-click any file → **Discard All Changes…**.

> ⚠️ Discard is final. No undo. Think twice before confirming.

Each file also has a little icon on the right (hover says "Revert file changes"). Clicking that does the same thing — faster than right-clicking.

#### Case 2: you committed locally but haven't pushed, and want to go back to origin

Say you made a few local commits, realized you went the wrong direction, and want to be back at `origin/main`.

**How**:

1. Switch to the **History** tab
2. Find the remote commit — usually labeled `origin/main` (or your branch name)
3. **Right-click** that commit → **Reset to Commit → Hard**
4. Confirm → your local is now identical to the remote

> ⚠️ Hard reset is final. Those local commits are gone.

#### Quick reference

| Situation | Action | Where |
| :--- | :--- | :--- |
| Edited files, not committed | Discard Changes | Changes tab |
| Committed locally, not pushed | Reset to Commit (Hard) | History → right-click origin commit |

---

## PyCharm + GitHub Desktop

### How they sync (or don't)

The first time I noticed this I stared at the screen for a bit. They don't need me to sync them. They just look at the same folder. Like two people reading the same book, no passing notes.

```
PyCharm opens ~/Documents/my-first-repo     ✍️ writing code
              ↓ saves files
     my-first-repo folder                   📁 the book
              ↓ auto-detected
  GitHub Desktop shows changes ✓            👀 already knows
```

No cables. No config file. No sync button. The folder changes, GitHub Desktop notices. That's the whole trick.

You just need PyCharm to open this folder, and GitHub Desktop to open the same folder. Nothing else.

### The actual steps

Write code in PyCharm. It auto-saves when you switch windows. Switch to GitHub Desktop. The changes are already listed on the left. Type a summary like "fixed that bug" or "login page done". Click **Commit to main**. The top bar now says **Push origin**. Click it. Done.

---

## PyCharm Setup

| Setting | Value | Path |
| :--- | :--- | :--- |
| Theme | Light (dark mode is overrated) | Settings → Appearance |
| Font size | 15 | Settings → Editor → Font |
| Auto-save | On window switch | Settings → System Settings |

---

<a id="workbuddy"></a>

## WorkBuddy

A desktop AI agent — think Claude, but workspace-native. Each project lives in its own workspace folder, and the agent can read your files, run commands, edit code, and talk to external services through connectors.

### Workspace model

WorkBuddy organizes work by workspace. Each workspace is a folder like `~/WorkBuddy/2026-08-03-16-17-13/`. Inside it: your project files, a `.workbuddy/` folder for memory and logs, and the agent's full context.

Switching projects is opening a new workspace. Everything is isolated. No cross-contamination.

### The three superpowers

| Power | What it does | Real example |
| :--- | :--- | :--- |
| **Skills** | Pre-built workflows the agent loads on demand | `momo` skill sets my assistant's personality; `data-maintenance` runs cleanup |
| **Automations** | Scheduled tasks that run on a timer | Daily self-evolution audit, system cleanup at 2 AM |
| **Connectors (MCP)** | Plug into external services | Lexiang knowledge base, Tencent Docs, WeChat Pay, Agent Mail |

### My active connectors

| Connector | What I use it for |
| :--- | :--- |
| **Lexiang** | Knowledge base — search, read, write docs |
| **Tencent Docs** | Online document creation and editing |
| **WeChat Pay** | Payment and agent card management |
| **Agent Mail** | Email in the agent interface |
| **ima** | Personal knowledge base search |

### How I actually use it

WorkBuddy is where I do my structured work. Not quick one-offs — the stuff that needs a plan, multiple steps, and a record of what happened.

**Daily rhythm**: open WorkBuddy → pick up where I left off → agent reads my workspace memory → do the work → memory auto-logged.

**Learning Git with WorkBuddy**: I ask Momo (my WorkBuddy persona) to explain concepts, edit my notes in real time, and guide me through operations. WorkBuddy reads my entire `my-first-repo` folder, so it always knows the context.

**The real win**: the `.workbuddy/memory/` folder. Every session leaves a daily log. The agent remembers what we talked about yesterday, what we decided, what's still open. I never have to re-explain.

### Key paths

| What | Where |
| :--- | :--- |
| App | `/Applications/WorkBuddy.app` |
| Workspaces | `~/WorkBuddy/` |
| Memory (per workspace) | `.workbuddy/memory/` |
| Skills (user-level) | `~/.workbuddy/skills/` |
| Global memory | `~/.workbuddy/MEMORY.md` |

---

<a id="claude-code"></a>

## Claude Code

Anthropic's command-line AI coding agent. Unlike the desktop chat app, Claude Code lives in your terminal — you `cd` into a project and run `claude`, and it reads your entire codebase and starts helping.

### Why Claude Code

It's a terminal-native tool. No GUI, no separate window — just you, your shell, and an agent that knows your project. Great for quick edits, code reviews, and terminal-heavy workflows where you're already in the zone.

### Installation

```bash
# Install via npm
npm install -g @anthropic-ai/claude-code

# Or with Homebrew
brew install claude-code

# Start it in any project
cd your-project
claude
```

### What it can do

| Capability | How it helps |
| :--- | :--- |
| Full repo context | Reads your entire project folder at once |
| Terminal-native | Runs shell commands, git operations, build scripts |
| Direct edits | Writes and modifies files in place |
| Git integration | Understands branches, diffs, and commit history |
| Multi-model | Claude by default, switchable via CC Switch |

### Using CC Switch to connect DeepSeek

Claude Code uses Claude's own model by default. CC Switch lets you swap in DeepSeek (or others):

1. Download [CC Switch](https://github.com/cc-switch/cc-switch) — a model switcher for Claude Code
2. Configure your DeepSeek API key following the setup guide
3. Restart Claude Code — toggle between Claude and DeepSeek

Same CLI, pick the model that fits the task.

### Claude Code vs WorkBuddy

| | Claude Code | WorkBuddy |
| :--- | :--- | :--- |
| Interface | Terminal CLI | Desktop app |
| Best for | Quick coding help, terminal-native | Structured projects, workflows |
| State | Stateless per session | Persistent memory per workspace |
| Strengths | Speed, simplicity, git-aware | Automation, connectors, memory |

They complement each other. Claude Code is my quick-draw coding buddy. WorkBuddy is where I plan, organize, and log everything.

### My tool chain

```
WorkBuddy               🧠 planning, editing, automation
       ↓
Claude Code             🔧 quick coding, model switch
       ↓
PyCharm                 💻 review & hand-edit code
       ↓
GitHub Desktop          🚀 commit & push to GitHub
```

All four tools share the same project folders. Each one does what it's best at.

### Quick setup check

```bash
# Make sure Claude Code is installed
claude --version

# Grant terminal access if needed
# System Settings → Privacy & Security → Developer Tools → Terminal
```

---

<a id="github-pages"></a>

## GitHub Pages: My First Website

This was my first detour outside of Git itself. Didn't realize until later that Git was quietly handling the whole thing anyway.

### What I built

Made the `andyttc05.github.io` repo. GitHub saw the name and turned Pages on automatically. Wrote everything in plain HTML and CSS. No frameworks, no build tools, just a few files. Split into `index.html` (EN) and `zh.html` with a card toggle to jump between them. Threw in some Pull Quotes, fade-in animations, alternating section backgrounds. Made it work on different screen sizes. Then spent way too long hunting down a Safari hover color bug on the contact links. Got it eventually.

### What clicked

| Concept | Takeaway |
| :--- | :--- |
| GitHub Pages | Name a repo `username.github.io` and it auto-deploys. Free domain |
| Static sites | HTML + CSS. Opens in a browser. No server needed |
| Bilingual design | Two files, a card toggle, page reloads on switch |
| Design iteration | Edit in PyCharm, commit in Desktop, live in 30 seconds |

---

## Open Source License

### Why you need one

Posting code on GitHub doesn't mean others can legally use it. Copyright law defaults to "all rights reserved" — no License means people can look but can't touch.

Adding a License says: hey, you can use my code, just follow these few rules.

### Common licenses at a glance

| License | In one sentence |
| :--- | :--- |
| MIT | Do whatever! Modify it, sell it, just keep my name on it |
| Apache 2.0 | Like MIT, plus patent protection. Big companies love it |
| GPL | You can use it, but your changes must also be open source |

### My pick: MIT

Went with MIT. Most permissive, most popular. Anyone can use, modify, or sell it — as long as they keep my copyright notice.

### How to add a License

**One-click on GitHub**:

1. Repo homepage → **Add file** → **Create new file**
2. Name it `LICENSE`
3. Click **Choose a license template** on the right
4. Pick MIT, fill in year and name → **Review and submit**
5. Commit → done

Also works in GitHub Desktop: create a file called `LICENSE` (no extension) in your repo folder, paste in the license text, and Push.

> 💡 MIT doesn't expire — no renewal needed. Some people update `2026` to `2026-2027`, but it's entirely optional.

---

## Common Pitfalls

<details open>
<summary>Pitfall 1: "No local changes" is not an error</summary>
<br>

After you commit and push, your workspace goes quiet. "No local changes" is Git's way of saying everything is accounted for. Nothing got left behind.

</details>

<details open>
<summary>Pitfall 2: .gitignore has a blind spot</summary>
<br>

`.gitignore` only watches untracked files. Files you've already `git add`-ed? It pretends they don't exist.

To fix it:

```bash
git rm --cached -r path/to/file
```

This removes the file from staging but keeps it on disk.

</details>

<details open>
<summary>Pitfall 3: You can't lose a repo by moving it</summary>
<br>

A Git repo is just a folder with a hidden `.git` directory inside. That `.git` directory carries everything: your history, where it connects to, every snapshot.

You can drag the whole folder anywhere and it still works. Only thing to remember: GitHub Desktop needs **File → Add local repository** pointed to the new spot.

</details>

---

## Tool Chain

| Tool | Status |
| :--- | :---: |
| **WorkBuddy** | ✅ |
| **Claude Code** | ✅ |
| **GitHub Desktop** | ✅ |
| **PyCharm** (Light, font 15) | ✅ |
| **GitHub Pages** → [andyttc05.github.io](https://andyttc05.github.io) | ✅ |
| **Git** | ✅ |

### Key paths

| What | Where |
| :--- | :--- |
| Repo | `~/Documents/my-first-repo` |
| Remote | `https://github.com/andyttc05/my-first-repo` |
| Git config | `~/.config/git/config` |

---

## How to Reset Tools

Move the config folder to `/tmp/` and the tool forgets everything. Clean start:

```bash
# PyCharm
mv ~/Library/Application\ Support/JetBrains/PyCharm2026.1 /tmp/removed-pycharm

# GitHub Desktop
mv ~/Library/Application\ Support/GitHub\ Desktop /tmp/removed-github-desktop
```

Old config sits in `/tmp/`. It's not gone. Go get it if you change your mind.

---

## Rewriting Git History (Advanced)

Be smart about this one. Rewriting commit hashes breaks things for anyone who cloned your repo. Two reasons to use it: you accidentally committed a password or API key, or your commit history looks like a scratch pad and you want a do-over.

### Scenario A: Replace sensitive strings everywhere

```bash
cd ~/path/to/your-repo

git filter-branch --force --tree-filter \
  "grep -rl 'string-to-replace' . 2>/dev/null | xargs -I{} sed -i '' 's|old-string|new-string|g' {}" \
  --prune-empty -- --all
```

Push the cleaned version:

```bash
git push --force-with-lease origin main
```

`--force-with-lease` is safer than `--force`. It refuses if someone else pushed since you last pulled.

### Scenario B: Wipe history, keep files

```bash
cd ~/path/to/your-repo

git checkout --orphan clean-slate
git add -A
git commit -m "clean slate"
git push --force origin clean-slate:main
```

Then clean up locally:

```bash
git checkout main
git reset --hard origin/main
git branch -D clean-slate
```

### Scenario C: Full workflow (dirty history → clean repo)

```bash
cd ~/path/to/your-repo

# Replace sensitive strings
git filter-branch --force --tree-filter \
  "grep -rl '/Users/your-name/' . 2>/dev/null | xargs -I{} sed -i '' 's|/Users/your-name/|~/|g' {}" \
  --prune-empty -- --all

# Push cleaned version
git push --force-with-lease origin main

# Or nuke everything, keep only current files
git checkout --orphan clean-slate
git add -A
git commit -m "clean slate"
git push --force origin clean-slate:main

# Clean up
git checkout main
git reset --hard origin/main
git branch -D clean-slate
```

### What I learned from doing this

| Lesson | Detail |
| :--- | :--- |
| Check before you commit | Run `git diff` first. Keep secrets out of your history |
| You'll need the terminal | GitHub Desktop doesn't support force push |
| Don't just `--force` | `--force-with-lease` is safer. It'll say no if someone else pushed since you last pulled |
| Terminal push needs a token | Desktop uses OAuth. Terminal still wants a PAT. See [Your First Push](#first-push) step ④ |
| Clean up after yourself | `branch -D` to delete temporary branches |
| Reset after force push | After `--force`, local and remote main have different histories. `git pull` won't work. Run `git fetch origin && git reset --hard origin/main` to get them back in sync |

---

## What's Next

Branches are in the toolbox now. Next up: probably an actual Python project — start small, use branches, build something that works. After that, maybe GitHub Actions to auto-deploy the website on every push. Or maybe VS Code instead of PyCharm for a week, just to see. No rush. Whatever feels fun next.

---

<br>

<div align="center">

> "Every expert started by typing `git init` for the first time. These notes are what that looks like."

</div>
