# Awesome Claude Code [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of awesome tools, MCPs, skills, workflows, and resources for Claude Code.
>
> 精选 Claude Code 相关工具、MCP 服务器、技巧、工作流与学习资源。

[Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) is Anthropic's official agentic coding CLI. This list focuses on community-built extensions, configurations, and guides that make Claude Code more powerful.

## Contents

- [Official Resources](#official-resources)
- [MCP Servers](#mcp-servers)
- [Skills & Slash Commands](#skills--slash-commands)
- [Hooks & Automation](#hooks--automation)
- [CLAUDE.md Templates](#claudemd-templates)
- [Prompting Guides](#prompting-guides)
- [Workflows](#workflows)
- [IDE Integrations](#ide-integrations)
- [Agent SDK](#agent-sdk)
- [Tools & Utilities](#tools--utilities)
- [Tutorials & Videos](#tutorials--videos)
- [Articles & Deep Dives / 中文深度文章](#articles--deep-dives--中文深度文章)
- [Community](#community)

---

## Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/overview) - Official docs covering setup, features, and configuration.
- [Claude Code Changelog](https://docs.anthropic.com/en/docs/claude-code/changelog) - Release notes and new feature announcements.
- [Model Context Protocol](https://modelcontextprotocol.io) - The open protocol powering Claude Code's MCP integrations.
- [MCP Official Servers](https://github.com/modelcontextprotocol/servers) - Reference MCP server implementations by Anthropic.
- [Claude Code Settings Reference](https://docs.anthropic.com/en/docs/claude-code/settings) - Full reference for `settings.json` configuration.
- [Claude Code Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks) - Automate actions triggered by Claude Code events.
- [Agent SDK Documentation](https://docs.anthropic.com/en/docs/claude-code/sdk) - Build custom subagents and multi-agent pipelines.

## MCP Servers

> MCP (Model Context Protocol) servers extend Claude Code with new tools and integrations.
> Add `--flat` initially; will be categorized once the list grows.

### Development

- [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) - Read/write local files with configurable access controls.
- [Git](https://github.com/modelcontextprotocol/servers/tree/main/src/git) - Run Git operations, view diffs, and browse commit history.
- [Playwright](https://github.com/microsoft/playwright-mcp) - Cross-browser automation by Microsoft.

### Data & Storage

- [PostgreSQL](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/postgres) - Read-only PostgreSQL database access.
- [SQLite](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/sqlite) - Query and inspect SQLite databases.
- [Supabase](https://github.com/supabase-community/supabase-mcp) - Full Supabase integration: database, auth, storage.

### Search & Knowledge

- [Brave Search](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/brave-search) - Web and local search via the Brave Search API.
- [Fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) - Fetch web content and convert it to Markdown.
- [Memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) - Persistent knowledge graph memory across sessions.
- [Context7](https://github.com/upstash/context7) - Always up-to-date library docs injected into context.

### Productivity & Collaboration

- [Slack](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/slack) - Read channels, send messages, manage Slack workspaces.
- [Google Drive](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/gdrive) - Search and read Google Drive files.
- [Linear](https://github.com/jerhadf/linear-mcp-server) - Manage Linear issues, projects, and cycles.
- [Figma](https://github.com/GLips/Figma-Context-MCP) - Read Figma designs, extract components and styles.

## Skills & Slash Commands

> Community-built skills (slash commands) that extend Claude Code's built-in capabilities.

- [Superpowers](https://github.com/anthropics/skills) - Official skill plugin system with brainstorming, TDD, debugging, and code review workflows. `(Official)`
- [TDD Workflow](https://docs.anthropic.com/en/docs/claude-code/skills) - Red-green-refactor cycle enforced via skill.
- [Systematic Debugging](https://docs.anthropic.com/en/docs/claude-code/skills) - Structured debugging flow: reproduce → isolate → fix → verify.
- [Code Review](https://docs.anthropic.com/en/docs/claude-code/skills) - Automated code review at configurable effort levels (low/medium/high/ultra).
- [Git Commit](https://docs.anthropic.com/en/docs/claude-code/skills) - Consistent commit messages following project conventions.

> **Contribute your skill:** Open a PR with your skill repo link and a one-line description.

## Hooks & Automation

> Hooks execute shell commands before/after Claude Code tool calls.

```jsonc
// .claude/settings.json — example hook configuration
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

**Hook recipes:**

- **Auto-format on edit** — Run Prettier/ESLint/gofmt after every file edit.
- **Test on save** — Trigger `npm test` after editing test files.
- **Token analytics** — Log tool call types to track usage patterns.
- **RTK proxy** — Route all shell commands through [RTK](#tools--utilities) for token savings.

## CLAUDE.md Templates

> `CLAUDE.md` files give Claude Code persistent project context. Place at repo root or `~/.claude/CLAUDE.md` for global config.

- **Web App (Next.js)** — Tech stack, testing conventions, env var rules, deploy instructions.
- **iOS App (Swift)** — Bundle ID, simulator launch commands, StoreKit testing notes, clean build reminders.
- **Python Backend** — Virtual env setup, migration commands, linting config.
- **Monorepo** — Per-package CLAUDE.md with shared root config.

**Key CLAUDE.md sections to include:**

```markdown
## Tech Stack        ← what you're building with
## Commands          ← build, test, lint, deploy commands
## Conventions       ← naming, file structure, patterns to follow
## Gotchas           ← known footguns, things Claude often gets wrong
## Off-limits        ← never auto-commit, never modify X file
```

## Prompting Guides

- **Be specific about scope** — "Edit only `src/auth.ts`" beats "fix the auth bug."
- **Give Claude the exit condition** — "Stop after writing tests, don't implement yet."
- **Use `CLAUDE.md` for invariants** — Don't repeat project rules in every prompt; put them in `CLAUDE.md`.
- **Decompose large tasks** — One PR's worth of work per session. Large tasks accumulate errors.
- **Reference files explicitly** — Claude reads what you point to; don't assume it found the right file.
- **Iterate in plan mode** — Use `/plan` for design-heavy tasks before touching code.

## Workflows

### Test-Driven Development (TDD)

1. Write failing test first.
2. Ask Claude to make it pass — minimal implementation only.
3. Refactor with tests green.
4. Repeat.

**Tip:** Use the `/tdd` skill to enforce this flow automatically.

### Systematic Debugging

1. Reproduce the bug with a failing test or repro script.
2. Add strategic `console.log` / breakpoints to isolate.
3. Fix the root cause (not the symptom).
4. Verify fix + check for regressions.

### Code Review Workflow

```bash
# Review current diff at medium effort
/code-review

# Deep multi-agent cloud review
/code-review ultra

# Post findings as inline PR comments
/code-review --comment
```

### Feature Branch Workflow

```bash
# Start a new feature
git checkout -b feature/my-feature

# Let Claude implement, then review
/code-review

# Verify before merging
/verify
```

## IDE Integrations

- **VS Code** — Install the [Claude Code extension](https://marketplace.visualstudio.com/items?itemName=Anthropic.claude-code) for in-editor access.
- **JetBrains** — Available via JetBrains Marketplace for IntelliJ, WebStorm, PyCharm, etc.
- **Neovim** — Community plugin: `claudecode.nvim` (see community links below).
- **Terminal** — Runs natively in any terminal. iTerm2 on macOS recommended for best experience.

## Agent SDK

> Build custom subagents and multi-agent pipelines with the Claude Code Agent SDK.

- [Agent SDK Docs](https://docs.anthropic.com/en/docs/claude-code/sdk) - Official SDK documentation.
- [Python Agent SDK](https://github.com/anthropics/claude-agent-sdk-python) - Python SDK for building agents.
- [TypeScript Agent SDK](https://github.com/anthropics/claude-agent-sdk-typescript) - TypeScript SDK for building agents.

**Use cases:**
- Parallel subagents for independent tasks (research + implementation simultaneously).
- Specialized agents per domain (frontend agent, backend agent, QA agent).
- Long-running autonomous loops with scheduled wakeups.

## Tools & Utilities

- [Agent Island](https://github.com/tristan666666/agent-island) — macOS notch companion for Claude/Codex sessions with live state display and auto-resume for selected long-running runs
- RTK (Rust Token Killer) — CLI proxy that filters verbose tool output before it reaches Claude, cutting token usage 60–90% on dev operations. *(Repo not yet public)* `(Community)`
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — Comprehensive list of MCP servers across all categories.
- [mcp.so](https://mcp.so) — MCP server registry and discovery.

## Tutorials & Videos

> ⚠️ Always check the publish date — Claude Code updates frequently.

- [Mastering Claude Code — Complete Visual Breakdown](https://www.youtube.com/watch?v=uFO9EAPINWo) — Community tutorial covering Claude Code concepts with visual breakdowns.
- [Building with MCP and the Claude API](https://www.youtube.com/watch?v=aZLr962R6Ag) — Anthropic team members discuss MCP origins and integration with Claude Code. `(Official)`

> **Contribute:** Know a great tutorial? Open a PR.

## Articles & Deep Dives / 中文深度文章

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

## Community

- [Anthropic Discord](https://discord.gg/anthropic) — Official server with a `#claude-code` channel.
- [r/ClaudeAI](https://reddit.com/r/ClaudeAI) — Community discussion, tips, and showcases.
- [Claude Code Twitter/X](https://x.com/AnthropicAI) — Follow for release announcements.

---

## Contributing

Contributions welcome! Please read the [contribution guidelines](CONTRIBUTING.md) first.

To add a resource:
1. Fork this repo.
2. Add your link in the appropriate section, alphabetically if possible.
3. Use this format: `- [Name](URL) — One-line description. Flags: \`(Official)\` \`(Chinese)\` \`(Paid)\``
4. Submit a PR.

**Quality bar:** Only add tools/resources you've personally used and found valuable.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
