---
name: using-git-worktrees
description: 开始实现前用于询问用户是否创建隔离 worktree，按用户选择创建隔离工作区或直接在当前分支开发
---

# 使用 Git 工作树

## 概述

开始实现前，先让用户选择开发工作区：创建隔离 worktree，或直接在当前分支开发。不要自动创建 worktree。

**核心原则：** 先检测现有隔离。未在隔离区时展示选择。用户选择隔离后，优先使用原生工具，再回退到 git。绝不与 harness 对抗。

**开始时宣布：** "我正在使用 using-git-worktrees 技能来确认开发工作区。"

## 步骤 0：检测当前工作区

**创建任何东西之前，先检查你是否已经在一个隔离的工作区里，并记录当前分支。**

```bash
GIT_DIR=$(cd "$(git rev-parse --git-dir)" 2>/dev/null && pwd -P)
GIT_COMMON=$(cd "$(git rev-parse --git-common-dir)" 2>/dev/null && pwd -P)
BRANCH=$(git branch --show-current)
WORKTREE_PATH=$(git rev-parse --show-toplevel)
```

**Submodule 守卫：** 在 git submodule 内 `GIT_DIR != GIT_COMMON` 也为真。在判定"已经在 worktree 内"之前，先确认你不在 submodule 里：

```bash
# 如果这条命令返回路径，说明你在 submodule 里，不是 worktree —— 按普通仓库处理
git rev-parse --show-superproject-working-tree 2>/dev/null
```

**如果 `GIT_DIR != GIT_COMMON`（且不是 submodule）：** 你已经在一个 linked worktree 内。跳到步骤 3（项目设置）。**不要**再创建一个 worktree，也不要再询问是否创建。

按分支状态报告：

- 在某个分支上："已经在隔离工作区 `<path>`，分支 `<name>`。"
- 分离 HEAD："已经在隔离工作区 `<path>`（分离 HEAD，由外部管理）。完成时需要创建分支。"

**如果 `GIT_DIR == GIT_COMMON`（或在 submodule 内）：** 你在一个普通的仓库检出里。

## 步骤 1：展示工作区选项

**除非用户已经在当前对话中明确选择过工作区，否则必须先展示选项并等待回复。**

准确展示以下选项：

```
开始实现前，请选择开发工作区：

1. 创建隔离 worktree 开发（保护当前分支，完成后可合并/清理）
2. 直接在当前分支开发（当前路径：<path>，当前分支：<branch>）

请选择 1 或 2。
```

**如果用户选择 2：** 不创建 worktree。报告："将在当前分支 `<branch>`、路径 `<path>` 继续开发。"然后跳到步骤 3。

**如果用户选择 1：** 继续步骤 2 创建隔离工作区。

**如果用户已在当前对话或 instructions 中明确声明偏好：** 遵循该选择，不再重复询问。

## 步骤 2：创建隔离工作区

**只有用户选择创建隔离 worktree 后，才执行本步骤。你有两种机制。按这个顺序尝试。**

### 2a. 原生 Worktree 工具（首选）

用户已经选择隔离工作区（步骤 1 已确认）。你是否已经有创建 worktree 的方法？可能是名为 `EnterWorktree`、`WorktreeCreate` 的工具、`/worktree` 命令，或 `--worktree` 标志。如果有，用它，然后跳到步骤 3。

原生工具自动处理目录放置、分支创建和清理。在你已经有原生工具的情况下使用 `git worktree add`，会创建你的 harness 看不到也无法管理的"幻影状态"。

只有在没有原生 worktree 工具可用时，才进入步骤 2b。

### 2b. Git Worktree 回退

**只在步骤 2a 不适用时使用** —— 你没有可用的原生 worktree 工具。手动用 git 创建 worktree。

#### 目录选择

按以下优先级。明确的用户偏好始终优先于观察到的文件系统状态。

1. **检查你的 instructions 里是否声明过 worktree 目录偏好。** 如果用户已指定，不再询问直接用。

2. **检查是否存在项目本地的 worktree 目录：**

   ```bash
   ls -d .worktrees 2>/dev/null     # 首选（隐藏目录）
   ls -d worktrees 2>/dev/null      # 备选
   ```

   找到就用。如果两者都存在，`.worktrees` 优先。

3. **检查是否存在全局目录：**

   ```bash
   project=$(basename "$(git rev-parse --show-toplevel)")
   ls -d ~/.config/superpowers/worktrees/$project 2>/dev/null
   ```

   找到就用（兼容老的全局路径）。

4. **如果没有其他可参考的信息**，使用项目根目录下的 `.worktrees/`。

#### 安全验证（仅项目本地目录）

**创建项目本地 worktree 前必须验证目录已被忽略：**

```bash
git check-ignore -q .worktrees 2>/dev/null || git check-ignore -q worktrees 2>/dev/null
```

**如果未被忽略：** 添加到 .gitignore，提交该改动，然后继续。

**为什么关键：** 防止 worktree 内容被意外提交到仓库。

全局目录（`~/.config/superpowers/worktrees/`）无需验证。

#### 创建工作树

