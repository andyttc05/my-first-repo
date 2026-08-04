**English** &nbsp;|&nbsp; [中文](git-github-guide-zh.md)

<br>

<div align="center">

# Git + GitHub Core Concepts

</div>

<br>

> **Core Philosophy**: Learning Git in the AI era is not about memorizing commands — it's about **understanding core concepts**. Once you grasp them, you can direct AI to perform all Git operations in natural language. **Get the meaning, forget the words.**

---

## Table of Contents

- [Introduction](#introduction)
- [1. Understanding Git and GitHub](#1-understanding-git-and-github)
- [2. Environment Setup](#2-environment-setup)
- [3. Commit: Saving Snapshots](#3-commit-saving-snapshots)
- [4. Branch: Branch Management](#4-branch-branch-management)
- [5. WorkTree: Parallel Dev](#5-worktree-parallel-dev)
- [6. Git Four Zones](#6-git-four-zones)
- [7. Remote Repos](#7-remote-repos)
- [8. GitHub Basics](#8-github-basics)
- [9. GitHub Collaboration](#9-github-collaboration)
- [Common Mistakes](#common-mistakes)
- [Must-Know List](#must-know-list)
- [Core Mindset](#core-mindset)

---

## Introduction

"AI can write code for me now — do I still need to learn Git?"

**Quite the opposite.**

AI coding tools all run on top of Git. When they initialize projects, create branches, commit code, or resolve conflicts — the underlying operations are all Git.

> **Git is a fundamental skill in the AI era, not optional.**

The good news: we don't need to memorize commands. Just master the core concepts, and direct AI in natural language.

```
Traditional: type commands manually, search docs, browse Stack Overflow
AI way:      understand concepts -> direct AI -> AI executes
```

---

## 1. Understanding Git and GitHub

### 1.1 The Thesis Story

Anyone who's written a thesis knows this:

```
Thesis_v1.docx
Thesis_v2.docx
Thesis_v3.docx
Thesis_final.docx
Thesis_final_final.docx
```

Carefully saving each version — that's **version control in its most primitive form**.

### 1.2 Git

| Concept | Description |
|---------|-------------|
| **Git** | Free open-source **version control** software |
| **Repository** | A folder managed by Git |
| **Commit** | Basic unit of version control; saves a **complete snapshot** |
| **Branch** | Independent line of development; branches are isolated |

### 1.3 Local vs Remote

| Concept | Description |
|---------|-------------|
| **Local Repository** | Git repo on your own computer |
| **Remote Repository** | Git repo on a server, for backup, sharing, collaboration |
| **GitHub** | Free remote repo hosting; world's largest code collaboration platform |

### 1.4 GitHub = Git + Hub

- **Git**: version control tool
- **Hub**: center, gathering place
- **Together**: a website hosting Git repositories

**What GitHub does:** store code, backup, share, collaborate, host open source, submit Issues and Pull Requests.

| Type | Meaning |
|------|---------|
| **Public** | Everyone can see |
| **Private** | Only owner + invited collaborators |

> Also: GitLab, Bitbucket. Learn GitHub and the others are easy.

---

## 2. Environment Setup

### 2.1 Register GitHub
[github.com](https://github.com/) → **Sign up**.

### 2.2 Install Git
**Windows:** [git-scm.com](https://git-scm.com/) → download → next, next, next.

**Mac:**
```bash
xcode-select --install
```

**Verify:**
```bash
git --version
```


### 2.3 GitHub Desktop
GitHub's official **graphical Git client** — turns command-line operations into button clicks. Commits, branches, pushes — all doable inside Desktop.

1. Go to [desktop.github.com](https://desktop.github.com), download and install
2. Open → **Sign in to GitHub.com** → browser popup → click **Authorize**
3. Automatically returns to Desktop — signed in

> 💡 OAuth handles authentication — no token needed. Sign in once, never type a password for push/pull again.

> 💡 GitHub Desktop and CLI share the same `.git` directory — no conflicts. Use Desktop for daily work, switch to CLI for force push or rebase.

### 2.4 Install VSCode
[code.visualstudio.com](https://code.visualstudio.com/) → download → install. This is our **code editor** — write and edit files here.

### 2.5 Bind AI Agent to Git and GitHub
This is the **key step** in the AI era — let AI handle initialization and push.

1. Create an empty folder
2. Select it as the project directory in your AI Agent
3. Prompt: "Init this folder as a Git project and push to GitHub"
4. AI asks for remote repo URL
5. Create a repo on GitHub, get the URL
6. Paste to AI Agent — authorized

> Once bound, all Git ops via natural language.

### 2.6 `git init` — Initialize
```bash
git init
```

Creates a `.git` subdirectory storing all version control data.

```
Before init:               After init:
my-project/                my-project/
                             .git/        <-- stores version control info
                             (other project files)
```

> ⚠️ Delete `.git/` and the repo is gone, history lost.

### 2.7 `.gitignore` — Declare Untracked Files
Files that should NOT be tracked or uploaded.

| File/Dir | Why |
|----------|-----|
| `.env` | May contain API keys, passwords |
| `node_modules/` | Reinstallable via `npm install` |
| `.DS_Store` | macOS system file |
| `*.log` | Log files |

**Example:**
```gitignore
.env
node_modules/
.DS_Store
*.log
dist/
.cache/
```

> ⚠️ Create `.gitignore` at project initialization!

**AI Prompt:**
> "Initialize the current directory as a Git project. Create an appropriate .gitignore excluding .env, node_modules, log files, and cache files."

### 2.8 Daily Essential Commands
These three commands are the most frequently used — run them before and after every commit:

| Command | Purpose | Example |
|---------|---------|---------|
| `git status` | Check current state: what's modified, what's staged | Run before every operation |
| `git diff` | See exactly what changed (unstaged changes) | `git diff` / `git diff --staged` |
| `git log --oneline` | View commit history, find Commit IDs | `git log --oneline -5` (last 5) |

```bash
git status              # "Where am I? What changed?"
git diff                # "What exactly changed?"
git diff --staged       # "What's in the staging area?"
git log --oneline       # "Show me the history so I can find a Commit ID"
```

> 💡 Make it a habit: `git status` before every action, `git diff` before committing, `git log` to find Commit IDs for rollback.

### 2.9 SSH Key Authentication (Optional)
GitHub supports two auth methods: HTTPS (needs a token) and SSH (set up once, password-free forever).

```bash
# 1. Generate SSH key
ssh-keygen -t ed25519 -C "your-email@example.com"
# Press Enter for defaults

# 2. Copy the public key
cat ~/.ssh/id_ed25519.pub

# 3. Paste into GitHub → Settings → SSH and GPG keys → New SSH key
# 4. Test the connection
ssh -T git@github.com
# Seeing "Hi username!" means success
```

> 💡 After SSH setup, clone with `git@github.com:username/repo.git` format — no more password prompts.

## 3. Commit: Saving Snapshots

### 3.1 What is a Commit

A **Commit** is the **basic unit** of Git version control. Each commit takes a snapshot, saving the state of all files.

**What commits do:** save project state, record who changed what, form a traceable history, support rollback and comparison, enable collaboration.

### 3.2 Commit Message

Every commit needs a message:

```
Add login page
Fix user profile bug
Update README documentation
```

**Convention:** concisely explain "what was done." Use [Conventional Commits](https://www.conventionalcommits.org/) format: `feat:` new feature, `fix:` bug fix, `docs:` documentation, `chore:` maintenance. Consistent format keeps history readable.

### 3.3 Commit ID / Commit Hash

Each commit gets a unique hash:

| Type | Characteristic |
|------|----------------|
| **Long ID** | Full 40-character hash |
| **Short ID** | First 7 characters, daily use |

> When communicating with AI, always provide the Commit ID.

### 3.4 Best Practice: Commit Frequently

```
1. AI completes login page -> test passes -> Commit
2. AI completes registration page -> test passes -> Commit
3. AI completes profile page -> test passes -> Commit
```

**Benefits:** quick rollback, clear history, less chance of messing up.

### 3.5 Three Ways to Undo

#### Discard — Abandon Uncommitted Changes

| Item | Description |
|------|-------------|
| **Use case** | Files modified but **not yet committed** |
| **Effect** | Abandon changes, restore to last commit |
| **Risk** | Changes **permanently lost** |

#### `reset` — Force Rollback

```bash
git reset --hard <commit-id>
```

| Item | Description |
|------|-------------|
| **Use case** | Go back to a historical commit, discard all after |
| **Risk** | If pushed, needs `git push -f` |
| **Scope** | **Local, single-person branches only** |

#### `revert` — Inverse Commit

```bash
git revert <commit-id>
```

| Item | Description |
|------|-------------|
| **Use case** | Undo a specific erroneous commit, keep other history |
| **Effect** | Creates an "inverse commit", does not destroy history |
| **Scope** | **Recommended for shared branches** |

#### Comparison

| Operation | Function | Use Case | Risk |
|-----------|----------|----------|------|
| **Discard** | Abandon uncommitted changes | Before commit | Changes lost |
| **Reset** | Go back to a historical commit | Local, single-person | May delete history |
| **Revert** | Inverse-cancel a commit | Shared branches | **Safest** |

> 💡 In collaboration, **revert is safer than reset**.

**AI Prompts:**
> "Check current changes, summarize modifications, generate an appropriate commit message. Complete commit after confirming no sensitive files."
>
> "Roll back to commit abc1234. Tell me which commits will be deleted before executing."
>
> "Revert changes from commit abc1234, keeping all other commits. Prefer revert over reset."

#### Ultimate Safety Net: `git reflog`

If you accidentally `reset --hard` and deleted something important — don't panic. Git almost never truly deletes data.

```bash
git reflog
# Shows every movement of HEAD, including deleted commits
# Find the commit ID you want back, then:
git reset --hard <that-commit-id>
```

`reflog` records every position change of HEAD, kept for 90 days by default. It's the "undo button for your undo button."

---

## 4. Branch: Branch Management

### 4.1 What is a Branch

A **Branch** is an independent line of development. Default main branch is `main` or `master`.

```
X Wrong: develop on main directly
   -> may break stable code

O Right:
   main --------------------> (stable)
     \___ feature/login ---> (new feature dev)
                 | testing passes
   main <-- merge --- feature/login
```

### 4.2 Branch Characteristics

- New branch code is **identical** to source branch
- Changes on a branch **do not affect main**
- After development, merge back to main

### 4.3 Naming Conventions

```
feature/login-page        # new feature
feature/payment           # new feature
fix/header-bug            # bug fix
hotfix/security-patch     # emergency fix
```

### 4.4 Core Workflow

```
1. Create a new branch from main
2. Develop and commit on the new branch
3. Merge back to main
4. Delete merged branch (optional)
```

> ⚠️ Git won't let you delete the branch you're on — switch first.

### 4.5 HEAD Pointer

**HEAD** points to the current commit:

| State | HEAD Points To |
|-------|---------------|
| On `main` branch | `main`'s latest commit |
| On `feature` branch | `feature`'s latest commit |
| Checked out a historical commit | That commit → **Detached HEAD** |

**Detached HEAD:** HEAD points to a historical commit, not a branch tip. View history here, but **don't make changes**. Create a new branch to continue development.

### 4.6 Merge Conflicts

When **two branches modify the same line of the same file**, Git doesn't know which to keep → conflict.

You choose: keep A's version, keep B's version, keep both, or create a new result.

**AI Prompts:**
> "Merge these two branches. If conflicts arise, stop and tell me the conflicting files. Do not auto-decide."
>
> "Resolve the current merge conflict. When the same line has two versions, keep both."

### 4.7 Cherry-pick — Selective Merge

Pick specific commits from a branch and apply them to the current branch.

Feature branch has 3 commits:
1. Create vegetable list
2. Create meat list
3. Create staple food list

You only want 1 and 3 merged to main. Use cherry-pick.

**AI Prompt:**
> "Cherry-pick commits `abc1234` `def5678` to main. Do not merge the branch's other commits."

### 4.8 Rebase

Move current branch's commits to "sit on top of" the target branch's latest commit.

```
Merge (preserves fork):
main:     A---B---C---M
                \     /
feature:         D---E

Rebase (linear history):
main:     A---B---C
                    \
feature:             D'---E'
```

**Advantage:** cleaner history, no extra merge commits.

**Risk:** rewrites commit history. Pushed branches need `git push -f` after rebase.

> ⚠️ **rebase + force push is for personal branches only**. Never on shared branches.

| Operation | Characteristic | Use Case |
|-----------|---------------|----------|
| **Merge** | Preserves branch merge history | Team collaboration, public branches |
| **Rebase** | Clean history, but rewrites | Personal feature branches |

**AI Prompts:**
> "Create a new branch feature/login-page from main. Develop the login page on this branch."
>
> "Merge feature/login-page into main. Stop and tell me if conflicts arise."
>
> "Rebase current feature branch onto latest main. State whether force push is needed and the risks."

---

## 5. WorkTree: Parallel Dev

### 5.1 What is WorkTree

**Git Worktree** creates independent working directory folders for different branches of the same repo.

### 5.2 Use Cases

- Multiple AI Agents developing different features in parallel
- Fix a bug while developing a new feature, no interference
- Avoid frequent branch switching
- Isolate experiments

### 5.3 Structure

```
Repo .git/
  +-- main/          (worktree 1 -- main)
  +-- feature-a/     (worktree 2 -- Feature A)
  +-- feature-b/     (worktree 3 -- Feature B)
```

- Each worktree = one branch, independent folder
- Changes don't interfere
- Merge back to main when done

**AI Prompt:**
> "Create a new worktree and branch for developing the login feature. Commit when done and merge back to main."

---

## 6. Git Four Zones

This is Git's **most important theoretical foundation**. Master it and all commands make sense.

### 6.1 The Four-Zone Model

```
+------------------+     git add     +----------------+    git commit    +------------------+
|     Working      |  ----------->   |    Staging     |  ------------>   |      Local       |
|    Directory     |                 |      Area      |                  |    Repository    |
+------------------+                 +----------------+                  +--------+---------+
                                                                                  |
                                                                         git push | git pull
                                                                                  |
                                                                                  v
                                                                         +--------+---------+
                                                                         |     Remote       |
                                                                         |    Repository    |
                                                                         |     (GitHub)     |
                                                                         +--------+---------+
```

### 6.2 Zone Descriptions

| Zone | Description | Operation |
|------|-------------|-----------|
| **Working Directory** | Project folder where you edit code | Edit files |
| **Staging Area** | "Shopping cart" before committing | `git add` |
| **Local Repo** | Where committed code is stored | `git commit` |
| **Remote Repo** | Repository on GitHub | `git push` / `git pull` |

### 6.3 Data Flow

```
Working Dir -> git add -> Staging Area -> git commit -> Local Repo -> git push -> Remote Repo
Remote Repo -> git pull (fetch + merge) -> Local Repo + Working Dir
Remote Repo -> git clone -> Local Repo + Working Dir (fresh copy)
```

> 💡 VSCode merges add and commit by default.

### 6.4 Stash — Temporary Storage

> ⚠️ `stash` and `staging area` are **completely different concepts**!

**Use case:** You're coding on a feature branch, halfway through. Suddenly need to switch to main for an urgent bug.

**Two options:**
1. Make a temporary commit
2. Use `stash` — **Recommended**

**Effect:** temporarily save unfinished changes, clear working directory, switch branches. Come back and `pop` to resume.

```bash
git stash      # save
git stash pop  # restore
```

**AI Prompts:**
> "I have uncommitted code. Please stash them, then switch to main."
>
> "Switch back to feature branch and pop the stashed changes."

---

## 7. Remote Repos

### 7.1 `git clone` — Copy Remote to Local

```bash
git clone <repo-url>
```

Download a project from GitHub, auto-creating local repo and working directory.

### 7.2 `git push` — Upload Local Commits

```bash
git push
```

Upload local commits to GitHub.

> ⚠️ Only repo admins or authorized collaborators can push. Can't push to someone else's repo.

### 7.3 `git pull` — Fetch Remote Updates

```bash
git pull
```

Fetch latest remote code and merge into local branch.

**`git pull` equals:**
```bash
git fetch    # fetch remote updates
git merge    # merge into local
```

### 7.4 What is `origin/main`

- **`origin`** = remote repo alias (default name)
- **`origin/main`** = `main` branch on remote
- **`main`** = `main` branch locally

| Status | Meaning |
|--------|---------|
| Local `main` ahead of `origin/main` | Local commits not pushed → `git push` |
| `origin/main` ahead of local `main` | Someone updated remote → `git pull` |

**AI Prompt:**
> "Merge upstream main's latest changes into the current feature branch. Let me choose if there are conflicts."

### 7.5 `git remote` — Manage Remote Connections

```bash
git remote -v                    # List current remote repos
git remote add <name> <url>      # Add a new remote
```

For example, after forking someone's project, add the upstream:
```bash
git remote add upstream https://github.com/original-owner/repo.git
git fetch upstream               # Pull upstream updates
git merge upstream/main          # Merge into local
```

### 7.6 `git tag` — Version Tags

Tag important commits, typically for marking releases:

```bash
git tag v1.0.0                        # Lightweight tag
git tag -a v1.0.0 -m "First release"  # Annotated tag (recommended)
git push origin v1.0.0                # Push a single tag
git push origin --tags                # Push all tags
```

---

## 8. GitHub Basics

### 8.1 Repository URL

```
https://github.com/username/repo-name
```

Example: `github.com/docmirror/dev-sidecar` → middle is author, end is repo name.

### 8.2 Core Areas

**Code:** browse source, download ZIP, copy clone URL.

**README:** project description, auto-displayed on repo homepage.

**Releases:** version numbers, changelogs, packaged install files.

### 8.3 About / Star / Fork

| Feature | Meaning |
|---------|---------|
| **About** | Project description, tags, license |
| **Star** | Like + bookmark |
| **Fork** | Copy someone's project to your account |

### 8.4 Issues

Report bugs, propose features, search problems, join discussions.

| Status | Meaning |
|--------|---------|
| **Open** | Unresolved / under discussion |
| **Closed** | Resolved |

### 8.5 GitHub Shortcuts

| Key | Function |
|-----|----------|
| `/` | Open search |
| `T` | Quick file search in repo |
| `L` | Jump to line number |
| `.` | Open web-based VSCode |
| `?` | View all shortcuts |
| `G` + `C` | Jump to Code |
| `G` + `I` | Jump to Issues |

### 8.6 Git Blame

Shows commit info per line: who, which commit, when.

> For investigating: "Who changed this line? Why?"

### 8.7 Codespaces

GitHub's **remote dev environment**. Open a VS Code-style editor in the browser. Run, debug, and commit code — all online.

### 8.8 GitHub Pages (Free Hosting)

Turn a repo into a live website at `https://username.github.io`:

1. Create a public repo named `username.github.io`
2. Upload HTML/CSS files (entry point must be `index.html`)
3. Settings → Pages → pick branch → Save
4. Wait ~30 seconds, visit `https://username.github.io` — live

> 💡 Perfect for personal sites, project docs, portfolios. Zero cost for static sites.

### 8.9 Profile README

Create a repo with **the same name as your GitHub username**. Its `README.md` automatically appears at the top of your GitHub profile page. Add an intro, skills, project links — your GitHub business card.

---

## 9. GitHub Collaboration

### 9.1 Open Source: Fork + Pull Request

**Use case:** You can't directly modify someone else's repo but want to contribute.

```
+------------------------------------------------------+
|  1. Fork                                             |
|     Original repo ----> Your GitHub account          |
|                                                      |
|  2. Clone                                            |
|     Your repo ----> Local machine                    |
|                                                      |
|  3. Create a new branch (do NOT modify main)         |
|     git checkout -b feature/my-contribution          |
|                                                      |
|  4. Edit code -> Commit -> Push to your GitHub repo  |
|                                                      |
|  5. Create Pull Request                              |
|     Your repo -> Original repo (request merge)       |
|                                                      |
|  6. Maintainer does Code Review                      |
|                                                      |
|  7. Approved -> Merge -> Your code enters the project|
+------------------------------------------------------+
```

### 9.2 What is a Pull Request

**PR = Merge Request**

"I made changes on this branch. Please merge them into the target branch."

**What you see in a PR:** changed files, added/removed code, commit history, discussions, Code Review comments.

### 9.3 Sync Upstream Before PR

```
1. Develop on your feature branch
2. Before PR, merge upstream main's latest code into your feature branch
3. Resolve conflicts locally
4. Push
5. Then create the PR
```

> **Why:** a branch far behind upstream may cause conflicts, reducing acceptance chance.

### 9.4 Team Collaboration: Collaborator Mode

When added as a Collaborator, you don't need to Fork:

```
1. Clone the original repo directly
2. Create your own feature branch
3. Edit code
4. Commit
5. Push to the remote feature branch
6. Create a PR from feature branch to main
7. Admin does Code Review
8. Merge to main
```

> ⚠️ Even with push permissions, don't modify `main` directly. Always use **branch + PR**.

**AI Prompt:**
> "Here is the upstream repo URL: <repo-url>. Merge upstream main's latest into current feature branch. Let me choose if there are conflicts."

### 9.5 Protected Branches

In team projects, set up protection rules for the `main` branch on GitHub:

**Path:** Repo → Settings → Branches → Add branch protection rule

**Common rules:**
- Block direct pushes to `main` (enforce PR workflow)
- Require PR reviews and approvals before merging
- Require CI tests to pass before merging

> 💡 This turns "conventions" into "enforcement" — the tool guards the rules so you don't accidentally break them.

---
## Common Mistakes

| # | Mistake | Correct |
|---|---------|---------|
| 1 | **Git and GitHub are the same** | Git = tool; GitHub = hosting site |
| 2 | **Commit uploads to GitHub** | `git commit` is local; `git push` uploads |
| 3 | **Direct push to someone's repo** | No permission → Fork → PR |
| 4 | **Develop directly on main** | Use feature branches, merge via PR |
| 5 | **Confuse reset and revert** | reset rewrites history (local); revert creates inverse (shared) |
| 6 | **Code in detached HEAD** | View only; create a branch to make changes |
| 7 | **Casual rebase + force push** | Personal branches only |
| 8 | **Commit .env** | Always add to .gitignore |
| 9 | **Commit node_modules** | Add to .gitignore |
| 10 | **PR without syncing upstream** | Sync → resolve → then PR |

---

## Must-Know List

| # | Concept | One-Liner |
|---|---------|-----------|
| 01 | **Git** | Version control tool |
| 02 | **GitHub** | Remote repo hosting platform |
| 03 | **Repository** | A folder managed by Git |
| 04 | **Commit** | Save a project snapshot |
| 05 | **Commit ID** | Unique identifier per commit |
| 06 | **Branch** | Isolate development |
| 07 | **Merge** | Combine branches |
| 08 | **Pull / Push** | Fetch / upload remote code |
| 09 | **Pull Request** | Request to merge into a target branch |
| 10 | **Revert over Reset** | Safer in collaboration |

---

## Core Mindset

```
Get the meaning, forget the words.

Master the core concepts — you don't need to memorize commands.
Understand commits, branches, merges, conflicts, and the four-zone model,
and AI becomes your best Git operator.
```

---

> 📝 This document covers all Git and GitHub core concepts, practical workflows, and advanced operations.
