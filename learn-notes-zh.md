[English](learning-notes.md) &nbsp;|&nbsp; **中文**

<br>

<div align="center">

# 我的 Git 学习笔记

### *从零到 Git/GitHub。一个问题，一个答案。*

</div>

<br>

<p align="center">
  <a href="https://andyttc05.github.io"><img src="https://img.shields.io/badge/在线网站-andyttc05.github.io-brightgreen?style=flat-square" alt="GitHub Pages"></a>
  <a href="https://github.com/andyttc05/my-first-repo/blob/main/learning-notes.md"><img src="https://img.shields.io/badge/笔记-English-%233498db?style=flat-square" alt="English"></a>
  <img src="https://img.shields.io/badge/师傅-Momo-ff69b4?style=flat-square" alt="帮手">
  <img src="https://img.shields.io/badge/始于-2026.08-orange?style=flat-square" alt="始于">
</p>

<br>

> "学东西最好的方法，就是在每一个"原来如此"消失之前把它记下来。"

---

## 核心概念

### Git 是什么

你拍照，回头能翻出来看。Git 就是给你的代码拍照。敲 `git commit`，它就拍一张快照。明天你能翻回去，看到"昨天这时候代码长什么样"。就这样，没了。

### 四个区域

```
Working Directory        ✍️ where I write code
       ↓  git add        📋 "I want this one in the album"
Staging Area             📸 lined up for the photo
       ↓  git commit     📷 click! saved to the album
Local Repository         📚 the photo album on my computer
       ↓  git push       ☁️ uploaded to the cloud
GitHub (Remote)          🌐 a backup that never gets lost
```

### 我的账号

