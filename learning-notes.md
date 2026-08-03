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
| **Git** v2.50.1 | ✅ |
| **GitHub Desktop** | ✅ |
| **PyCharm** 2026.1 (Light, font 15) | ✅ |
| **GitHub Pages** → [andyttc05.github.io](https://andyttc05.github.io) | ✅ |
| **Claude Desktop** | |

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

## Learning Timeline

| When | Milestone |
| :--- | :--- |
| Aug 1, noon | Typed my first `git commit`. Felt like clicking a shutter |
| Aug 1, afternoon | First `git push`. Terminal, tokens, sweaty palms. The full thing |
| Aug 1, evening | Found GitHub Desktop. Wait, buttons? No terminal? |
| Aug 1, late night | `.gitignore` finally made sense. PyCharm and GitHub Desktop started talking to each other |
| Aug 2, past midnight | Moved the repo to `~/Documents`… and it just followed. Git is wild |
| Aug 2, afternoon | Built a bilingual site with GitHub Pages → [have a look](https://andyttc05.github.io) |
| Aug 2, afternoon | Made the repo bilingual: two READMEs, two sets of notes |
| Aug 3, afternoon | Gave all four docs a makeover, tidied up the structure |
| Aug 3, afternoon | Learned Discard Changes and Reset to Commit — no more re-cloning when things go sideways |

---

## What's Next

GitHub Pages site is up, both languages are in place, all the docs got a refresh. Next I want to figure out Git branching, and maybe start an actual Python project. After that? No plan. I'll follow whatever I get curious about. VS Code and JavaScript are somewhere on the horizon. Contributing to something open source sounds fun too. We'll see.

---

<br>

<div align="center">

> "Every expert started by typing `git init` for the first time. These notes are what that looks like."

</div>
