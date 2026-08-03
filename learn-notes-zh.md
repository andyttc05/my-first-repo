[English](learning-notes.md) &nbsp;|&nbsp; **中文**

<br>

<div align="center">

# 我的 Git 学习笔记

### *从零到 Git/GitHub。一个问题，一个答案。*

</div>

<br>

<p align="center">
  <a href="https://andyttc05.github.io"><img src="https://img.shields.io/badge/在线网站-andyttc05.github.io-4c1?style=flat-square" alt="GitHub Pages"></a>
  <a href="https://github.com/andyttc05/my-first-repo/blob/main/learning-notes.md"><img src="https://img.shields.io/badge/笔记-English-blue?style=flat-square" alt="English"></a>
  <img src="https://img.shields.io/badge/师傅-Momo-ff69b4?style=flat-square" alt="帮手">
  <img src="https://img.shields.io/badge/始于-2026.08-lightgrey?style=flat-square" alt="始于">
</p>

<br>

> "学东西最好的方法，就是在每一个"原来如此"消失之前把它记下来。"

---

## 核心概念

### Git 是什么

你拍照，回头能翻出来看。Git 就是给你的代码拍照。敲 `git commit`，它就拍一张快照。明天你能翻回去，看到"昨天这时候代码长什么样"。就这样，没了。

### 四个区域

```
工作区            ✍️ 我写代码的地方
  ↓  git add      📋 "这张照片我要了"
暂存区            📸 排队等拍照
  ↓  git commit   📷 咔嚓！存进相册
本地仓库          📚 你电脑上的相册
  ↓  git push     ☁️ 传到云端
GitHub（云端）    🌐 永远不会丢的备份
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
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
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
cd 你的项目文件夹
git init
git add .
git commit -m "first commit"
git remote add origin 刚才复制的网址
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
git commit -m "这次做了什么"
git push
```

不想碰终端也行。上面三行，在 GitHub Desktop 里各点一下就好。

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
PyCharm 打开 ~/Documents/my-first-repo     ✍️ 写代码
              ↓ 保存文件
     my-first-repo 文件夹                  📁 书在这里
              ↓ 自动检测
  GitHub Desktop 显示改动 ✓                👀 它已经知道了
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
git rm --cached -r 文件路径
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
| **Git** v2.50.1 | ✅ |
| **GitHub Desktop** | ✅ |
| **PyCharm** 2026.1（Light，字体 15） | ✅ |
| **GitHub Pages** → [andyttc05.github.io](https://andyttc05.github.io) | ✅ |
| **Claude Desktop** | |

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
  "grep -rl '要被替换的字符串' . 2>/dev/null | xargs -I{} sed -i '' 's|旧字符串|新字符串|g' {}" \
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

# 替换历史字符串
git filter-branch --force --tree-filter \
  "grep -rl '/Users/你的名字/' . 2>/dev/null | xargs -I{} sed -i '' 's|/Users/你的名字/|~/|g' {}" \
  --prune-empty -- --all

# 推送干净版本
git push --force-with-lease origin main

# 或者干脆清零，只留当前文件
git checkout --orphan clean-slate
git add -A
git commit -m "clean slate"
git push --force origin clean-slate:main

# 清理
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

## 学习时间线

| 时间 | 里程碑 |
| :--- | :--- |
| 8/1 中午 | 敲下人生第一个 `git commit`。像第一次按快门 |
| 8/1 下午 | 第一次 `git push`。黑框框、token、手心出汗，全套 |
| 8/1 晚上 | 发现 GitHub Desktop。等等，有按钮？不用终端？ |
| 8/1 深夜 | `.gitignore` 终于通了。PyCharm 和 GitHub Desktop 开始互相认识了 |
| 8/2 凌晨 | 把仓库从桌面拖到 Documents……它就这么跟着走了。Git 真离谱 |
| 8/2 白天 | 从零建了中英双语的 GitHub Pages 主页 → [点开看看](https://andyttc05.github.io) |
| 8/2 下午 | 仓库双语化，两套 README、两套笔记 |
| 8/3 白天 | 给四份文档翻了个新，加徽章、调间距 |
| 8/3 晚上 | 改了中文文件名、整理了笔记结构、见识了什么是 AI 味 |
| 8/3 又一会 | 学会 Discard Changes 和 Reset to Commit，还原云端版本再也不用重新 clone |

---

## 下一步

GitHub Pages 上线了，双语笔记也到位了，文档都翻了一遍。接下来想搞 Git 分支，可能正经开个 Python 项目。再往后没计划，跟着好奇心走吧。VS Code 和 JavaScript 迟早会碰。能给开源项目贡献点东西也挺好。到时候再说。

---

<br>

<div align="center">

> "每个高手都敲过第一次 `git init`。这份笔记，就是那个起点的样子。"

</div>
