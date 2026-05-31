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

- [PostgreSQL](https://github.com/modelcontextprotocol/servers/tree/main/src/postgres) - Read-only PostgreSQL database access.
- [SQLite](https://github.com/modelcontextprotocol/servers/tree/main/src/sqlite) - Query and inspect SQLite databases.
- [Supabase](https://github.com/supabase-community/supabase-mcp) - Full Supabase integration: database, auth, storage.

### Search & Knowledge

- [Brave Search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) - Web and local search via the Brave Search API.
- [Fetch](https://github.com/modelcontextprotocol/servers/tree/main/src/fetch) - Fetch web content and convert it to Markdown.
- [Memory](https://github.com/modelcontextprotocol/servers/tree/main/src/memory) - Persistent knowledge graph memory across sessions.
- [Context7](https://github.com/upstash/context7) - Always up-to-date library docs injected into context.

### Productivity & Collaboration

- [Slack](https://github.com/modelcontextprotocol/servers/tree/main/src/slack) - Read channels, send messages, manage Slack workspaces.
- [Google Drive](https://github.com/modelcontextprotocol/servers/tree/main/src/gdrive) - Search and read Google Drive files.
- [Linear](https://github.com/linear/linear-mcp-server) - Manage Linear issues, projects, and cycles.
- [Figma](https://github.com/figma/figma-mcp) - Read Figma designs, extract components and styles.

## Skills & Slash Commands

> Community-built skills (slash commands) that extend Claude Code's built-in capabilities.

- [Superpowers](https://github.com/anthropics/claude-code-skills) - Official skill plugin system with brainstorming, TDD, debugging, and code review workflows. `(Official)`
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
- [Python Agent SDK](https://github.com/anthropics/claude-code-sdk-python) - Python SDK for building agents.
- [TypeScript Agent SDK](https://github.com/anthropics/claude-code-sdk-typescript) - TypeScript SDK for building agents.

**Use cases:**
- Parallel subagents for independent tasks (research + implementation simultaneously).
- Specialized agents per domain (frontend agent, backend agent, QA agent).
- Long-running autonomous loops with scheduled wakeups.

## Tools & Utilities

- [RTK (Rust Token Killer)](https://github.com/changyou0730/rtk) — CLI proxy that filters verbose tool output before it reaches Claude, cutting token usage 60–90% on dev operations. `(Community)`
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) — Comprehensive list of MCP servers across all categories.
- [mcp.so](https://mcp.so) — MCP server registry and discovery.

## Tutorials & Videos

> ⚠️ Always check the publish date — Claude Code updates frequently.

- [Claude Code Overview](https://www.youtube.com/watch?v=PLACEHOLDER) — Official intro from Anthropic. `(TODO: replace with real link)`
- [Building with MCP](https://www.youtube.com/watch?v=PLACEHOLDER) — How to add MCP servers to your workflow. `(TODO: replace with real link)`

> **Contribute:** Know a great tutorial? Open a PR.

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
