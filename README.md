# superpowers-zh（AI 编程超能力 · 中文增强版）

🌐 **简体中文** | [English (upstream)](https://github.com/obra/superpowers)

> 🦸 **superpowers（159k+ ⭐）完整汉化 + 4 个中国原创 skills** — 让 Claude Code / Copilot CLI / Hermes Agent / Cursor / Windsurf / Kiro / Gemini CLI / Qoder 等 **18 款 AI 编程工具**真正会干活。从头脑风暴到代码审查，从 TDD 到调试，每个 skill 都是经过实战验证的工作方法论。

Chinese community edition of [superpowers](https://github.com/obra/superpowers) — 20 skills across 18 AI coding tools, including full translations and China-specific development skills.

<!-- 效果对比 -->
<table>
<tr><td>

**没装 superpowers-zh：**
```
你：给用户模块加个批量导出功能
AI：好的，我来实现...（直接开始写代码）
    export async function exportUsers() { ... }
你：等等，格式不对，没分页，大数据量会 OOM...
```

</td><td>

**装了 superpowers-zh：**
```
你：给用户模块加个批量导出功能
AI：在开始实现之前，我需要了解几个关键问题：
    1. 导出格式是 CSV 还是 Excel？
    2. 预计数据量多大？需要异步处理吗？
    3. 有权限要求吗？
    → 给出 2-3 个方案，确认后再动手
```

</td></tr>
</table>

[![GitHub stars](https://img.shields.io/github/stars/jnMetaCode/superpowers-zh?style=social)](https://github.com/jnMetaCode/superpowers-zh)
[![private npm](https://img.shields.io/badge/npm-%40tianma%2Fsuperpowers--zh-blue)](http://192.168.21.9:4873/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://makeapullrequest.com)

> 📖 **配套阅读**：[《AI 编程实战 · 方法论三卷书》](https://book.aibuzhiyu.com/) — 10 个 AI 编程工具完整教程 + 真实踩坑 · superpowers 装好之后，配上方法论效率翻倍 · 在线书 + PDF · 永久免费

### 📊 项目规模

| 📦 翻译 Skills | 🇨🇳 中国特色 Skills | 🤖 支持工具 |
|:---:|:---:|:---:|
| **14** | **6** | **Claude Code / Copilot CLI / Hermes Agent / Cursor / Windsurf / Kiro / Gemini CLI / Codex / Aider / Trae / VS Code (Copilot) / DeerFlow / OpenCode / OpenClaw / Qwen Code / Antigravity / Claw Code / Qoder** |

---

## 这是什么？

[superpowers](https://github.com/obra/superpowers) 是目前最火的 AI 编程 skills 框架（159k+ stars），为 AI 编程工具提供**系统化的工作方法论**。

**superpowers-zh** 在完整翻译的基础上，新增了面向中国开发者的特色 skills。

### 🆚 与英文上游的区别（老被问，一次说清）

| 维度 | superpowers（英文上游） | superpowers-zh（中文增强版） |
|------|----------------------|---------------------------|
| ⭐ Star 数 | 159k+ | — |
| 📦 Skills 总数 | 14 | **20**（14 翻译 + 4 国产原创 + 2 上游历史保留） |
| 🌐 语言 | 英文 | 中文（技术术语保留英文） |
| 🤖 **支持工具** | **6 款**：Claude Code / Cursor / Codex / OpenCode / Copilot CLI / Gemini CLI | **18 款**：上述 6 款 + Hermes Agent / Trae / Kiro / Qwen Code（通义灵码）/ OpenClaw / Claw Code / Antigravity / DeerFlow / VS Code / Windsurf / Aider / Qoder |
| ⚡ **安装方式** | 按工具分别装（每款一条不同的 plugin marketplace 命令） | **`npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` 一条命令自动识别项目里的工具并安装**；识别不出可 `--tool <name>` 显式指定 |
| 🇨🇳 Git 平台 | GitHub 为主 | GitHub + Gitee + Coding + 极狐 GitLab + **CNB（腾讯云原生构建）** |
| 🇨🇳 CI/CD 示例 | GitHub Actions | GitHub Actions + Gitee Go + Coding CI + 极狐 CI + `.cnb.yml` |
| 🇨🇳 代码审查风格 | 西方直接风格 | 适配国内团队沟通文化 |
| 🇨🇳 Git 提交规范 | 无 | Conventional Commits 中文适配 |
| 🇨🇳 中文文档规范 | 无 | 中文排版 + 中英混排规则 + 告别机翻味 |
| ➕ MCP 服务器构建 | 无 | 独立 `mcp-builder` skill |
| ➕ 工作流执行器 | 无 | 独立 `workflow-runner` skill（多角色 YAML 编排） |
| 🔄 版本跟进 | 独立迭代 | **同步上游 + 国产增量叠加** |
| 🤝 接受新 skill PR | 一般不接受（原文：*"we don't generally accept contributions of new skills"*） | 欢迎 PR（中国开发者痛点优先） |
| 💬 社区 | Discord |  |
| 📜 License | MIT | MIT |

**一句话总结：** 英文上游 = 方法论内核；中文增强版 = 方法论内核 **+** 18 款工具一键适配 **+** 国内 Git/CI 生态 **+** 中文化表达习惯。

### 🤖 支持 18 款主流 AI 编程工具

| 工具 | 类型 | 一键安装 | 手动安装 |
|------|------|:---:|:---:|
| [Claude Code](https://claude.ai/code) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.claude/skills/` |
| [Copilot CLI](https://githubnext.com/projects/copilot-cli) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh --tool copilot` | `.claude/skills/` |
| [Hermes Agent](https://github.com/NousResearch/hermes-agent) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh --tool hermes` | `.hermes/skills/` |
| [Cursor](https://cursor.sh) | IDE | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.cursor/skills/` |
| [Windsurf](https://codeium.com/windsurf) | IDE | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.windsurf/skills/` |
| [Kiro](https://kiro.dev) | IDE | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.kiro/steering/` |
| [Gemini CLI](https://github.com/google-gemini/gemini-cli) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.gemini/skills/` |
| [Codex CLI](https://github.com/openai/codex) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.codex/skills/` |
| [Aider](https://aider.chat) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.aider/skills/` |
| [Trae](https://trae.ai) | IDE | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.trae/skills/` + `.trae/rules/` |
| [VS Code](https://code.visualstudio.com) (Copilot) | IDE 插件 | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.github/superpowers/` |
| [DeerFlow 2.0](https://github.com/bytedance/deer-flow) | Agent 框架 | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `skills/custom/` |
| [OpenCode](https://opencode.ai) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.opencode/skills/` |
| [OpenClaw](https://github.com/anthropics/openclaw) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `skills/` |
| [Qwen Code](https://tongyi.aliyun.com/lingma) (通义灵码) | IDE 插件 | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.qwen/skills/` |
| [Antigravity](https://github.com/anthropics/antigravity) | CLI | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.antigravity/skills/` |
| [Claw Code](https://github.com/ultraworkers/claw-code) | CLI (Rust) | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.claw/skills/` |
| [Qoder](https://qoder.com) (阿里 AI IDE) | IDE | `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` | `.qoder/skills/` + `.qoder/rules/` |

> 运行 `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh` 会自动检测你项目中使用的工具，将 20 个 skills 安装到正确位置。

### 翻译的 Skills（14 个）

| Skill | 用途 |
|-------|------|
| **头脑风暴** (brainstorming) | 需求分析 → 设计规格，不写代码先想清楚 |
| **编写计划** (writing-plans) | 把规格拆成可执行的实施步骤 |
| **执行计划** (executing-plans) | 按计划逐步实施，每步验证 |
| **测试驱动开发** (test-driven-development) | 严格 TDD：先写测试，再写代码 |
| **系统化调试** (systematic-debugging) | 四阶段调试法：定位→分析→假设→修复 |
| **请求代码审查** (requesting-code-review) | 派遣审查 agent 检查代码质量 |
| **接收代码审查** (receiving-code-review) | 技术严谨地处理审查反馈，拒绝敷衍 |
| **完成前验证** (verification-before-completion) | 证据先行——声称完成前必须跑验证 |
| **派遣并行 Agent** (dispatching-parallel-agents) | 多任务并发执行 |
| **子 Agent 驱动开发** (subagent-driven-development) | 每个任务一个 agent，两轮审查 |
| **Git Worktree 使用** (using-git-worktrees) | 实现前询问用户选择隔离 worktree 或当前分支开发 |
| **完成开发分支** (finishing-a-development-branch) | 合并/PR/保留/丢弃四选一 |
| **编写 Skills** (writing-skills) | 创建新 skill 的方法论 |
| **使用 Superpowers** (using-superpowers) | 元技能：如何调用和优先使用 skills |

### 🇨🇳 中国特色 Skills（6 个）

> ⚠️ **下表前 4 个 chinese-\* 为「手动调用」skill**——不会自动触发，需在对话中显式输入 `/chinese-xxx` 才会加载。
> 设计为参考资料而非工作流，避免污染上游 skill 的自动调度（如 `requesting-code-review`、`brainstorming` 等）。

| Skill | 用途 | 调用方式 | 上游有吗？ |
|-------|------|---------|:---:|
| **中文代码审查** (chinese-code-review) | 符合国内团队文化的代码审查规范 | `/chinese-code-review`（手动） | 无 |
| **中文 Git 工作流** (chinese-git-workflow) | 适配 Gitee/Coding/极狐 GitLab/CNB | `/chinese-git-workflow`（手动） | 无 |
| **中文技术文档** (chinese-documentation) | 中文排版规范、中英混排、告别机翻味 | `/chinese-documentation`（手动） | 无 |
| **中文提交规范** (chinese-commit-conventions) | 适配国内团队的 commit message 规范 | `/chinese-commit-conventions`（手动） | 无 |
| **MCP 服务器构建** (mcp-builder) | 构建生产级 MCP 工具，扩展 AI 能力边界 | 自动 | 无 |
| **工作流执行器** (workflow-runner) | 在 AI 工具内运行多角色 YAML 工作流 | 自动 | 无 |

---

## 快速开始

### 方式一：npm 安装（推荐）

```bash
cd /your/project
npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh
```

如果项目根目录已经配置 `.npmrc`：

```ini
registry=http://192.168.21.9:4873/
```

也可以简写为：

```bash
npx @tianma/superpowers-zh
```

> ⚠️ **不要在主目录（`~`）下跑**。v1.2.1 起会拒绝并提示，老版本会把 skills 和 `CLAUDE.md` 等 bootstrap 文件写到你的 home 目录，污染所有项目。如已误装见下文「卸载 / 误装清理」。

### 方式二：手动安装（low-fidelity，仅作备选）

> ⚠️ **手动 `cp -r skills` 是低保版安装，不等同于完整 plugin。**
>
> superpowers-zh 是一个完整 plugin，包含：`skills/`（20 个能力）+ `hooks/`（SessionStart 钩子，让 skill 在合适时机自动触发）+ `CLAUDE.md` / `GEMINI.md` 等 bootstrap 引导文件 + 4 套 plugin manifest（Claude Code / Cursor / Codex / Marketplace）。
>
> **下面的 `cp -r skills` 命令只复制 skills 目录**，不会自动配置 hooks、不会生成 bootstrap 引导。结果：skills 物理上存在，但 AI 不会在合适时机自动调用，需要你每次手动喊 "use brainstorming skill" 之类。
>
> **强烈推荐用方式一 `npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh`** —— 它会一键处理 skills 复制 + bootstrap 生成 + hooks 配置 + 工具特定适配。仅在 npx 不可用（极端无网络环境）时才退到手动。

```bash
# 克隆仓库
git clone https://github.com/jnMetaCode/superpowers-zh.git

# 复制 skills 到你的项目（选择你使用的工具）
cp -r superpowers-zh/skills /your/project/.claude/skills      # Claude Code / Copilot CLI
cp -r superpowers-zh/skills /your/project/.hermes/skills      # Hermes Agent
cp -r superpowers-zh/skills /your/project/.cursor/skills      # Cursor
cp -r superpowers-zh/skills /your/project/.codex/skills       # Codex CLI
cp -r superpowers-zh/skills /your/project/.kiro/steering      # Kiro
cp -r superpowers-zh/skills /your/project/skills/custom       # DeerFlow 2.0
cp -r superpowers-zh/skills /your/project/.trae/rules         # Trae
cp -r superpowers-zh/skills /your/project/.antigravity        # Antigravity
cp -r superpowers-zh/skills /your/project/.github/superpowers # VS Code (Copilot)
cp -r superpowers-zh/skills /your/project/skills              # OpenClaw
cp -r superpowers-zh/skills /your/project/.windsurf/skills   # Windsurf
cp -r superpowers-zh/skills /your/project/.gemini/skills     # Gemini CLI
cp -r superpowers-zh/skills /your/project/.aider/skills      # Aider
cp -r superpowers-zh/skills /your/project/.opencode/skills   # OpenCode
cp -r superpowers-zh/skills /your/project/.qwen/skills       # Qwen Code
cp -r superpowers-zh/skills /your/project/.claw/skills       # Claw Code（Rust 版）
cp -r superpowers-zh/skills /your/project/.qoder/skills      # Qoder（阿里 AI IDE）
```

### 方式三：在配置文件中引用

根据你使用的工具，在对应配置文件中引用 skills：

| 工具 | 配置文件 | 说明 |
|------|---------|------|
| Claude Code | `CLAUDE.md` | 项目根目录 |
| Copilot CLI | `CLAUDE.md` | 与 Claude Code 共用插件格式 |
| Hermes Agent | `HERMES.md` 或 `.hermes.md` | 项目根目录，安装时自动生成 |
| Kiro | `.kiro/steering/*.md` | 支持 always/globs/手动三种模式 |
| DeerFlow 2.0 | `skills/custom/*/SKILL.md` | 字节跳动开源 SuperAgent，自动发现自定义 skills |
| Trae | `.trae/rules/project_rules.md` | 项目级规则 |
| Antigravity | `GEMINI.md` 或 `AGENTS.md` | 项目根目录 |
| VS Code | `.github/copilot-instructions.md` | Copilot 自定义指令 |
| Cursor | `.cursor/rules/*.md` | 项目级规则目录 |
| OpenClaw | `skills/*/SKILL.md` | 工作区级 skills 目录，自动发现 |
| Windsurf | `.windsurf/skills/*/SKILL.md` | 项目级 skills 目录 |
| Gemini CLI | `.gemini/skills/*/SKILL.md` | 项目级 skills 目录 |
| Aider | `.aider/skills/*/SKILL.md` | 项目级 skills 目录 |
| OpenCode | `.opencode/skills/*/SKILL.md` | 项目级 skills 目录 |
| Hermes Agent | `.hermes/skills/*/SKILL.md` | 项目级 skills 目录 |
| Qwen Code | `.qwen/skills/*/SKILL.md` | 项目级 skills 目录 |
| Claw Code | `.claw/skills/*/SKILL.md` | Rust 版 CLI agent，兼容 Claude Code 的 SKILL.md 格式 |
| Qoder | `.qoder/skills/*/SKILL.md` + `.qoder/rules/superpowers-zh.md` | 阿里 AI IDE，自动生成 `trigger: always_on` 的 bootstrap rule |

> **详细安装指南**：[Kiro](docs/README.kiro.md) · [DeerFlow](docs/README.deerflow.md) · [Trae](docs/README.trae.md) · [Antigravity](docs/README.antigravity.md) · [VS Code](docs/README.vscode.md) · [Codex](docs/README.codex.md) · [OpenCode](docs/README.opencode.md) · [OpenClaw](docs/README.openclaw.md) · [Windsurf](docs/README.windsurf.md) · [Gemini CLI](docs/README.gemini-cli.md) · [Aider](docs/README.aider.md) · [Qwen Code](docs/README.qwen.md) · [Hermes Agent](docs/README.hermes.md) · [Qoder](docs/README.qoder.md)

### 卸载 / 误装清理（v1.2.1+）

```bash
cd /your/project          # 或 cd ~ 如果误装到了主目录
npx --registry http://192.168.21.9:4873/ @tianma/superpowers-zh@latest --uninstall
```

会做这些：

- 删除所有装过的 skill 目录（`.claude/skills/`、`.trae/skills/` 等）
- 删除独立 bootstrap 文件（`.trae/rules/superpowers-zh.md`、`.qoder/rules/superpowers-zh.md`、`.antigravity/rules.md`）
- 清理追加到 `CLAUDE.md` / `HERMES.md` / `GEMINI.md` / `CONVENTIONS.md` 里的 superpowers-zh 段，**保留你自己写的内容**

数据安全说明：v1.2.1 起，安装会把追加内容包在 `<!-- superpowers-zh:begin/end -->` 哨兵注释之间，卸载按哨兵精确切除。识别不可靠时跳过 + 警告，**绝不会误删用户内容**。

其他参数：

| 参数 | 用途 |
|---|---|
| `--tool <name>` | 自动检测不到时显式指定（cursor / trae / hermes / 等） |
| `--force` | 允许在主目录(~)安装（默认拒绝，**不建议**） |
| `--uninstall` | 卸载当前目录下的 superpowers-zh |
| `--help` / `--version` | 帮助 / 版本 |

---

## 致谢

- 原始英文版：[obra/superpowers](https://github.com/obra/superpowers)（MIT 协议）
- 感谢 [@obra](https://github.com/obra) 创建了这个优秀的项目

---

## 许可证

MIT License — 自由使用，商业或个人均可。

---