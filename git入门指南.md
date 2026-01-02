# Git 从零到 GitHub 完整入门指南

> 本文档记录了从安装 Git 到成功将项目上传到 GitHub 的完整流程，适合零基础初学者。

---

## 📋 目录

1. [Git 是什么？](#git-是什么)
2. [安装 Git](#安装-git)
3. [配置 Git](#配置-git)
4. [Git 基本概念](#git-基本概念)
5. [从零到 GitHub 完整流程](#从零到-github-完整流程)
6. [常用 Git 命令速查](#常用-git-命令速查)
7. [日常开发工作流](#日常开发工作流)
8. [常见问题解决](#常见问题解决)
9. [最佳实践](#最佳实践)

---

## Git 是什么？

**Git** 是一个**分布式版本控制系统**，简单理解就是：

- 📝 **记录代码的每次修改**：谁改了什么、什么时候改的、为什么改
- 🔄 **可以回到任意历史版本**：代码改坏了？一键回退
- 👥 **多人协作**：多人同时开发，自动合并代码
- ☁️ **备份到云端**：代码上传到 GitHub，不怕丢失

**GitHub** 是一个代码托管平台，可以：
- 把你的代码存到云端
- 展示你的项目给别人看
- 和其他开发者协作

---

## 安装 Git

### Windows 系统

1. **下载 Git**
   - 访问：https://git-scm.com/download/win
   - 下载最新版本的 Git for Windows

2. **安装 Git**
   - 运行下载的安装程序
   - ⚠️ **重要**：安装时勾选 **"Add Git to PATH"**（将 Git 添加到环境变量）
   - 其他选项保持默认即可

3. **验证安装**
   打开 PowerShell 或 CMD，输入：
   ```powershell
   git --version
   ```
   如果显示版本号（如 `git version 2.xx.x`），说明安装成功！

### 配置环境变量（如果安装后无法使用）

如果提示 `'git' 不是内部或外部命令`，需要手动配置环境变量：

1. 找到 Git 安装目录，通常在：
   - `C:\Program Files\Git\bin\`
   - 或 `E:\install_program\Git\bin\`（你的情况）

2. 添加到系统 PATH：
   - 右键"此电脑" → 属性 → 高级系统设置 → 环境变量
   - 在"系统变量"中找到 `Path`，点击编辑
   - 点击"新建"，输入 Git 的 `bin` 目录路径
   - 确定保存

3. **重新打开 PowerShell**，再次测试 `git --version`

---

## 配置 Git

### 1. 设置用户信息（必须）

Git 需要知道你是谁，才能记录提交：

```powershell
# 设置全局用户名（所有仓库都用这个）
git config --global user.name "你的名字"

# 设置全局邮箱（建议用 GitHub 邮箱）
git config --global user.email "你的邮箱@example.com"
```

**示例：**
```powershell
git config --global user.name "Zhang San"
git config --global user.email "zhangsan@example.com"
```

### 2. 验证配置

```powershell
git config --global user.name
git config --global user.email
```

### 3. 查看所有配置

```powershell
git config --list
```

---

## Git 基本概念

### 三个重要区域

```
工作区 (Working Directory)
    ↓ git add
暂存区 (Staging Area)
    ↓ git commit
本地仓库 (Local Repository)
    ↓ git push
远程仓库 (Remote Repository - GitHub)
```

1. **工作区**：你正在编辑的代码文件
2. **暂存区**：准备提交的文件（`git add` 后）
3. **本地仓库**：已提交的代码历史（`git commit` 后）
4. **远程仓库**：GitHub 上的代码（`git push` 后）

### 基本工作流

```
修改代码 → git add → git commit → git push
  ↓          ↓          ↓           ↓
工作区    暂存区    本地仓库    远程仓库
```

---

## 从零到 GitHub 完整流程

### 第一步：初始化本地仓库

```powershell
# 1. 进入你的项目目录
cd E:\cursor_program\agent_study

# 2. 初始化 Git 仓库
git init
```

会看到：`Initialized empty Git repository in ...`

### 第二步：创建 .gitignore 文件（重要！）

`.gitignore` 告诉 Git 哪些文件**不要**提交（比如密码、临时文件等）。

**创建 `.gitignore` 文件：**

```gitignore
# 环境变量文件（包含敏感信息）
.env
*.env

# Python 相关
__pycache__/
*.py[cod]
*.so
venv/
env/

# IDE
.vscode/
.idea/

# 数据库文件
*.db
*.sqlite

# 日志文件
*.log
```

### 第三步：添加文件到暂存区

```powershell
# 添加所有文件
git add .

# 或者只添加特定文件/文件夹
git add applications/sql_agent/
```

### 第四步：查看状态

```powershell
git status
```

会显示：
- 哪些文件已添加到暂存区（绿色）
- 哪些文件还没添加（红色）

### 第五步：提交到本地仓库

```powershell
git commit -m "提交说明"
```

**提交说明要清晰，例如：**
- `"初始提交：添加 LangChain Agent 学习项目"`
- `"添加 SQL Agent 功能"`
- `"修复数据库连接问题"`

### 第六步：在 GitHub 创建仓库

1. 登录 GitHub：https://github.com
2. 点击右上角 `+` → `New repository`
3. 填写信息：
   - **Repository name**：仓库名（如 `agent_study`）
   - **Description**：描述（可选）
   - **Public/Private**：公开或私有
   - ⚠️ **不要勾选** "Initialize with README"（本地已有代码）
4. 点击 `Create repository`

### 第七步：连接本地仓库到 GitHub

```powershell
# 添加远程仓库（替换成你的 GitHub 用户名和仓库名）
git remote add origin https://github.com/你的用户名/仓库名.git

# 验证连接
git remote -v
```

### 第八步：推送到 GitHub

```powershell
# 第一次推送（设置上游分支）
git push -u origin main
```

**如果分支名是 `master` 而不是 `main`：**
```powershell
# 重命名分支
git branch -M main

# 然后推送
git push -u origin main
```

### 第九步：处理可能的错误

#### 错误1：网络连接失败

**问题：** `Failed to connect to github.com port 443`

**解决：**
- 如果使用代理，配置 Git 使用代理：
  ```powershell
  git config --global http.proxy http://127.0.0.1:7890
  git config --global https.proxy http://127.0.0.1:7890
  ```
- 或使用 SSH 连接（更稳定，见下文）

#### 错误2：远程仓库有本地没有的内容

**问题：** `Updates were rejected because the remote contains work...`

**解决：**
```powershell
# 先拉取远程内容并合并
git pull origin main --allow-unrelated-histories

# 如果有冲突，解决冲突后
git commit -m "合并远程仓库内容"

# 再推送
git push -u origin main
```

#### 错误3：需要登录认证

**问题：** 弹出 GitHub 登录对话框

**解决：**
- 点击 "Sign in with your browser"
- 在浏览器中登录并授权
- 完成后会自动继续推送

---

## 使用 SSH 连接 GitHub（推荐）

SSH 连接更稳定，不需要每次输入密码。

### 1. 生成 SSH 密钥

```powershell
ssh-keygen -t ed25519 -C "你的邮箱@example.com"
```

按提示操作：
- 保存位置：直接回车（使用默认位置）
- 密码：可设置，也可直接回车

### 2. 复制公钥

```powershell
cat ~/.ssh/id_ed25519.pub
```

会显示类似：
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI... 你的邮箱@example.com
```

**复制这整行内容**

### 3. 添加到 GitHub

1. 登录 GitHub
2. 右上角头像 → `Settings`
3. 左侧 `SSH and GPG keys`
4. 点击 `New SSH key`
5. **Title**：例如 `My Windows PC`
6. **Key**：粘贴刚才复制的公钥
7. 点击 `Add SSH key`

### 4. 测试 SSH 连接

```powershell
ssh -T git@github.com
```

如果看到：
```
Hi 你的用户名! You've successfully authenticated...
```
说明 SSH 配置成功！

### 5. 修改远程地址为 SSH

```powershell
# 查看当前远程地址
git remote -v

# 修改为 SSH 地址
git remote set-url origin git@github.com:你的用户名/仓库名.git

# 验证
git remote -v
```

### 6. 重新推送

```powershell
git push -u origin main
```

---

## 常用 Git 命令速查

### 基础命令

| 命令 | 作用 | 示例 |
|------|------|------|
| `git init` | 初始化仓库 | `git init` |
| `git status` | 查看状态 | `git status` |
| `git add <文件>` | 添加文件到暂存区 | `git add .` |
| `git commit -m "说明"` | 提交到本地仓库 | `git commit -m "更新代码"` |
| `git log` | 查看提交历史 | `git log` |
| `git push` | 推送到远程仓库 | `git push` |
| `git pull` | 从远程拉取更新 | `git pull` |

### 远程仓库命令

| 命令 | 作用 |
|------|------|
| `git remote add origin <地址>` | 添加远程仓库 |
| `git remote -v` | 查看远程仓库 |
| `git remote set-url origin <地址>` | 修改远程地址 |
| `git push -u origin main` | 首次推送并设置上游 |

### 分支命令

| 命令 | 作用 |
|------|------|
| `git branch` | 查看所有分支 |
| `git branch <分支名>` | 创建新分支 |
| `git checkout <分支名>` | 切换分支 |
| `git branch -M main` | 重命名当前分支为 main |

### 查看和比较

| 命令 | 作用 |
|------|------|
| `git diff` | 查看工作区的修改 |
| `git diff --staged` | 查看暂存区的修改 |
| `git show` | 查看最后一次提交的详情 |

---

## 日常开发工作流

### 标准工作流

```powershell
# 1. 开始工作前，先拉取最新代码
git pull

# 2. 修改代码...

# 3. 查看修改了哪些文件
git status

# 4. 添加修改的文件
git add .

# 5. 提交
git commit -m "描述你的修改"

# 6. 推送到 GitHub
git push
```

### 提交信息规范

好的提交信息应该：
- ✅ **清晰描述**：`"添加 SQL Agent 功能"`
- ✅ **说明原因**：`"修复数据库连接超时问题"`
- ❌ **避免模糊**：`"更新"`、`"修改"`

**格式建议：**
```
类型: 简短描述

详细说明（可选）
```

**类型示例：**
- `feat:` 新功能
- `fix:` 修复 bug
- `docs:` 文档更新
- `style:` 代码格式
- `refactor:` 重构

---

## 常见问题解决

### Q1: `fatal: not a git repository`

**原因：** 当前目录不是 Git 仓库

**解决：**
```powershell
git init
```

### Q2: `Author identity unknown`

**原因：** 没有配置用户信息

**解决：**
```powershell
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

### Q3: `git: command not found`

**原因：** Git 没有添加到环境变量

**解决：** 参考[配置环境变量](#配置环境变量如果安装后无法使用)部分

### Q4: 推送时弹出 vim 编辑器

**原因：** Git 需要输入合并提交信息

**解决：**
1. 按 `Esc` 键
2. 输入 `:wq`
3. 按 `Enter` 键

### Q5: 想撤销最后一次提交

```powershell
# 撤销提交，但保留修改
git reset --soft HEAD~1

# 完全撤销提交和修改（谨慎使用）
git reset --hard HEAD~1
```

### Q6: 想查看某个文件的修改历史

```powershell
git log --follow -- <文件名>
```

### Q7: 想回到某个历史版本

```powershell
# 查看提交历史
git log

# 回到某个提交（替换 COMMIT_ID）
git checkout COMMIT_ID

# 创建新分支回到某个版本
git checkout -b 新分支名 COMMIT_ID
```

---

## 最佳实践

### 1. 提交前检查

```powershell
# 提交前先查看修改了什么
git status
git diff
```

### 2. 频繁提交

- ✅ 每完成一个小功能就提交
- ✅ 提交信息要清晰
- ❌ 不要积累大量修改才提交

### 3. 保护敏感信息

- ✅ 使用 `.gitignore` 排除敏感文件
- ✅ 使用环境变量存储 API Key、密码
- ❌ 不要把密码、API Key 写死在代码里

### 4. 定期推送

- ✅ 每天工作结束前推送代码
- ✅ 重要功能完成后立即推送
- ❌ 不要只在本地提交，不推送

### 5. 拉取前先提交

```powershell
# 先提交本地修改
git add .
git commit -m "保存当前工作"

# 再拉取远程更新
git pull
```

### 6. 使用分支开发

```powershell
# 创建新分支开发新功能
git checkout -b feature/新功能名

# 开发完成后合并到主分支
git checkout main
git merge feature/新功能名
```

---

## 总结

### 完整流程回顾

1. ✅ **安装 Git** → 配置环境变量
2. ✅ **配置用户信息** → `git config --global user.name/email`
3. ✅ **初始化仓库** → `git init`
4. ✅ **创建 .gitignore** → 保护敏感信息
5. ✅ **添加文件** → `git add .`
6. ✅ **提交** → `git commit -m "说明"`
7. ✅ **创建 GitHub 仓库** → 在网页上操作
8. ✅ **连接远程** → `git remote add origin <地址>`
9. ✅ **推送** → `git push -u origin main`
10. ✅ **配置 SSH**（可选但推荐）→ 更稳定的连接

### 日常使用三件套

```powershell
git add .                    # 添加修改
git commit -m "提交说明"     # 提交
git push                     # 推送
```

---

## 下一步学习

- 📚 **Git 官方文档**：https://git-scm.com/doc
- 🎓 **GitHub 学习资源**：https://docs.github.com/zh/get-started
- 🔧 **Git 可视化工具**：GitKraken、SourceTree（可选）

---

## 本项目的 Git 配置记录

### 项目信息
- **仓库地址**：https://github.com/2033276091/LangChain-Agent-Study.git
- **本地路径**：`E:\cursor_program\agent_study`
- **分支**：`main`

### 已配置内容
- ✅ `.gitignore`：已配置，排除 `.env`、`__pycache__` 等
- ✅ 用户信息：已配置全局用户信息
- ✅ 远程仓库：已连接到 GitHub

### 常用操作

```powershell
# 查看状态
git status

# 添加并提交
git add .
git commit -m "你的提交说明"
git push

# 拉取最新代码
git pull
```

---

**🎉 恭喜！你已经掌握了 Git 的基本使用！**