```bash
project=$(basename "$(git rev-parse --show-toplevel)")

# 根据选定位置确定路径
# 项目本地：path="$LOCATION/$BRANCH_NAME"
# 全局：path="~/.config/superpowers/worktrees/$project/$BRANCH_NAME"

git worktree add "$path" -b "$BRANCH_NAME"
cd "$path"
```

**沙盒回退：** 如果 `git worktree add` 因权限错误（沙盒拒绝）失败，告诉用户沙盒阻止了 worktree 创建，并询问是否改为当前分支开发。用户同意后，原地运行 setup 和基线测试。

## 步骤 3：项目设置

自动检测并运行相应的设置命令：

```bash
# Node.js
if [ -f package.json ]; then npm install; fi

# Rust
if [ -f Cargo.toml ]; then cargo build; fi

# Python
if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
if [ -f pyproject.toml ]; then poetry install; fi

# Go
if [ -f go.mod ]; then go mod download; fi
```

## 步骤 4：验证基线干净

运行测试确保工作区初始状态干净：

```bash
# 使用项目对应的命令
npm test / cargo test / pytest / go test ./...
```

**如果测试失败：** 报告失败，询问是继续还是排查。

**如果测试通过：** 报告就绪。

### 报告

```
开发工作区已就绪：<full-path>
工作区类型：<linked-worktree|current-branch>
当前分支：<branch>
测试通过（<N> 个测试，0 个失败）
准备实现 <feature-name>
```

## 快速参考

| 情况 | 操作 |
|------|------|
| 已在 linked worktree 内 | 跳过创建（步骤 0） |
| 在 submodule 内 | 按普通仓库处理（步骤 0 守卫） |
| 普通仓库且未选择工作区 | 展示 2 个选项并等待用户选择 |
| 用户选择当前分支 | 不创建 worktree，原地开发 |
| 用户选择隔离 worktree 且有原生工具 | 用它（步骤 2a） |
| 用户选择隔离 worktree 且没有原生工具 | git worktree 回退（步骤 2b） |
| `.worktrees/` 存在 | 用它（验证已忽略） |
| `worktrees/` 存在 | 用它（验证已忽略） |
| 两者都存在 | 用 `.worktrees/` |
| 都不存在 | 检查 instructions 文件，再使用 `.worktrees/` |
| 全局路径存在 | 用它（向后兼容） |
| 目录未被忽略 | 添加到 .gitignore + 提交 |
| 创建时权限错误 | 沙盒回退，询问是否原地工作 |
| 基线测试失败 | 报告失败 + 询问 |
| 无 package.json/Cargo.toml | 跳过依赖安装 |

## 常见错误

### 与 harness 对抗

- **问题：** 平台已经提供隔离的情况下还在用 `git worktree add`
- **修复：** 步骤 0 检测现有隔离。用户选择隔离后，步骤 2a 让位给原生工具。

### 跳过检测

- **问题：** 在已有的 worktree 内嵌套创建另一个 worktree
- **修复：** 创建任何东西之前都先跑步骤 0

### 跳过用户选择

- **问题：** 未经用户选择就自动创建 worktree，或默认在当前分支开始实现
- **修复：** 普通仓库中必须先展示步骤 1 的两个选项并等待用户回复

### 跳过忽略验证

- **问题：** worktree 内容被跟踪，污染 git status
- **修复：** 创建项目本地 worktree 前始终使用 `git check-ignore`

### 假设目录位置

- **问题：** 造成不一致、违反项目约定
- **修复：** 遵循优先级：现有目录 > 全局历史路径 > instructions 文件 > 默认

### 带着失败的测试继续

- **问题：** 无法区分新 bug 和已有问题
- **修复：** 报告失败，获得明确许可后再继续

## 红线

**绝不：**

- 步骤 0 已检测到现有隔离时还创建 worktree
- 在普通仓库中未经用户选择就创建 worktree 或开始实现
- 在已有原生 worktree 工具（如 `EnterWorktree`）的情况下还用 `git worktree add`。这是 #1 错误——有就用。
- 用户选择当前分支开发后仍创建 worktree
- 用户选择隔离 worktree 后跳过步骤 2a 直接跳到步骤 2b 的 git 命令
- 不验证已忽略就创建项目本地 worktree
- 跳过基线测试验证
- 不询问就带着失败的测试继续

**始终：**

- 先跑步骤 0 检测
- 普通仓库中先展示工作区选项
- 用户选择隔离后，优先原生工具，其次 git 回退
- 遵循目录优先级：现有目录 > 全局历史路径 > instructions 文件 > 默认
- 项目本地目录验证已忽略
- 自动检测并运行项目设置
- 验证测试基线干净

## 集成

**被以下技能调用：**

- **brainstorming**（阶段 4）- 设计通过且需要实现时必需
- **subagent-driven-development** - 执行任何任务前用于选择开发工作区
- **executing-plans** - 执行任何任务前用于选择开发工作区
- 任何需要在隔离 worktree 与当前分支之间选择的技能

**配合使用：**

- **finishing-a-development-branch** - 工作完成后清理时必需
