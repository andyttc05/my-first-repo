**English** &nbsp;|&nbsp; [中文](学习笔记.md)

<br>

<div align="center">

# &nbsp;Git Learning Notes

### &nbsp;*From zero to Git/GitHub — a two-day evolution*

<br>

> &nbsp;&nbsp;Teacher: **Momo** 🍑 &nbsp;·&nbsp; Student: **andyttc05** &nbsp;·&nbsp; Est. 2026.08

<br>

[Timeline](#-learning-timeline) &nbsp;·&nbsp;
[Install Git](#-installing-git) &nbsp;·&nbsp;
[First Push](#first-push) &nbsp;·&nbsp;
[Desktop](#github-desktop) &nbsp;·&nbsp;
[Pages](#github-pages) &nbsp;·&nbsp;
[Git Basics](#-core-git-concepts) &nbsp;·&nbsp;
[Daily Workflow](#-the-daily-three) &nbsp;·&nbsp;
[Pitfalls](#-common-pitfalls) &nbsp;·&nbsp;
[Setup](#-pycharm-setup) &nbsp;·&nbsp;
[Next](#-whats-next)

</div>

<br>
<br>

---

## 🎓 Learning Timeline

| When | Milestone |
| :--- | :--- |
| **Aug 1 &middot; Noon** | Typed my first `git commit`. Felt like clicking a shutter for the first time |
| **Aug 1 &middot; Afternoon** | First `git push` — terminal, tokens, slightly sweaty palms. The full rite of passage |
| **Aug 1 &middot; Evening** | Discovered GitHub Desktop. Wait — buttons? No terminal? The world got brighter |
| **Aug 1 &middot; Late night** | `.gitignore` finally clicked. PyCharm and GitHub Desktop started talking |
| **Aug 2 &middot; Past midnight** | Dragged the repo to `~/Documents`… and it just followed. Git is magic |
| **Aug 2 &middot; Daytime** | Built a bilingual personal website with GitHub Pages → [take a look](https://andyttc05.github.io) |
| **Aug 2 &middot; Afternoon** | Made repo bilingual (two READMEs, two sets of notes) + replaced cold badges with warm words |

<br>

---

## 💻 Installing Git

> 💡 Installing Git is step zero — without it, commit, push, and GitHub Desktop won't work.

### macOS (my environment)

```bash
# Recommended: install via Homebrew
brew install git
```

Verify:

```bash
git --version
# → git version 2.50.1
```

Any version number = it's installed.

### Windows

Download the installer from [git-scm.com](https://git-scm.com) and follow the prompts. After installation, open **Git Bash** and run `git --version` to verify.

### First thing after installing: introduce yourself

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

> ⚠️ Use the **same email** as your GitHub account — otherwise commits won't link to your GitHub profile.

<br>

---

<a id="first-push"></a>

## 🚀 Your First Push — Step by Step

> 💡 I stumbled through this on Day 1 — writing it down for future me (and anyone starting from zero).

### ① Sign up for GitHub

1. Go to [github.com](https://github.com) → click **Sign up**
2. Enter your email, password, and a username (pick something you'll use as your developer identity)
3. Verify your email → done

### ② Create a repo on GitHub (web)

1. Log in, click the **+** in the top-right → **New repository**
2. **Repository name**: pick a name (e.g. `my-first-repo`)
3. Choose **Public** or **Private**
4. ⚠️ **Do NOT check** "Add a README file" (we'll create it locally)
5. Click **Create repository** → copy the URL shown:
   ```
   https://github.com/your-username/your-repo.git
   ```

### ③ Initialize locally & connect to GitHub

```bash
cd your-project-folder
git init                                    # initialize Git repo
git add .                                   # stage everything
git commit -m "first commit"                # your first snapshot
git remote add origin <the-url-you-copied>  # link to GitHub
git push -u origin main                     # upload
```

### ④ About tokens (authentication)

Since 2021, GitHub no longer accepts passwords for push — you need a **Personal Access Token**:

1. GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token → check `repo` scope → generate
3. When pushing, use your GitHub username + **the token** as the password (not your login password)

> 💡 Once you install GitHub Desktop, you never need to deal with tokens again — browser auth handles everything.

### ⑤ Verify — refresh your GitHub repo page

Open `https://github.com/your-username/your-repo` — your code is now in the cloud 🎉

<br>

---

<a id="github-desktop"></a>

## 🖥 GitHub Desktop — Install & Use

> 💡 This is my go-to tool — everything is point-and-click, no terminal needed.

### Installation

Go to [desktop.github.com](https://desktop.github.com) → download → open the dmg → drag to Applications → done.

### First login

Launch GitHub Desktop → **Sign in to GitHub.com** → browser opens → click **Authorize** → you're in. **No token, no password.**

### Daily three-click workflow

1. **Edit files** (PyCharm / Notepad / any editor)
2. Switch back to GitHub Desktop → **Changes** tab shows everything automatically
3. Write a **Summary** → click **Commit to main** → top bar shows **Push origin** → click

> 🎯 No `git add`, no `git push` — all changes are auto-staged, one-click upload.

### Adding an existing repo

**File → Add local repository** → pick your folder → **Add**. The repo appears in the sidebar — click to switch anytime.

### Relationship with the terminal

They don't conflict. If you `git commit` in the terminal, GitHub Desktop sees it. Vice versa.

<br>

---

<a id="github-pages"></a>

## 🌐 GitHub Pages — My First Website

> 💡 This was my first "non-Git" skill — but Git managed the whole process.

### What I built

1. Created the `andyttc05.github.io` repo (GitHub auto-detects it as a Pages site)
2. Wrote a pure HTML + CSS personal homepage (editorial/magazine style)
3. Split into `index.html` (EN) + `zh.html` (中文) with card-style language toggle
4. Added Pull Quote, fade-in animations, alternating backgrounds, responsive layout
5. Fixed a Safari hover color bug on contact links

### What I learned

| Concept | Takeaway |
| :--- | :--- |
| GitHub Pages | Repo named `username.github.io` → auto-deployed, free domain |
| Static sites | HTML + CSS → opens in browser, no server needed |
| Bilingual design | Two files + card toggle → page reload on switch |
| Design iteration | Edit in PyCharm, commit in GitHub Desktop → live in 30s |

---

## 🎯 Core Git Concepts

### What is Git?
Imagine holding a camera. Every time you finish writing some code, you press the shutter — `git commit`. The photo goes into an album, and you can flip back to see "what my code looked like yesterday." Git is that camera.

### The Four Zones

```
Working Directory        ✍️ where I write code
       ↓  git add        📋 "I want this one in the album"
Staging Area             📸 lined up for the photo
       ↓  git commit     📷 click! saved to the album
Local Repository         📚 the photo album on my computer
       ↓  git push       ☁️ uploaded to the cloud
GitHub (Remote)          🌐 a backup that never gets lost
```

### My Account

| Field | Value |
| :--- | :--- |
| GitHub | [andyttc05](https://github.com/andyttc05) |
| Email | andyttc2463@gmail.com |
| Config path | `~/.config/git/config` (XDG, sandbox-safe) |

<br>

---

## ⚡ The Daily Three

```bash
git add .                         # stage all changes
git commit -m "what I did"        # save a snapshot
git push                          # upload to GitHub
```

> 💡 **No terminal needed**: All three can be done with button clicks in **GitHub Desktop**.

<br>

---

## 🔗 PyCharm + GitHub Desktop Workflow

### The auto-sync truth

The first time I noticed this I stared at the screen for a few seconds — **they don't need manual syncing**. They share the same folder, like two people reading the same book:

```
PyCharm opens ~/Documents/my-first-repo     ✍️ writing code here
              ↓ saves files
     my-first-repo folder                   📁 the book is here
              ↓ auto-detected
  GitHub Desktop shows changes ✓            👀 it already knows
```

No cables. No "sync" button. No config. The folder changes, and GitHub Desktop just… knows. That's the whole trick.

**All you need:**
- PyCharm opens this folder
- GitHub Desktop opens the same folder
- That's it. Nothing more.

### Step-by-step

1. Write code in PyCharm (auto-saves on window switch — no Cmd+S required)
2. Switch to GitHub Desktop → **Changes** are already listed on the left
3. Write a Summary ("fixed a bug" / "added login feature") → click **Commit to main**
4. Top bar now says **Push origin** → one more click → done
3. Write **Summary** → click **Commit to main**
4. Top bar shows **Push origin** → click → done

<br>

---

## ⚠️ Common Pitfalls

<details open>
<summary><strong>Pitfall 1: "No local changes" is a feature, not a bug</strong></summary>
<br>

After commit + push, your workspace is **clean**. "No local changes" means *"everything committed, nothing left behind."*

</details>

<details open>
<summary><strong>Pitfall 2: .gitignore won't touch already-added files</strong></summary>
<br>

> `.gitignore` only affects **untracked** files. Already `git add`-ed files are immune.

To detach them:

```bash
git rm --cached -r path/to/file   # remove from staging, keep the file
```

</details>

<details open>
<summary><strong>Pitfall 3: You can't lose a repo by moving it</strong></summary>
<br>

A Git repo = a folder with a hidden `.git` directory. **Self-contained and portable.**

- Drag the whole folder anywhere — code, history, remote connection all follow
- Only thing to do: GitHub Desktop → **File → Add local repository** → pick new location

</details>

<br>

---

## 🐍 PyCharm Setup

| Setting | Value | Path |
| :--- | :--- | :--- |
| Theme | **Light** | Settings → Appearance |
| Font size | **15** | Settings → Editor → Font |
| Auto-save | **On window switch** | Settings → System Settings |

<br>

---

## 📂 Tool Chain

| Tool | Status |
| :--- | :---: |
| **Git** `v2.50.1` | ✅ |
| **GitHub Desktop** | ✅ |
| **PyCharm** `2026.1` (Light / font 15) | ✅ |
| **GitHub Pages** → [andyttc05.github.io](https://andyttc05.github.io) | ✅ |
| **Claude Code** | ⬜ |

### Key Paths

| What | Where |
| :--- | :--- |
| Repo | `~/Documents/my-first-repo` |
| Remote | `https://github.com/andyttc05/my-first-repo` |
| Git config | `~/.config/git/config` |

<br>

---

## 🔄 How to Reset Tools

Move config directories to `/tmp/` = factory reset:

```bash
# PyCharm
mv ~/Library/Application\ Support/JetBrains/PyCharm2026.1 /tmp/removed-pycharm

# GitHub Desktop
mv ~/Library/Application\ Support/GitHub\ Desktop /tmp/removed-github-desktop
```

> 📦 Old config stays in `/tmp/` — recoverable anytime.

<br>

---

## 🔧 Rewriting Git History (Advanced)

> ⚠️ **Use with care** — rewrites commit hashes, breaks other people's clones. Only for "I accidentally committed sensitive info" or "my history is a mess."

### Scenario A: Replace sensitive strings across all history

```bash
cd ~/path/to/your-repo

# Walk through every commit and replace /Users/your-name/... with ~
git filter-branch --force --tree-filter \
  "grep -rl 'string-to-replace' . 2>/dev/null | xargs -I{} sed -i '' 's|old-string|new-string|g' {}" \
  --prune-empty -- --all
```

Push the cleaned version:

```bash
git push --force-with-lease origin main
# --force-with-lease is safer than --force: it refuses if someone else pushed new commits
```

### Scenario B: Nuke all history, keep current files

```bash
cd ~/path/to/your-repo

# 1. Create a branch with zero history
git checkout --orphan clean-slate

# 2. Commit all current files in one shot
git add -A
git commit -m "clean slate"

# 3. Overwrite GitHub's main
git push --force origin clean-slate:main

# 4. Clean up locally
git checkout main && git reset --hard origin/main && git branch -D clean-slate
```

### Scenario C: Full workflow (from dirty history to clean repo)

```bash
cd ~/path/to/your-repo

# === Replace sensitive strings in history ===
git filter-branch --force --tree-filter \
  "grep -rl '/Users/your-name/' . 2>/dev/null | xargs -I{} sed -i '' 's|/Users/your-name/|~/|g' {}" \
  --prune-empty -- --all

# === Push the clean version ===
git push --force-with-lease origin main

# === Or: nuke everything, keep only current files ===
git checkout --orphan clean-slate
git add -A
git commit -m "clean slate"
git push --force origin clean-slate:main

# === Local cleanup ===
git checkout main
git reset --hard origin/main
git branch -D clean-slate
```

### Lessons learned

| Lesson | Detail |
| :--- | :--- |
| Review before commit | Run `git diff` before `git add` — keep secrets out of history |
| Terminal required | GitHub Desktop doesn't support force push — history rewrites need the terminal |
| Don't blindly force | `--force-with-lease` is safer than `--force` — refuses if someone else pushed recently |
| Terminal push needs a token | GitHub Desktop uses OAuth (no password). Terminal needs a PAT. See [🚀 Your First Push](#first-push) → ④ About tokens |
| Clean up after | Run `branch -D` to delete temporary branches |
| Reset after force push | After `--force`, local main and remote main have completely different histories — `git pull` will fail. Run `git fetch origin && git reset --hard origin/main` to sync |

<br>

---

## 🎯 What's Next

<table>
  <tr>
    <td width="33%">
      <strong>✅ Done</strong><br>
      <sub>GitHub Pages site<br>Bilingual zh/en docs<br>Editorial design polish</sub>
    </td>
    <td width="33%">
      <strong>⬜ Up Next</strong><br>
      <sub>Claude Code CLI<br>Git branching<br>First Python project</sub>
    </td>
    <td width="33%">
      <strong>🔮 Someday</strong><br>
      <sub>VS Code workflow<br>JavaScript basics<br>Open source contribution</sub>
    </td>
  </tr>
</table>

<br>

---

<br>

<div align="center">

> 🍑 *"Learning is like taking snapshots — every commit preserves a moment you can always revisit."*

<sub>— Momo &nbsp;·&nbsp; August 2026</sub>

</div>
