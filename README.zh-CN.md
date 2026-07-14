# Awesome Claude Code [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) | **简体中文**

> 精选 Claude Code 相关工具、MCP 服务器、技巧、工作流与学习资源。

[Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) 是 Anthropic 官方的 Agent 编码 CLI。本清单聚焦社区构建的扩展、配置与指南，让 Claude Code 更强大。

## 目录

- [官方资源](#官方资源)
- [MCP 服务器](#mcp-服务器)
- [Skills 与斜杠命令](#skills-与斜杠命令)
- [Hooks 与自动化](#hooks-与自动化)
- [CLAUDE.md 模板](#claudemd-模板)
- [DESIGN.md — 给 Agent 的设计上下文](#designmd--给-agent-的设计上下文)
- [提示词指南](#提示词指南)
- [工作流](#工作流)
- [IDE 集成](#ide-集成)
- [Agent SDK](#agent-sdk)
- [工具与实用程序](#工具与实用程序)
- [教程与视频](#教程与视频)
- [中文深度文章](#中文深度文章)
- [社区](#社区)

---

## 官方资源

- [Claude Code 文档](https://docs.anthropic.com/en/docs/claude-code/overview) — 官方文档，涵盖安装、功能与配置。
- [Claude Code 更新日志](https://docs.anthropic.com/en/docs/claude-code/changelog) — 版本发布说明与新功能公告。
- [Model Context Protocol](https://modelcontextprotocol.io) — 支撑 Claude Code MCP 集成的开放协议。
- [MCP 官方服务器](https://github.com/modelcontextprotocol/servers) — Anthropic 提供的参考 MCP 服务器实现。
- [Claude Code 设置参考](https://docs.anthropic.com/en/docs/claude-code/settings) — `settings.json` 配置的完整参考。
- [Claude Code Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks) — 由 Claude Code 事件触发、自动执行动作。
- [Agent SDK 文档](https://docs.anthropic.com/en/docs/claude-code/sdk) — 构建自定义子代理与多代理流水线。

## MCP 服务器

> MCP（Model Context Protocol）服务器为 Claude Code 扩展新的工具与集成。

### 开发

- [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) — 读写本地文件，可配置访问控制。
- [Git](https://github.com/modelcontextprotocol/servers/tree/main/src/git) — 执行 Git 操作、查看 diff、浏览提交历史。
- [Playwright](https://github.com/microsoft/playwright-mcp) — 微软出品的跨浏览器自动化。

### 数据与存储

- [PostgreSQL](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/postgres) — 只读访问 PostgreSQL 数据库。
- [SQLite](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/sqlite) — 查询与检视 SQLite 数据库。
- [Supabase](https://github.com/supabase-community/supabase-mcp) — 完整 Supabase 集成：数据库、认证、存储。

### 搜索与知识

- [Brave Search](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/brave-search) — 通过 Brave Search API 进行网络与本地搜索。
- [Fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) — 抓取网页内容并转为 Markdown。
- [Memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) — 跨会话持久化的知识图谱记忆。
- [Context7](https://github.com/upstash/context7) — 将始终最新的库文档注入上下文。

### 生产力与协作

- [Slack](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/slack) — 读取频道、发送消息、管理 Slack 工作区。
- [Google Drive](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/gdrive) — 搜索与读取 Google Drive 文件。
- [Linear](https://github.com/jerhadf/linear-mcp-server) — 管理 Linear 的 issue、项目与迭代。
- [Figma](https://github.com/GLips/Figma-Context-MCP) — 读取 Figma 设计，提取组件与样式。

## Skills 与斜杠命令

> 社区构建的 Skills（斜杠命令），扩展 Claude Code 的内置能力。

- [Skills for Real Engineers](https://github.com/mattpocock/skills) — Matt Pocock 的 Claude Code 技能集；`grill-me` 会在编码前反复追问、把 Agent 对齐到你的真实意图，另含 `to-spec`、`tdd`、`code-review` 与架构类技能。可用 `npx skills@latest add mattpocock/skills` 或插件市场安装。 `(Community)`
- [Superpowers](https://github.com/obra/superpowers) — Jesse Vincent 的技能框架，把 AI 编程纳入工程流程：brainstorming、TDD、系统化调试、写计划、子代理开发、代码审查。通过 `/plugin install superpowers@claude-plugins-official` 安装。 `(Community)`
- [TDD Workflow](https://docs.anthropic.com/en/docs/claude-code/skills) — 以技能强制执行 red-green-refactor 循环。
- [Systematic Debugging](https://docs.anthropic.com/en/docs/claude-code/skills) — 结构化调试流程：复现 → 隔离 → 修复 → 验证。
- [Code Review](https://docs.anthropic.com/en/docs/claude-code/skills) — 可配置力度（low/medium/high/ultra）的自动代码审查。
- [Git Commit](https://docs.anthropic.com/en/docs/claude-code/skills) — 遵循项目规范的一致提交信息。

> **贡献你的技能：** 提一个 PR，附上技能仓库链接与一句话描述。

## Hooks 与自动化

> Hooks 在 Claude Code 工具调用前后执行 shell 命令。

```jsonc
// .claude/settings.json — hook 配置示例
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [{ "type": "command", "command": "echo 'Running bash command'" }]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Edit",
        "hooks": [{ "type": "command", "command": "prettier --write $CLAUDE_FILE_PATH" }]
      }
    ]
  }
}
```

**Hook 妙用：**

- **编辑后自动格式化** — 每次改文件后跑 Prettier/ESLint/gofmt。
- **保存即测试** — 编辑测试文件后触发 `npm test`。
- **Token 分析** — 记录工具调用类型以追踪使用模式。
- **RTK 代理** — 把所有 shell 命令经 [RTK](#工具与实用程序) 路由以节省 token。

## CLAUDE.md 模板

> `CLAUDE.md` 为 Claude Code 提供持久化的项目上下文。放在仓库根目录，或放 `~/.claude/CLAUDE.md` 作为全局配置。

- **Web 应用（Next.js）** — 技术栈、测试规范、环境变量规则、部署说明。
- **iOS 应用（Swift）** — Bundle ID、模拟器启动命令、StoreKit 测试注意事项、clean build 提醒。
- **Python 后端** — 虚拟环境配置、迁移命令、lint 配置。
- **Monorepo** — 每个包一份 CLAUDE.md，配合共享的根配置。

**CLAUDE.md 值得包含的关键区块：**

```markdown
## Tech Stack        ← 你在用什么构建
## Commands          ← 构建、测试、lint、部署命令
## Conventions       ← 命名、文件结构、要遵循的模式
## Gotchas           ← 已知坑点、Claude 常出错的地方
## Off-limits        ← 绝不自动 commit、绝不修改某文件
```

## DESIGN.md — 给 Agent 的设计上下文

> `DESIGN.md` 之于设计系统，如同 `CLAUDE.md` 之于项目上下文：一份结构化文件，给编码 Agent 提供持久化的视觉规范（配色、字体、间距、组件、语气），让它生成的 UI 与你的设计系统一致。

- [DESIGN.md Specification](https://github.com/google-labs-code/design.md) — Google Labs 的格式规范：把 `DESIGN.md` 放进仓库，Agent 就按你的设计系统构建 UI。
- [Vercel Geist (DESIGN.md)](https://vercel.com/design.md) — Vercel Geist 设计系统以 `DESIGN.md` 格式发布——可学习或改用的真实范例。
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — 各知名品牌设计系统的 `DESIGN.md` 合集，可直接放进项目。

## 提示词指南

- **明确范围** — “只改 `src/auth.ts`” 胜过 “修一下 auth 的 bug”。
- **给出退出条件** — “写完测试就停，先别实现”。
- **用 `CLAUDE.md` 承载不变量** — 项目规则别在每个提示里重复，写进 `CLAUDE.md`。
- **拆分大任务** — 一次会话做一个 PR 的量。大任务会累积错误。
- **显式引用文件** — Claude 只读你指到的地方，别假设它找对了文件。
- **在 plan 模式迭代** — 设计密集型任务先用 `/plan` 再动代码。

## 工作流

### 测试驱动开发（TDD）

1. 先写会失败的测试。
2. 让 Claude 让它通过——只做最小实现。
3. 测试绿灯后重构。
4. 重复。

**提示：** 用 `/tdd` 技能自动强制该流程。

### 系统化调试

1. 用失败的测试或复现脚本复现 bug。
2. 加关键 `console.log` / 断点以隔离问题。
3. 修根因（不是修表象）。
4. 验证修复 + 检查回归。

### 代码审查工作流

```bash
# 以中等力度审查当前 diff
/code-review

# 深度多代理云端审查
/code-review ultra

# 将结果作为行内 PR 评论发布
/code-review --comment
```

### 功能分支工作流

```bash
# 开一个新功能
git checkout -b feature/my-feature

# 让 Claude 实现，然后审查
/code-review

# 合并前验证
/verify
```

## IDE 集成

- **VS Code** — 安装 [Claude Code 扩展](https://marketplace.visualstudio.com/items?itemName=Anthropic.claude-code) 以在编辑器内使用。
- **JetBrains** — 通过 JetBrains Marketplace 支持 IntelliJ、WebStorm、PyCharm 等。
- **Neovim** — 社区插件 `claudecode.nvim`（见下方社区链接）。
- **终端** — 在任意终端原生运行。macOS 上推荐 iTerm2 以获得最佳体验。

## Agent SDK

> 用 Claude Code Agent SDK 构建自定义子代理与多代理流水线。

- [Agent SDK 文档](https://docs.anthropic.com/en/docs/claude-code/sdk) — 官方 SDK 文档。
- [Python Agent SDK](https://github.com/anthropics/claude-agent-sdk-python) — 构建 Agent 的 Python SDK。
- [TypeScript Agent SDK](https://github.com/anthropics/claude-agent-sdk-typescript) — 构建 Agent 的 TypeScript SDK。

**使用场景：**
- 并行子代理处理独立任务（同时做调研 + 实现）。
- 按领域划分的专职代理（前端代理、后端代理、QA 代理）。
- 带定时唤醒的长时自主循环。

## 工具与实用程序

- [Agent Island](https://github.com/tristan666666/agent-island) — macOS 刘海伴侣，展示 Claude/Codex 会话实时状态，并对选定的长任务自动续跑。
- RTK（Rust Token Killer） — CLI 代理，在冗长工具输出抵达 Claude 前先过滤，开发操作省 60–90% token。*（仓库尚未公开）* `(Community)`
- [ax](https://github.com/Necmttn/ax) — Claude Code 会话、工具调用、技能与成本的本地遥测与回溯图谱。
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — 覆盖各类别的 MCP 服务器综合清单。
- [mcp.so](https://mcp.so) — MCP 服务器注册与发现平台。

## 教程与视频

> ⚠️ 务必查看发布日期——Claude Code 更新很快。

- [Mastering Claude Code — Complete Visual Breakdown](https://www.youtube.com/watch?v=uFO9EAPINWo) — 社区教程，用可视化方式讲解 Claude Code 概念。
- [Building with MCP and the Claude API](https://www.youtube.com/watch?v=aZLr962R6Ag) — Anthropic 团队讨论 MCP 由来及其与 Claude Code 的集成。 `(Official)`

> **贡献：** 知道好教程？提个 PR。

## 中文深度文章

> 中文社区里值得一读的 Claude Code 深度文章，按主题归类。目前来源为 [mufeng.blog](https://mufeng.blog)，欢迎 PR 补充其他博客。

### 入门 / 概览

- [如果你还没用 Claude Code，可能已经落后一个时代](https://mufeng.blog/article/claude-code-is-the-most-underrated-ai-tool) — 面向新手的 Claude Code 价值与定位介绍。 `(Chinese)`
- [Claude Code 从 0 到 1 全攻略](https://mufeng.blog/article/how-ai-is-rebuilding-the-way-we-work-and-think) — 从安装到上手的完整入门流程。 `(Chinese)`
- [Claude Code 使用洞察：第一个月 /insight 真实案例](https://mufeng.blog/article/claude-code-insights-report-and-ai-workflow-analysis) — 用 /insight 复盘真实使用数据与协作模式。 `(Chinese)`

### CLAUDE.md & 权限配置

- [CLAUDE.md 完全指南](https://mufeng.blog/article/claude-md-guide-for-claude-code-project-memory) — 如何用 CLAUDE.md 给项目设定持久规则与上下文。 `(Chinese)`
- [权限配置完全指南](https://mufeng.blog/article/claude-code-permissions-settings-guide) — settings.json 中 allow/deny 权限的配置方法。 `(Chinese)`
- [权限模式完全指南：Auto / Bypass / Ask](https://mufeng.blog/article/claude-code-permission-modes) — 三种权限模式的区别与适用场景。 `(Chinese)`
- [文件过滤完全指南：.claudeignore 到 permissions.deny](https://mufeng.blog/article/claude-code-claudeignore-file-filtering-guide) — 控制 Claude 可访问文件范围的几种机制。 `(Chinese)`

### Skills & 工作流

- [Claude Skill 官方指南](https://mufeng.blog/article/anthropic-claude-skill-guide-and-best-practices) — 把提示词沉淀为可复用 Skill 的官方做法。 `(Chinese)`
- [Claude Code Skills 深度解析：SKILL.md 结构](https://mufeng.blog/article/claude-code-skills-guide-skill-md-structure) — 拆解 SKILL.md 的结构与编写要点。 `(Chinese)`
- [Superpowers：让 Claude Code 和 Codex 按工程流程开发](https://mufeng.blog/article/superpowers-skill-claude-codex-workflow) — 用 Superpowers 插件把 AI 编程纳入规范流程。 `(Chinese)`
- [Claude Code + Obsidian + NotebookLM 研究系统](https://mufeng.blog/article/claude-code-obsidian-notebooklm-ai-research-system) — 三者组合搭建可自我迭代的 AI 研究工作流。 `(Chinese)`

### 源码与架构

- [Claude Code 源码泄露：架构深度解构](https://mufeng.blog/article/claude-code-source-code-leaked) — 从泄露源码分析 Claude Code 的整体架构。 `(Chinese)`
- [Claude Code 深度解析：从终端 Agent 到一人工程团队](https://mufeng.blog/article/claude-code-deep-dive) — 解析其如何支撑单人完成完整工程流程。 `(Chinese)`
- [你的 AI Agent 跑不好，根本不是模型的问题](https://mufeng.blog/article/harness-engineering-ai-agent) — 从 harness 工程角度分析 Agent 表现的决定因素。 `(Chinese)`

### 技巧 & 工具

- [Claude Code 常用快捷键](https://mufeng.blog/article/claude-code-shortcuts-and-terminal-workflow-guide) — 终端内常用快捷键与操作流。 `(Chinese)`
- [Claude Code Token 消耗太高？RTK 帮你省下 9 成](https://mufeng.blog/article/claude-code-token-rtk-89-percent) — 用 RTK 代理过滤工具输出、降低 token 消耗。 `(Chinese)`

## 社区

- [Anthropic Discord](https://discord.gg/anthropic) — 官方服务器，含 `#claude-code` 频道。
- [r/ClaudeAI](https://reddit.com/r/ClaudeAI) — 社区讨论、技巧与展示。
- [Claude Code Twitter/X](https://x.com/AnthropicAI) — 关注发布公告。

---

## 贡献

欢迎贡献！请先阅读[贡献指南](CONTRIBUTING.md)。

添加资源：
1. Fork 本仓库。
2. 在合适的分区添加链接，尽量按字母序。
3. 使用此格式：`- [Name](URL) — 一句话描述。标记：\`(Official)\` \`(Chinese)\` \`(Paid)\``
4. 提交 PR。

**质量线：** 只添加你亲自用过且觉得有价值的工具/资源。

---

## 许可

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