| 项目 | 内容 |
| :--- | :--- |
| GitHub | [andyttc05](https://github.com/andyttc05) |
| 邮箱 | andyttc2463@gmail.com |
| 配置路径 | `~/.config/git/config` |

---

## 安装 Git

别急，先装 Git。没它后面全白搭。

### macOS（我的环境）

```bash
brew install git
```

看看装好没：

```bash
git --version
# → git version 2.50.1
```

有版本号就是装好了。

### Windows

去 [git-scm.com](https://git-scm.com)，下载安装包，一路点下一步。装完打开 Git Bash，敲 `git --version`。

### 第一件事：让 Git 知道你是谁

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

⚠️ 邮箱得和 GitHub 注册的一致。不然你的 commit 会像个幽灵，挂不上头像。

---

<a id="first-push-cn"></a>

## 第一次 Push 全流程

第一天在这个环节踩了不少坑。写下来给一礼拜后的自己，肯定会忘。

### ① 注册 GitHub 账号

打开 [github.com](https://github.com)，点 **Sign up**。起个你喜欢的用户名，以后它就挂在你的每行代码下面了。

### ② 在 GitHub 上建仓库

点右上角 **+** → **New repository**。起个名字，选公开还是私有。不要勾 "Add a README file"，我们马上自己写。

点 **Create repository**，记下那个网址。长这样：`https://github.com/你的用户名/仓库名.git`。

### ③ 让本地文件夹连上 GitHub

```bash
cd your-project-folder
git init
git add .
git commit -m "first commit"
git remote add origin <the-url-you-copied>
git push -u origin main
```

### ④ Token

2021 年起 GitHub 不让用密码 push 了，得搞个 Personal Access Token。

GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)。生成一个新的，勾 `repo`。push 的时候，用户名填你的 GitHub 用户名，密码贴那串 token。

好消息是：装了 GitHub Desktop 就不用管这些了。浏览器授权一次完事儿。

### ⑤ 验证

刷新 `https://github.com/你的用户名/仓库名`。代码飘在云端了。🎉

---

## 日常三连

```bash
git add .
git commit -m "what I did"
git push
```

不想碰终端也行。上面三行，在 GitHub Desktop 里各点一下就好。

---

<a id="branches-cn"></a>

## Git 分支

分支就是一个平行时间线。你从 `main` 分叉出去，随便折腾。搞定了——合回来。`main` 全程干干净净。

### 概念

```
main    o---o---o-------o---o   never broken
            |               |
feature     o---o---o-------+   playground → merged
```

feature 分支是 `main` 在那个时间点的拷贝。你在上面不管怎么炸，`main` 都不知道。直到你 merge 的那一刻。

### GitHub Desktop 操作（全程鼠标）

**创建分支**：

`Current Branch` → 输入名字 → `New Branch`（选基于 `main`）

顶部栏显示新分支名字，你就已经在分支上了。

**在分支上干活**：

编辑器里正常改代码。commit 照常。提交记录只写在这条分支上，不影响 `main`。

**Push + 发 Pull Request**：

点 `Publish branch` → `Create Pull Request` → 浏览器打开 GitHub。检查 diff，写个说明，点 `Create pull request`。

**合并**：

PR 页面点 `Merge pull request` → `Confirm merge`。分支上的改动就进 `main` 了。

**切回 main**：

`Current Branch` → 选 `main`。点 `Fetch origin` 把合并后的内容拉下来。

### 完整流程速览

```
branch → changes → commit → push → PR → merge
   ↑                                       │
   └─────────── back to main ──────────────┘
```

### 本地合并（不用 PR）

不需要发 Pull Request，直接合进 `main` 也行：

1. 切到 `main`：`Current Branch` → 选 `main`
2. 菜单栏：**Branch** → **Merge into Current Branch…**
3. 从列表里选你要合的分支 → 点 **Merge**

搞定。分支上的 commit 都到 `main` 了。Push 一下 `main` 同步到 GitHub。

### 删除分支（合并完之后）

合并完了，分支就成了空壳。清理掉：

1. `Current Branch` → 右键分支名字
2. 点 **Delete…**
3. 确认

或者菜单栏：**Branch** → **Delete…** → 选分支。

> 💡 如果分支还没合并，GitHub Desktop 会弹出警告。这是安全网——删之前再确认一下。

### 丢弃分支（不改了，放弃合并）

开了一条分支，写着写着发现方向不对，不想合了？

1. 先切回 `main`：`Current Branch` → 选 `main`
2. `Current Branch` → 右键那条废掉的分支 → **Delete…**
3. 确认

分支上的所有 commit 就没了。`main` 从头到尾没被碰过——就像那条分支从来没存在过。

> ⚠️ 如果已经把分支 push 到 GitHub 了，本地删除只删本地。去 GitHub 网页 → 分支页面 → 也把它删掉。

| 场景 | 操作 |
| :--- | :--- |
| 分支搞定，PR 合并了 | 删掉——本地和远程都删 |
| 分支搞定，本地合并了 | 删掉 |
| 分支废了，不想合并 | 删掉——`main` 本来就没被碰过 |
| 分支 push 了但没合 | 删本地 + 删远程 |

### Stash：没写完的改动先收起来

```text
  改动到一半
       ↓ git stash
  [隐藏抽屉]             ← 改动收好，工作区变干净
       ↓ 切分支 / pull / 干别的事
       ↓ git stash pop
  改动到一半             ← 改动拿回来，继续写
```

`git stash` 就像把改了一半的东西塞进抽屉。工作区瞬间干净——想切分支、pull 新代码、干什么都行。`git stash pop` 再拿回来。

它特别适合这种场景：正在分支上改代码，突然需要切到别的地方看一眼，但当前改动还没到能 commit 的程度。GitHub Desktop 左下角有 "Stashed Changes" 面板——Restore 拿出来，Discard 扔掉。

---

<a id="github-desktop-cn"></a>

## GitHub Desktop

这是我最喜欢的工具。全程点按钮，不碰终端。

### 安装

去 [desktop.github.com](https://desktop.github.com)，下载 dmg，双击，拖进 Applications。完了。

### 首次登录

打开 GitHub Desktop → **Sign in to GitHub.com** → 浏览器弹窗 → 点 **Authorize** → 自动回到桌面。不用 token，不用密码。

### 日常三步

打开编辑器写代码。切回 GitHub Desktop，左边 Changes 已经列出来了。写一行 summary，点 **Commit to main**。顶部变成 **Push origin**，点一下。发出去了。

不用 `git add`，不用 `git push`。所有改动自动暂存，一键上传。

### 添加已有仓库

**File → Add local repository** → 选文件夹。出现在左边列表里，以后点一下就能切。

### Desktop 和终端处得来

终端 `git commit` 了，Desktop 能看到。Desktop 里 commit 了，终端也能看到。它们看的是同一个 `.git` 目录。不打架。

### 还原成云端版本

改了一通，越改越乱，最后想推倒重来——回到 GitHub 上的那个版本。这种"撤销"在 GitHub Desktop 里**分两种情况**，做法不一样。

#### 情况一：还没 commit，只是改了文件

最常见。文件改了，Changes 标签页里一堆，但还没点 Commit。

**操作**：在 Changes 标签页**右键点击那个文件** → 选 **Discard Changes…** → 确认。这个文件就回到上次 commit 的样子了。

想一次清掉所有文件？右键任意文件 → **Discard All Changes…**。

> ⚠️ Discard 不可逆。点了就没了，确认前想清楚。

每个文件右边还有个小图标（鼠标悬停显示"Revert file changes"），点那个也能直接 Discard 单个文件，比右键更顺手。

#### 情况二：本地 commit 了，但还没 push，想把本地回退到远端

本地 commit 了几次，发现方向走错了，想回到 `origin/main`。

**操作**：

1. 切到 **History** 标签页
2. 找到远端那个 commit——通常标着 `origin/main`（或你对应的分支名）
3. **右键点击**那个 commit → 选 **Reset to Commit → Hard**
4. 确认 → 本地完全回到远端状态

> ⚠️ Hard reset 不可逆。本地那几次 commit 会真的没掉。

#### 速查

| 状态 | 操作 | 在哪儿 |
| :--- | :--- | :--- |
| 改了文件但没 commit | Discard Changes | Changes 标签页 |
| 本地 commit 了但没 push | Reset to Commit (Hard) | History → 右键 origin commit |

---

## PyCharm + GitHub Desktop 协同

### 它俩怎么同步的（其实不靠你同步）

第一次发现的时候我愣了好几秒。它们居然不用我手动同步。就共享同一个文件夹。像两个人看同一本书，不用传纸条。

```
PyCharm opens ~/Documents/my-first-repo     ✍️ writing code
              ↓ saves files
     my-first-repo folder                   📁 the book
              ↓ auto-detected
  GitHub Desktop shows changes ✓            👀 already knows
```

没有连接线、没有配置文件、没有同步按钮。文件夹变了，它就知道了。就这样。

你只需要 PyCharm 打开这个文件夹，GitHub Desktop 也打开同一个文件夹。没了。

### 操作步骤

PyCharm 里写代码，切窗口自动保存。切到 GitHub Desktop，左边 Changes 已经列好了。写一句 summary，比如"修了个 bug"或者"登录页收工"。点 **Commit to main**，顶部变 **Push origin**，再点一下。发出去了。

---

## PyCharm 配置

| 设置项 | 值 | 位置 |
| :--- | :--- | :--- |
| 主题 | Light，暗黑模式算了 | Settings → Appearance |
| 字体大小 | 15 | Settings → Editor → Font |
| 自动保存 | 切换窗口时 | Settings → System Settings |

---

<a id="workbuddy-cn"></a>

## WorkBuddy

一个桌面 AI 智能体——你可以理解为 Claude，但以工作区为原生单位。每个项目独立一个工作区文件夹，智能体能读你的文件、跑命令、改代码、通过连接器接通外部服务。

### 工作区模式

WorkBuddy 用工作区来组织项目。每个工作区是一个文件夹，比如 `~/WorkBuddy/2026-08-03-16-17-13/`。里面有你的项目文件、`.workbuddy/` 目录存记忆和日志，还有智能体的完整上下文。

切换项目就是打开一个新工作区。互不干扰，干干净净。

### 三大核心能力

| 能力 | 做什么 | 实际例子 |
| :--- | :--- | :--- |
| **Skills 技能** | 按需加载的预设工作流 | `momo` 技能设定助手人格；`data-maintenance` 跑系统清理 |
| **自动化** | 按定时器运行的任务 | 每日自我进化审查、凌晨 2 点系统清理 |
| **连接器（MCP）** | 接通外部服务 | 乐享知识库、腾讯文档、微信支付、智能体邮箱 |

### 我接入了哪些连接器

| 连接器 | 用途 |
| :--- | :--- |
| **乐享知识库** | 搜索、阅读、写入文档 |
| **腾讯文档** | 在线创建编辑文档 |
| **微信支付** | 支付和智能体卡片管理 |
| **Agent Mail** | 在智能体界面收发邮件 |
| **ima 知识库** | 个人知识库搜索 |

### 我实际上怎么用它

WorkBuddy 是我做正经结构化工作的地方。不是那种随口一问的——是需要计划、多步骤、留下记录的那种。

**日常节奏**：打开 WorkBuddy → 接着上次的进度 → 智能体自动读取工作区记忆 → 干活 → 记忆自动归档。

**用它学 Git**：我问 Momo（我的 WorkBuddy 人格）解释概念、实时编辑笔记、引导操作。WorkBuddy 能读我整个 `my-first-repo` 文件夹，永远知道上下文。

**真正好用的地方**：`.workbuddy/memory/` 目录。每个工作阶段都留下每日日志。智能体会记得昨天聊了什么、定了什么、还有什么没做完。我从来不用重新解释一遍。

### 关键路径

| 项目 | 路径 |
| :--- | :--- |
| 应用 | `/Applications/WorkBuddy.app` |
| 工作区 | `~/WorkBuddy/` |
| 记忆（按工作区） | `.workbuddy/memory/` |
| 技能（用户级） | `~/.workbuddy/skills/` |
| 全局记忆 | `~/.workbuddy/MEMORY.md` |

---

<a id="claude-code-cn"></a>

## Claude Code

Anthropic 出品的命令行 AI 编程智能体。跟桌面聊天应用不一样，Claude Code 住在终端里——`cd` 进项目跑个 `claude`，它就吃进你整个代码库，开始帮你干活。

### 为什么是 Claude Code

它是终端原生的。没有 GUI，没有独立的窗口——就是你的黑框框 + 一个懂你项目的智能体。适合快速改代码、code review，还有你已经在终端里的时候随手叫一下。

### 安装

```bash
# npm 安装
npm install -g @anthropic-ai/claude-code

# 或者 Homebrew
brew install claude-code

# 在任意项目里启动
cd 你的项目
claude
```

### 能做什么

| 能力 | 对我有什么用 |
| :--- | :--- |
| 全项目上下文 | 一次吃掉整个文件夹，不用一个一个指 |
| 终端原生 | 跑 shell 命令、git 操作、构建脚本 |
| 直接改文件 | 原地读写，不绕弯 |
| Git 集成 | 懂分支、diff、提交历史 |
| 多模型 | 默认 Claude，CC Switch 一键切 |

### 用 CC Switch 接入 DeepSeek

Claude Code 默认用 Claude 自己的模型。CC Switch 可以切 DeepSeek（或其他）：

1. 下载 [CC Switch](https://github.com/cc-switch/cc-switch) ——给 Claude Code 切换后端模型的工具
2. 按说明配好 DeepSeek API Key
3. 重启 Claude Code，在 Claude 和 DeepSeek 之间随意切

同一个终端，根据任务选最合适的模型。

### Claude Code vs WorkBuddy

| | Claude Code | WorkBuddy |
| :--- | :--- | :--- |
| 界面 | 终端 CLI | 桌面应用 |
| 最适合 | 快速编程、终端原生操作 | 结构化项目、复杂工作流 |
| 状态 | 每次对话无记忆 | 按工作区持久化记忆 |
| 强项 | 快、简单、懂 Git | 自动化、连接器、记忆系统 |

互补关系。Claude Code 是我的快刀，随手拔。WorkBuddy 是我的工作台，规划、组织、记录。

### 我的工具链

```
WorkBuddy               🧠 planning, editing, automation
       ↓
Claude Code             🔧 quick coding, model switch
       ↓
PyCharm                 💻 review & hand-edit code
       ↓
GitHub Desktop          🚀 commit & push to GitHub
```

四个工具共享同一个项目文件夹。各干各的强项，不打架。

### 快速检查

```bash
# 确认装好了
claude --version

# 如果需要，给终端开权限
# 系统设置 → 隐私与安全性 → 开发者工具 → 终端
```

---

<a id="github-pages-cn"></a>

## GitHub Pages 建站

这是我第一次跑偏去学 Git 之外的东西。很久之后才意识到，Git 默默把整个过程都管了。

### 做了什么

建了 `andyttc05.github.io` 仓库，GitHub 一看这名字就把 Pages 打开了。拿纯 HTML 和 CSS 写的，没框架、没构建工具，几个文件往上一丢。拆成 `index.html`（英文）和 `zh.html`，做了个卡片按钮跳来跳去。塞了点 Pull Quote、渐入动效、交替背景，让它能随屏幕大小自适应。然后花了不少时间追一个 Safari 上 hover 颜色不对的 bug。最后搞定了。

### 学到的

| 概念 | 要点 |
| :--- | :--- |
| GitHub Pages | 仓库名叫 `用户名.github.io`，自动部署，免费域名 |
| 静态网站 | HTML + CSS，浏览器直接打开，不需要服务器 |
| 双语设计 | 两个文件，一个卡片切换，页面刷新跳转 |
| 设计迭代 | PyCharm 改代码，Desktop commit，30 秒上线 |

---

## 开源协议（License）

### 为什么要贴 License

代码公开在 GitHub 上，不等于别人就能合法地用。版权法默认"All rights reserved"——没贴 License 的公开仓库，别人看了也白看，碰都不能碰。

贴了 License 就相当于说：嘿，可以用我的代码，遵守这几条规矩就行。

### 常见协议速查

| 协议 | 一句话 |
| :--- | :--- |
| MIT | 随便用！改也行、卖也行，只要留着我的名字 |
| Apache 2.0 | 跟 MIT 差不多，多一层专利保护，大公司喜欢 |
| GPL | 可以用，但你改完的代码也必须开源（传染性） |

### 我的选择：MIT

选了 MIT。最宽松，最主流。别人拿去用、改、卖，都行——只要保留我的版权声明。

### 怎么加 License

**GitHub 网页一键生成**：

1. 仓库主页 → **Add file** → **Create new file**
2. 文件名填 `LICENSE`
3. 右边弹出 **Choose a license template** → 点它
4. 选 MIT，填年份和名字 → **Review and submit**
5. Commit → 搞定

GitHub Desktop 里也行：在文件夹里新建一个叫 `LICENSE` 的文件（注意没有后缀），把协议内容贴进去，Push。

> 💡 LICENSE 不需要更新。MIT 不会过期，放上去就一直有效。有人改年份为 `2026-2027`，但完全不是必须的。

---

## 常踩的坑

<details open>
<summary>坑 1：「No local changes」不是报错</summary>
<br>

commit + push 完了，工作区安安静静。"No local changes" 是 Git 在说"全搞定了，没落东西"。

</details>

<details open>
<summary>坑 2：.gitignore 有个盲点</summary>
<br>

`.gitignore` 只管没跟踪的文件。已经 `git add` 过的，它装看不见。

要脱钩：

```bash
git rm --cached -r path/to/file
```

文件还在本地，只是从暂存区拿下来。

</details>

<details open>
<summary>坑 3：仓库移动不会丢</summary>
<br>

Git 仓库就是个文件夹，里面藏了个 `.git` 目录。这目录装着所有东西：你的历史、连到哪、拍过的每一张快照。

整个文件夹拖到哪都行，一切照常。唯一要记住的：GitHub Desktop 需要 **File → Add local repository** 指到新位置。

</details>

---

## 工具链

| 工具 | 状态 |
| :--- | :---: |
| **WorkBuddy** | ✅ |
| **Claude Code** | ✅ |
| **GitHub Desktop** | ✅ |
| **PyCharm**（Light，字体 15） | ✅ |
| **GitHub Pages** → [andyttc05.github.io](https://andyttc05.github.io) | ✅ |
| **Git** | ✅ |

### 关键路径

| 项目 | 路径 |
| :--- | :--- |
| 仓库 | `~/Documents/my-first-repo` |
| 远程 | `https://github.com/andyttc05/my-first-repo` |
| Git 配置 | `~/.config/git/config` |

---

## 如何重置工具

把配置目录 mv 到 `/tmp/`，工具就什么都不记得了。干净重来：

```bash
# PyCharm
mv ~/Library/Application\ Support/JetBrains/PyCharm2026.1 /tmp/removed-pycharm

# GitHub Desktop
mv ~/Library/Application\ Support/GitHub\ Desktop /tmp/removed-github-desktop
```

旧配置就躺在 `/tmp/`，没丢。想反悔了随时去捡回来。

---

## 改写 Git 历史（高级）

想清楚再动手。改写 commit hash，别人 clone 过的就全乱了。两种场景才值得：密码或者隐私信息不小心交上去了，或者提交历史跟草稿纸似的想重来。

### 场景 A：替换历史里的敏感字符串

```bash
cd ~/path/to/your-repo

git filter-branch --force --tree-filter \
  "grep -rl 'string-to-replace' . 2>/dev/null | xargs -I{} sed -i '' 's|old-string|new-string|g' {}" \
  --prune-empty -- --all
```

推送到 GitHub：

```bash
git push --force-with-lease origin main
```

`--force-with-lease` 比 `--force` 安全。别人在你之后推了新东西，它会直接拒绝。

### 场景 B：完全清零历史（文件保留）

```bash
cd ~/path/to/your-repo

git checkout --orphan clean-slate
git add -A
git commit -m "clean slate"
git push --force origin clean-slate:main
```

然后清理本地：

```bash
git checkout main
git reset --hard origin/main
git branch -D clean-slate
```

### 场景 C：完整流程（脏历史 → 干净仓库）

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

### 做完之后的教训

| 教训 | 细节 |
| :--- | :--- |
| 提交前看一眼 | `git diff` 先跑一遍，敏感信息别进历史 |
| 得用终端 | GitHub Desktop 不支持 force push |
| 别直接 `--force` | `--force-with-lease` 更安全，别人推过新东西会拒绝你 |
| 终端 push 要 token | Desktop 用 OAuth 免密，终端还是得 PAT。忘了怎么弄 → [第一次 Push](#first-push-cn) 第④步 |
| 记得打扫 | 跑 `branch -D` 删掉临时分支 |
| force push 之后要 reset | `--force` 之后本地 main 和远程 main 历史对不上了，`git pull` 会报错。跑 `git fetch origin && git reset --hard origin/main` 让它们重归于好 |

---

## 下一步

分支已经会了。接下来：正经开个 Python 小项目——从小开始，用分支管版本，做一个能跑的东西。之后可能搞 GitHub Actions，每次 push 自动部署网站。或者换 VS Code 用一周，换换口味。不赶时间，想玩什么就玩什么。

---

<br>

<div align="center">

> "每个高手都敲过第一次 `git init`。这份笔记，就是那个起点的样子。"

</div>
