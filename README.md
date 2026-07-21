# Awesome Claude Code [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

**English** | [简体中文](README.zh-CN.md)

> A curated list of awesome tools, MCPs, skills, workflows, and resources for Claude Code.

[Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview) is Anthropic's official agentic coding CLI. This list focuses on community-built extensions, configurations, and guides that make Claude Code more powerful.

## Contents

- [Official Resources](#official-resources)
- [MCP Servers](#mcp-servers)
- [Skills & Slash Commands](#skills--slash-commands)
- [Hooks & Automation](#hooks--automation)
- [CLAUDE.md Templates](#claudemd-templates)
- [DESIGN.md — Design Context for Agents](#designmd--design-context-for-agents)
- [Prompting Guides](#prompting-guides)
- [Workflows](#workflows)
- [IDE Integrations](#ide-integrations)
- [Agent SDK](#agent-sdk)
- [Tools & Utilities](#tools--utilities)
- [Tutorials & Videos](#tutorials--videos)
- [Articles & Deep Dives (Chinese)](#articles--deep-dives-chinese)
- [Community](#community)

---

## Official Resources

- [Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/overview) — Official docs covering setup, features, and configuration.
- [Claude Code Changelog](https://docs.anthropic.com/en/docs/claude-code/changelog) — Release notes and new feature announcements.
- [Model Context Protocol](https://modelcontextprotocol.io) — The open protocol powering Claude Code's MCP integrations.
- [MCP Official Servers](https://github.com/modelcontextprotocol/servers) — Reference MCP server implementations by Anthropic.
- [Claude Code Settings Reference](https://docs.anthropic.com/en/docs/claude-code/settings) — Full reference for `settings.json` configuration.
- [Claude Code Hooks](https://docs.anthropic.com/en/docs/claude-code/hooks) — Automate actions triggered by Claude Code events.
- [Agent SDK Documentation](https://docs.anthropic.com/en/docs/claude-code/sdk) — Build custom subagents and multi-agent pipelines.

## MCP Servers

> MCP (Model Context Protocol) servers extend Claude Code with new tools and integrations.

### Development

- [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem) — Read/write local files with configurable access controls.
- [Git](https://github.com/modelcontextprotocol/servers/tree/main/src/git) — Run Git operations, view diffs, and browse commit history.
- [Playwright](https://github.com/microsoft/playwright-mcp) — Cross-browser automation by Microsoft.

### Data & Storage

- [PostgreSQL](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/postgres) — Read-only PostgreSQL database access.
- [SQLite](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/sqlite) — Query and inspect SQLite databases.
- [Supabase](https://github.com/supabase-community/supabase-mcp) — Full Supabase integration: database, auth, storage.

### Search & Knowledge

- [Brave Search](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/brave-search) — Web and local search via the Brave Search API.
- [Fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) — Fetch web content and convert it to Markdown.
- [Memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) — Persistent knowledge graph memory across sessions.
- [Context7](https://github.com/upstash/context7) — Always up-to-date library docs injected into context.

### Productivity & Collaboration

- [Slack](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/slack) — Read channels, send messages, manage Slack workspaces.
- [Google Drive](https://github.com/modelcontextprotocol/servers-archived/tree/main/src/gdrive) — Search and read Google Drive files.
- [Linear](https://github.com/jerhadf/linear-mcp-server) — Manage Linear issues, projects, and cycles.
- [Figma](https://github.com/GLips/Figma-Context-MCP) — Read Figma designs, extract components and styles.

## Skills & Slash Commands

> Community-built skills (slash commands) that extend Claude Code's built-in capabilities.

- [Skills for Real Engineers](https://github.com/mattpocock/skills) — Matt Pocock's Claude Code skill collection; the `grill-me` skill interrogates you to align on intent before coding, alongside `to-spec`, `tdd`, `code-review`, and architecture skills. Install via `npx skills@latest add mattpocock/skills` or the plugin marketplace. `(Community)`
- [Superpowers](https://github.com/obra/superpowers) — Jesse Vincent's skills framework that runs AI coding through an engineering process: brainstorming, TDD, systematic debugging, plan writing, subagent-driven development, and code review. Installs via `/plugin install superpowers@claude-plugins-official`. `(Community)`
- [TDD Workflow](https://docs.anthropic.com/en/docs/claude-code/skills) — Red-green-refactor cycle enforced via skill.
- [Systematic Debugging](https://docs.anthropic.com/en/docs/claude-code/skills) — Structured debugging flow: reproduce → isolate → fix → verify.
- [Code Review](https://docs.anthropic.com/en/docs/claude-code/skills) — Automated code review at configurable effort levels (low/medium/high/ultra).
- [Git Commit](https://docs.anthropic.com/en/docs/claude-code/skills) — Consistent commit messages following project conventions.

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

## DESIGN.md — Design Context for Agents

> `DESIGN.md` is to a design system what `CLAUDE.md` is to project context: a structured file that gives coding agents a persistent understanding of a visual identity (colors, type, spacing, components, tone) — so the UI they generate matches your design system.

- [DESIGN.md Specification](https://github.com/google-labs-code/design.md) — The format spec by Google Labs: drop a `DESIGN.md` into your repo and agents build UI that follows your design system.
- [Vercel Geist (DESIGN.md)](https://vercel.com/design.md) — Vercel's Geist design system published in `DESIGN.md` format — a real-world reference to study or adapt. Dark theme variant: [design.dark.md](https://vercel.com/design.dark.md).
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — Curated collection of `DESIGN.md` files from popular brand design systems, ready to drop into a project.

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

- [Agent SDK Docs](https://docs.anthropic.com/en/docs/claude-code/sdk) — Official SDK documentation.
- [Python Agent SDK](https://github.com/anthropics/claude-agent-sdk-python) — Python SDK for building agents.
- [TypeScript Agent SDK](https://github.com/anthropics/claude-agent-sdk-typescript) — TypeScript SDK for building agents.

**Use cases:**
- Parallel subagents for independent tasks (research + implementation simultaneously).
- Specialized agents per domain (frontend agent, backend agent, QA agent).
- Long-running autonomous loops with scheduled wakeups.

## Tools & Utilities

- [Agent Island](https://github.com/tristan666666/agent-island) — macOS notch companion for Claude/Codex sessions with live state display and auto-resume for selected long-running runs.
- RTK (Rust Token Killer) — CLI proxy that filters verbose tool output before it reaches Claude, cutting token usage 60–90% on dev operations. *(Repo not yet public)* `(Community)`
- [ax](https://github.com/Necmttn/ax) — Local telemetry and recall graph for Claude Code sessions, tool calls, skills, and costs.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — Comprehensive list of MCP servers across all categories.
- [mcp.so](https://mcp.so) — MCP server registry and discovery.

## Tutorials & Videos

> ⚠️ Always check the publish date — Claude Code updates frequently.

- [Mastering Claude Code — Complete Visual Breakdown](https://www.youtube.com/watch?v=uFO9EAPINWo) — Community tutorial covering Claude Code concepts with visual breakdowns.
- [Building with MCP and the Claude API](https://www.youtube.com/watch?v=aZLr962R6Ag) — Anthropic team members discuss MCP origins and integration with Claude Code. `(Official)`

> **Contribute:** Know a great tutorial? Open a PR.

## Articles & Deep Dives (Chinese)

> In-depth Chinese-language articles on Claude Code, grouped by topic. Current source is [mufeng.blog](https://mufeng.blog); PRs adding other blogs are welcome. Titles are kept in the original Chinese.

### Getting Started / Overview

- [如果你还没用 Claude Code，可能已经落后一个时代](https://mufeng.blog/article/claude-code-is-the-most-underrated-ai-tool) — A beginner-oriented take on what Claude Code is and why it matters. `(Chinese)`
- [Claude Code 从 0 到 1 全攻略](https://mufeng.blog/article/how-ai-is-rebuilding-the-way-we-work-and-think) — Full onboarding flow from install to first real use. `(Chinese)`
- [Claude Code 使用洞察：第一个月 /insight 真实案例](https://mufeng.blog/article/claude-code-insights-report-and-ai-workflow-analysis) — Reviewing real usage data and collaboration patterns via `/insight`. `(Chinese)`

### CLAUDE.md & Permissions

- [CLAUDE.md 完全指南](https://mufeng.blog/article/claude-md-guide-for-claude-code-project-memory) — How to use CLAUDE.md to give a project persistent rules and context. `(Chinese)`
- [权限配置完全指南](https://mufeng.blog/article/claude-code-permissions-settings-guide) — Configuring allow/deny permissions in `settings.json`. `(Chinese)`
- [权限模式完全指南：Auto / Bypass / Ask](https://mufeng.blog/article/claude-code-permission-modes) — Differences and use cases of the three permission modes. `(Chinese)`
- [文件过滤完全指南：.claudeignore 到 permissions.deny](https://mufeng.blog/article/claude-code-claudeignore-file-filtering-guide) — Mechanisms for controlling which files Claude can access. `(Chinese)`

### Skills & Workflows

- [Claude Skill 官方指南](https://mufeng.blog/article/anthropic-claude-skill-guide-and-best-practices) — The official approach to distilling prompts into reusable Skills. `(Chinese)`
- [Claude Code Skills 深度解析：SKILL.md 结构](https://mufeng.blog/article/claude-code-skills-guide-skill-md-structure) — Breaking down the structure and authoring of SKILL.md. `(Chinese)`
- [Superpowers：让 Claude Code 和 Codex 按工程流程开发](https://mufeng.blog/article/superpowers-skill-claude-codex-workflow) — Using the Superpowers plugin to run AI coding through a disciplined process. `(Chinese)`
- [Claude Code + Obsidian + NotebookLM 研究系统](https://mufeng.blog/article/claude-code-obsidian-notebooklm-ai-research-system) — Combining the three into a self-iterating AI research workflow. `(Chinese)`

### Internals & Architecture

- [Claude Code 源码泄露：架构深度解构](https://mufeng.blog/article/claude-code-source-code-leaked) — Analyzing Claude Code's overall architecture from leaked source. `(Chinese)`
- [Claude Code 深度解析：从终端 Agent 到一人工程团队](https://mufeng.blog/article/claude-code-deep-dive) — How it lets one person run a full engineering process. `(Chinese)`
- [你的 AI Agent 跑不好，根本不是模型的问题](https://mufeng.blog/article/harness-engineering-ai-agent) — Why agent performance is decided by harness engineering, not just the model. `(Chinese)`

### Tips & Tools

- [Claude Code 常用快捷键](https://mufeng.blog/article/claude-code-shortcuts-and-terminal-workflow-guide) — Common in-terminal shortcuts and operation flow. `(Chinese)`
- [Claude Code Token 消耗太高？RTK 帮你省下 9 成](https://mufeng.blog/article/claude-code-token-rtk-89-percent) — Cutting token usage by filtering tool output through the RTK proxy. `(Chinese)`

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
