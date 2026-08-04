[English](git-github-guide.md) &nbsp;|&nbsp; **中文**

<br>

<div align="center">

# Git + GitHub 核心概念大串讲

</div>

<br>

> **核心理念**：AI 时代的 Git 学习不是死记命令，而是**理解核心概念**。掌握了概念，你就可以用自然语言指挥 AI 完成所有 Git 操作。**得意忘言**——得其意，忘其言。

---

## 目录

- [引言](#引言)
- [一、认识 Git 与 GitHub](#一认识-git-与-github)
- [二、环境准备](#二环境准备)
- [三、Commit：保存快照](#三commit保存快照)
- [四、Branch：分支管理](#四branch分支管理)
- [五、WorkTree：并行开发](#五worktree并行开发)
- [六、Git 四分区](#六git-四分区)
- [七、远端仓库](#七远端仓库)
- [八、GitHub 入门](#八github-入门)
- [九、GitHub 协作](#九github-协作)
- [常见错误](#常见错误)
- [必会清单](#必会清单)
- [核心心法](#核心心法)

---

## 引言

很多人觉得：AI 都能帮我写代码了，Git 还有必要学吗？

**恰恰相反。**

事实是，各类 AI 编程工具在初始化项目、创建分支、提交代码、处理冲突的时候，底层操作的全是 Git。

> **Git 是 AI 时代的基本功，不是可选项。**

好消息是：我们不需要死记硬背命令，只需掌握核心概念，就可以用自然语言指挥 AI 完成所有 Git 操作。

```
传统方式：手动敲命令行，查文档，搜 Stack Overflow
AI 方式：理解概念 → 用自然语言指挥 AI → AI 执行命令
```

---

## 一、认识 Git 与 GitHub

### 1.1 从写论文说起

写过论文的同学一定有这种经历：

```
Thesis_v1.docx
Thesis_v2.docx
Thesis_v3.docx
Thesis_final.docx
Thesis_final_final.docx
```

小心翼翼地保存每个版本，这就是**最原始的版本控制**。

### 1.2 Git

| 概念 | 说明 |
|------|------|
| **Git** | 免费开源的**版本控制**软件 |
| **Git 仓库 (Repository)** | 被 Git 管理的文件夹 |
| **提交 (Commit)** | 版本控制基本单元，每次 commit 保存仓库的**完整快照** |
| **分支 (Branch)** | 独立的开发线，分支间代码隔离，互不干扰 |

### 1.3 本地仓库 vs 远程仓库

| 概念 | 说明 |
|------|------|
| **本地仓库** | 运行在自己电脑上的 Git 仓库 |
| **远程仓库** | 托管在服务器上的 Git 仓库，用于备份、分享和协作 |
| **GitHub** | 免费提供远程仓库的网站，全球最大的代码托管与协作平台 |

### 1.4 GitHub = Git + Hub

- **Git**：版本控制工具
- **Hub**：中心、聚集地
- **合起来**：托管 Git 仓库的网站

**GitHub 能做什么：** 存储代码、备份、分享、多人协作、托管开源项目、提交 Issue 和 Pull Request。

| 仓库类型 | 含义 |
|------|------|
| **公开仓库 (Public)** | 所有人都能看到 |
| **私有仓库 (Private)** | 只有所有者和受邀协作者能看到 |

> 补充：还有 GitLab、Bitbucket 等服务。学会 GitHub，另外两个也能轻松上手。

---

## 二、环境准备

### 2.1 注册 GitHub 账号
访问 [GitHub](https://github.com/)，点 **Sign up**。

### 2.2 安装 Git
**Windows：** [Git 官网](https://git-scm.com/) 下载安装包 → 一路下一步。

**Mac：**
```bash
xcode-select --install
```

**验证：**
```bash
git --version
```


### 2.3 GitHub Desktop
GitHub 官方出品的**图形化 Git 客户端**，把命令行操作变成点按钮。后面的 Commit、分支、推送等操作都可以在 Desktop 里完成。

1. 去 [desktop.github.com](https://desktop.github.com) 下载安装
2. 打开 → **Sign in to GitHub.com** → 浏览器弹窗 → 点 **Authorize**
3. 自动跳回 Desktop，登录完成

> 💡 OAuth 自动认证，不需要配置 token。登录一次，以后 push/pull 都不用输密码。

### 2.4 安装 VSCode
前往 [VSCode 官网](https://code.visualstudio.com/) 下载安装。这是我们的**代码编辑器**——写代码、改文件都在这里。

### 2.5 AI Agent 绑定 Git 与 GitHub
这是 AI 时代的**关键操作**——用 AI 帮你完成初始化和推送。

1. 创建空白文件夹
2. 在 AI Agent 中选择该文件夹作为项目目录
3. 输入："把这个文件夹初始化成 Git 项目，推送到 GitHub"
4. AI 会让你提供远程仓库地址
5. 在 GitHub 创建新仓库，获取地址
6. 粘贴给 AI，完成授权

> 绑定完成后，后续操作都用自然语言指挥 AI。

### 2.6 `git init` — 初始化仓库
```bash
git init
```

执行后生成 `.git` 子目录，存放所有版本控制信息。

```
Before init:               After init:
my-project/                my-project/
                             .git/        <-- stores version control info
                             (other project files)
```

> ⚠️ 删除 `.git/` 目录，仓库就没了，版本历史也丢失。

### 2.7 `.gitignore`
声明哪些文件不应被 Git 跟踪、不应上传到 GitHub。

| 文件/目录 | 原因 |
|-----------|------|
| `.env` | 可能含 API 密钥、密码 |
| `node_modules/` | 可通过 `npm install` 重装 |
| `.DS_Store` | macOS 系统文件 |
| `*.log` | 日志文件 |

**示例：**
```gitignore
.env
node_modules/

# VS Code
.vscode/

# macOS system files
.DS_Store

# Python cache
__pycache__/
*.pyc

*.log
dist/
.cache/
```

> ⚠️ 项目初始化时就创建 `.gitignore`！

**AI 提示词：**
> "将当前目录初始化为 Git 项目。同时创建合适的 .gitignore，排除 .env、node_modules、日志文件和缓存文件。"

### 2.8 日常必会命令
这三个命令是使用频率最高的，每次 commit 前后都会用到：

| 命令 | 作用 | 示例 |
|------|------|------|
| `git status` | 查看当前状态：哪些文件改了、哪些已暂存 | 每次操作前先看一眼 |
| `git diff` | 查看具体改了什么内容（未暂存的改动） | `git diff` / `git diff --staged` |
| `git log --oneline` | 查看提交历史，找到 Commit ID | `git log --oneline -5`（最近 5 条） |

```bash
git status              # "我现在在哪？改了啥？"
git diff                # "具体改了什么内容？"
git diff --staged       # "暂存区里有什么？"
git log --oneline       # "历史记录，找 Commit ID"
```

> 💡 养成习惯：每次操作前 `git status`，提交前 `git diff` 确认改动，回退时 `git log` 找 Commit ID。

### 2.9 SSH 密钥认证（可选）
GitHub 支持两种认证方式：HTTPS（需要 token）和 SSH（配置一次，永久免密）。

```bash
# 1. 生成 SSH 密钥
ssh-keygen -t ed25519 -C "your-email@example.com"
# 一路回车即可

# 2. 复制公钥
cat ~/.ssh/id_ed25519.pub

# 3. 粘贴到 GitHub → Settings → SSH and GPG keys → New SSH key
# 4. 测试连接
ssh -T git@github.com
# 看到 "Hi username!" 就成功了
```

> 💡 配置 SSH 后，clone 时用 `git@github.com:username/repo.git` 格式，push/pull 不再需要输密码。

## 三、Commit：保存快照

### 3.1 什么是 Commit

**Commit** 是 Git 版本控制的**基本单元**。每次 commit 就像给仓库拍一张快照，保存当前所有文件状态。

**Commit 的作用：** 保存项目状态、记录谁改了什么、形成可回溯历史链、支持回退对比、支撑多人协作。

### 3.2 Commit Message

每次提交必须写 Commit Message：

```
Add login page
Fix user profile bug
Update README documentation
```

**规范：** 简明扼要说明"做了什么"。推荐 [Conventional Commits](https://www.conventionalcommits.org/) 格式：`feat:` 新功能、`fix:` 修 bug、`docs:` 文档、`chore:` 杂项。统一格式让提交历史一目了然。

### 3.3 Commit ID / Commit Hash

每次提交生成唯一哈希值：

| 类型 | 特征 |
|------|------|
| **长 ID** | 完整 40 位哈希值 |
| **短 ID** | 前 7 位，日常用 |

> 与 AI 沟通时，始终提供 Commit ID 精确定位。

### 3.4 最佳实践：频繁提交

```
1. AI 完成登录页面 → 测试通过 → Commit
2. AI 完成注册页面 → 测试通过 → Commit
3. AI 完成个人中心 → 测试通过 → Commit
```

**好处：** 出错可快速回退，历史清晰，不容易搞乱项目。

### 3.5 三种"后悔药"：版本回退

#### Discard — 放弃未提交的更改

| 项目 | 说明 |
|------|------|
| **使用场景** | 文件已修改但**尚未 commit** |
| **效果** | 放弃更改，恢复到上次 commit 状态 |
| **风险** | 放弃的更改**永久丢失** |

#### `reset` — 强制回退

```bash
git reset --hard <commit-id>
```

| 项目 | 说明 |
|------|------|
| **使用场景** | 回到某个历史 commit，丢弃之后所有提交 |
| **风险** | 已推到远端需要 `git push -f` |
| **适用范围** | **仅本地、单人分支** |

#### `revert` — 反向提交撤销

```bash
git revert <commit-id>
```

| 项目 | 说明 |
|------|------|
| **使用场景** | 撤销特定错误 commit，保留其他历史 |
| **效果** | 创建"反向 commit"，不破坏历史 |
| **适用范围** | **多人协作推荐使用** |

#### 对比

| 操作 | 功能 | 适用场景 | 风险 |
|------|------|----------|------|
| **Discard** | 放弃未提交的更改 | 还没 commit 时反悔 | 更改丢失 |
| **Reset** | 回到历史 commit | 本地、单人分支 | 可能删除历史 |
| **Revert** | 反向抵消某个 commit | 多人协作分支 | **最安全** |

> 💡 多人协作场景下，**revert 比 reset 更安全**。

**AI 提示词：**
> "检查当前改动，总结修改内容，生成合适的 commit message。确认无敏感文件后完成 commit。"
>
> "将仓库回退到 commit abc1234。执行前告诉我哪些 commit 会被删除。"
>
> "撤销 commit abc1234 的改动，但保留其他提交。优先使用 revert。"

#### 终极安全网：`git reflog`

如果不小心 `reset --hard` 删错了，不要慌——Git 几乎不会真正删除数据。

```bash
git reflog
# 显示 HEAD 的所有移动记录，包括已删除的 commit
# 找到想恢复的 commit ID，然后：
git reset --hard <那个commit-id>
```

`reflog` 记录了 HEAD 的每一次位置变化，默认保留 90 天。它是 Git 的"后悔药中的后悔药"。

---

## 四、Branch：分支管理

### 4.1 什么是分支

**分支（Branch）** 代表独立开发线。默认主干叫 `main` 或 `master`。

```
X Wrong: develop on main directly
   -> may break stable code

O Right:
   main --------------------> (stable)
     \___ feature/login ---> (new feature dev)
                 | testing passes
   main <-- merge --- feature/login
```

### 4.2 分支特点

- 新建分支代码与源分支**完全一致**
- 分支上的修改**不影响 main**
- 开发完成后通过**合并（Merge）** 回到 main

### 4.3 命名规范

```
feature/login-page        # new feature
feature/payment           # new feature
fix/header-bug            # bug fix
hotfix/security-patch     # emergency fix
```

### 4.4 核心流程

```
1. 从 main 创建新分支
2. 在新分支上开发和提交
3. 合并回 main
4. 删除已合并的分支（可选）
```

> ⚠️ Git 不允许删除当前所在分支——先切到其他分支再删。

### 4.5 HEAD 指针

**HEAD** 指向仓库当前所在的 commit：

| 状态 | HEAD 指向 |
|------|-----------|
| 在 `main` 分支上 | `main` 的最新 commit |
| 在 `feature` 分支上 | `feature` 的最新 commit |
| 检出一个历史 commit | 那个 commit → **分离头指针** |

**分离头指针（Detached HEAD）**：HEAD 指向历史 commit 而非分支末尾。可查看历史版本，但**不推荐在此状态下修改**。要改代码就创建新分支。

### 4.6 合并冲突（Merge Conflict）

两个分支修改了**同一文件的同一行**时，Git 不知道保留哪个版本 → 冲突。

你需要选择：保留 A 的版本、保留 B 的版本、两者都保留、手动创建新结果。

**AI 提示词：**
> "合并这两个分支。如果出现冲突，停下来告诉我冲突的文件和内容，不要自动决策。"
>
> "解决当前合并冲突。同一行两个版本时，两者都保留。"

### 4.7 Cherry-pick — 选择性合并

只选择某个分支的特定 commit，应用到当前分支。

Feature 分支有 3 个 commit：
1. 创建蔬菜列表
2. 创建肉类列表
3. 创建主食列表

只想把 1 和 3 合并到 main，跳过 2。用 cherry-pick。

**AI 提示词：**
> "Cherry-pick 这两个 commit 到 main：`abc1234` `def5678`。不要合并该分支的其他 commit。"

### 4.8 Rebase — 变基

把当前分支的 commit "搬家"到目标分支最新位置之后。

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

**优点：** 历史清晰，无多余 merge commit。

**风险：** 改写提交历史。已推送的分支 rebase 后需要 `git push -f`。

> ⚠️ **rebase + 强制推送仅适用于只有你一个人使用的分支**。不要在多人协作分支上随意 rebase。

| 操作 | 特点 | 适用场景 |
|------|------|----------|
| **Merge** | 保留分支合并历史 | 团队协作、公共分支 |
| **Rebase** | 历史干净，但改写历史 | 个人 feature 分支 |

**AI 提示词：**
> "从 main 创建新分支 feature/login-page，在该分支上开发登录页面。"
>
> "将 feature/login-page 合并到 main。如有冲突，停下来告诉我。"
>
> "把当前 feature 分支 rebase 到最新 main 上。执行前说明是否需要强制推送及风险。"

---

## 五、WorkTree：并行开发

### 5.1 什么是 WorkTree

**Git Worktree** 为同一仓库的不同分支创建**独立的工作目录文件夹**。

### 5.2 使用场景

- 多个 AI Agent 并行开发不同功能
- 修 bug 同时开发新功能，互不干扰
- 避免频繁切换分支
- 隔离不同实验

### 5.3 结构

```
Repo .git/
  +-- main/          (worktree 1 -- main)
  +-- feature-a/     (worktree 2 -- Feature A)
  +-- feature-b/     (worktree 3 -- Feature B)
```

- 每个 worktree 对应一个分支，是独立文件夹
- 不同文件夹修改互不干扰
- 完成后合并回 main

**AI 提示词：**
> "创建新的 worktree 和分支，用于开发登录功能。完成后 commit 并合并回 main。"

---

## 六、Git 四分区

这是 Git **最重要的理论基础**。理解了它，所有命令就都通了。

### 6.1 四分区模型

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

### 6.2 分区说明

| 分区 | 说明 | 对应操作 |
|------|------|----------|
| **工作区 (Working Directory)** | 项目文件夹，直接编辑代码 | 编辑文件 |
| **暂存区 (Staging Area)** | 提交前的"购物车"，选择要提交的文件 | `git add` |
| **本地仓库 (Local Repo)** | commit 后的代码存储位置 | `git commit` |
| **远程仓库 (Remote Repo)** | GitHub 上的仓库 | `git push` / `git pull` |

### 6.3 数据流向

```
Working Dir -> git add -> Staging Area -> git commit -> Local Repo -> git push -> Remote Repo
Remote Repo -> git pull (fetch + merge) -> Local Repo + Working Dir
Remote Repo -> git clone -> Local Repo + Working Dir (fresh copy)
```

> 💡 VSCode 中默认合并 add 和 commit 操作。

### 6.4 Stash — 临时存储

> ⚠️ `stash` 和 `staging area (暂存区)` 是**完全不同的概念**！

**使用场景：** 你在 feature 分支上写到一半，突然要切到 main 处理紧急 bug。

**两种选择：**
1. 做一个临时 commit
2. 用 `stash` 临时保存 ← **推荐**

**效果：** 临时保存未完成的修改，清空工作目录，方便切换分支。回来 `pop` 恢复继续写。

```bash
git stash      # save
git stash pop  # restore
```

**AI 提示词：**
> "我有些未提交的代码，请 stash 它们，然后切换到 main 分支。"
>
> "切换回 feature 分支，把 stash 的改动 pop 回来。"

---

## 七、远端仓库

### 7.1 `git clone` — 复制远程仓库到本地

```bash
git clone <repo-url>
```

从 GitHub 下载项目到本地，自动创建本地仓库和工作目录。

### 7.2 `git push` — 上传本地提交

```bash
git push
```

将本地 commit 上传到 GitHub。

> ⚠️ 只有仓库管理员或被授权协作者才能 push。不能直接 push 到别人仓库。

### 7.3 `git pull` — 拉取远程更新

```bash
git pull
```

获取远程最新代码并合并到本地。

**`git pull` 等价于：**
```bash
git fetch    # 先获取远程更新
git merge    # 再合并到本地
```

### 7.4 `origin/main` 是什么

- **`origin`** = 远程仓库别名（默认名称）
- **`origin/main`** = 远程仓库上的 `main` 分支
- **`main`** = 本地仓库的 `main` 分支

| 状态 | 含义 |
|------|------|
| 本地 `main` 领先 `origin/main` | 有本地 commit 未推送 → `git push` |
| `origin/main` 领先本地 `main` | 有人更新了远程 → `git pull` |

**AI 提示词：**
> "把上游 main 的最新改动合并到当前 feature 分支。如有冲突，让我选择怎么处理。"

### 7.5 `git remote` — 管理远程连接

```bash
git remote -v            # 查看当前关联的远程仓库
git remote add <name> <url>  # 添加新的远程仓库
```

比如 Fork 了别人的项目后，添加上游仓库：
```bash
git remote add upstream https://github.com/original-owner/repo.git
git fetch upstream        # 拉取上游更新
git merge upstream/main   # 合并到本地
```

### 7.6 `git tag` — 版本标签

给重要的 commit 打标签，通常用于标记发布版本：

```bash
git tag v1.0.0                    # 轻量标签
git tag -a v1.0.0 -m "首次发布"    # 附注标签（推荐）
git push origin v1.0.0            # 推送单个标签
git push origin --tags            # 推送所有标签
```

---

## 八、GitHub 入门

### 8.1 仓库页面 URL

```
https://github.com/username/repo-name
```

例如：`github.com/docmirror/dev-sidecar` → 中间是作者名，末尾是仓库名。

### 8.2 核心功能区

**Code 区域：** 浏览源码、下载 ZIP、复制 clone URL。

**README：** 项目说明文件，自动显示在仓库首页。

**Releases：** 版本号、更新说明、打包好的安装文件。

### 8.3 About / Star / Fork

| 功能 | 含义 |
|------|------|
| **About** | 项目简介、标签、许可证 |
| **Star** | 点赞 + 收藏 |
| **Fork** | 将别人项目复制到自己账号下 |

### 8.4 Issues（问题讨论区）

用于报告 Bug、提议新功能、搜索问题、参与讨论。

| 状态 | 含义 |
|------|------|
| **Open** | 未解决 / 讨论中 |
| **Closed** | 已解决 |

### 8.5 GitHub 快捷键

| 快捷键 | 功能 |
|--------|------|
| `/` | 打开搜索 |
| `T` | 仓库内快速搜索文件 |
| `L` | 跳转到指定行号 |
| `.` | 打开网页版 VSCode |
| `?` | 查看所有快捷键 |
| `G` + `C` | 跳到 Code 页面 |
| `G` + `I` | 跳到 Issues 页面 |

### 8.6 Git Blame

逐行显示代码的提交信息：谁提交的、哪次 commit、什么时间。

> 用于排查："这行代码是谁改的？为什么这么写？"

### 8.7 Codespaces

GitHub 提供的**远程开发环境**。浏览器中直接打开 VS Code 风格编辑器，运行、调试、提交代码。

### 8.8 GitHub Pages（免费建站）

把仓库变成网站，免费域名 `https://用户名.github.io`：

1. 创建名为 `用户名.github.io` 的公开仓库
2. 上传 HTML/CSS 文件（入口文件叫 `index.html`）
3. Settings → Pages → 选分支 → Save
4. 等几十秒，访问 `https://用户名.github.io` 就上线了

> 💡 适合放个人主页、项目文档、作品集。静态网站零成本。

### 8.9 Profile README（个人主页）

创建一个**和自己用户名同名的仓库**，里面的 `README.md` 会自动显示在你的 GitHub 个人主页顶部。放自我介绍、技能标签、项目链接——你的 GitHub 名片。

---

## 九、GitHub 协作

### 9.1 开源贡献：Fork + Pull Request

**适用场景：** 你没有权限直接修改别人的仓库，但想贡献代码。

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

### 9.2 Pull Request（PR）是什么

**PR = Merge Request（合并请求）**

"我在这个分支上做了修改，请求你合并到目标分支。"

**PR 中可看到：** 改了哪些文件、增减了什么代码、提交历史、讨论记录、Code Review 意见。

### 9.3 提交 PR 前先同步上游

```
1. 在自己的 feature 分支上开发
2. 提交 PR 前，先把上游 main 的最新代码合并到你的 feature 分支
3. 本地解决冲突
4. Push
5. 再创建 PR
```

> **原因：** 分支落后上游太多，直接 PR 可能冲突，降低被接受概率。

### 9.4 团队协作：Collaborator 模式

被添加为 Collaborator 后，不需要 Fork：

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

> ⚠️ 即使有 push 权限，也不建议直接改 `main`。始终使用 **分支 + PR** 工作流。

**AI 提示词：**
> "这是上游仓库地址：<repo-url>。把上游 main 最新改动合并到当前 feature 分支。如有冲突，让我选择怎么处理。"

### 9.5 Protected Branches（分支保护）

在团队项目中，可以在 GitHub 上给 `main` 分支设置保护规则：

**设置路径：** Repo → Settings → Branches → Add branch protection rule

**常用规则：**
- 禁止直接 push 到 `main`（强制走 PR）
- PR 必须有人 Review 并批准后才能合并
- PR 必须通过 CI 测试才能合并

> 💡 这是从"约定"变成"强制"——工具替你守住规则，防止手滑。


## 常见错误

| # | 错误 | 正确做法 |
|---|------|----------|
| 1 | **Git 和 GitHub 是同一个东西** | Git = 版本控制工具；GitHub = 托管 Git 仓库的网站 |
| 2 | **以为 commit 就上传到 GitHub** | `git commit` 只在本地；`git push` 才上传远程 |
| 3 | **直接 push 到别人仓库** | 没权限时走 Fork → PR |
| 4 | **直接在 main 上开发** | 用 feature 分支，通过 PR 合并 |
| 5 | **混淆 reset 和 revert** | reset 改写历史（本地）；revert 创建反向提交（公共分支） |
| 6 | **在 detached HEAD 状态下写代码** | 只用于查看历史；改代码就创建新分支 |
| 7 | **随意 rebase + force push** | 仅个人分支，公共分支禁止 |
| 8 | **提交 .env 文件** | 始终加入 .gitignore |
| 9 | **提交 node_modules** | 加入 .gitignore |
| 10 | **提交 PR 前不同步上游** | 先同步 → 解决冲突 → 再提交 PR |

---

## 必会清单

| # | 概念 | 一句话 |
|---|------|--------|
| 01 | **Git** | 版本控制工具 |
| 02 | **GitHub** | 远程仓库托管平台 |
| 03 | **Repository** | 被 Git 管理的文件夹 |
| 04 | **Commit** | 保存一次项目快照 |
| 05 | **Commit ID** | 每次提交的唯一编号 |
| 06 | **Branch** | 分支，隔离开发 |
| 07 | **Merge** | 合并分支 |
| 08 | **Pull / Push** | 拉取 / 推送远程代码 |
| 09 | **Pull Request** | 请求合并代码到目标分支 |
| 10 | **Revert 优于 Reset** | 多人协作下 revert 更安全 |

---

## 核心心法

```
得意忘言 —— 得其意，忘其言

掌握核心概念，具体命令不需要死记。
理解了提交、分支、合并、冲突、四分区模型，
AI 就是你最好的 Git 操作员。
```

---

> 📝 本文档涵盖 Git 与 GitHub 核心概念、实战流程与进阶操作。
