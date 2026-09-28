# Changelog

> 本仓库每周更新一次。最新更新在最上方。
> 想只看增量内容，看这里即可。

---

## 2026-W39 (截至 2026-09-27)

### 新增
- [Skills & Slash Commands] [App Store ASO](https://github.com/TimBroddin/skills/tree/main/skills/app-store-aso) — Tim Broddin 的 Apple App Store 元数据技能，按 Apple 字符上限校验名称 / 副标题 / 关键词等，含截图文案策略。原独立仓库 `TimBroddin/app-store-aso-skill` 已标注 Moved，链接指向合并后的 `TimBroddin/skills`。MIT。
- [Skills & Slash Commands] [ASO Skills](https://github.com/appeeky/aso-skills) — Appeeky 的 30+ 个 ASO 与 App 营销技能，`/aso-router` 统一入口，实时数据依赖 Appeeky API（部分技能需付费套餐）。2.1k star。安装命令仍用旧路径 `eronred/aso-skills`（GitHub 重定向到 `appeeky/aso-skills`）。
- [Tools & Utilities] [OpenSEO](https://github.com/every-app/open-seo) — 开源 Semrush / Ahrefs 替代品，自带 MCP 服务器与 Agent Skills，支持 Claude Code；BYOK DataForSEO 按量付费。21k star。

---

## 2026-W38 (截至 2026-09-20)

### 新增
- [Skills & Slash Commands] [ASC CLI Skills](https://github.com/rorkai/app-store-connect-cli-skills) — 25 个围绕 `asc`（App Store Connect CLI）的 Agent Skills，覆盖构建、TestFlight、元数据、提审、签名、截图与 Apple Ads；仓库同时是 Claude Code 插件市场（`asc@rorkai`）。MIT，1k star。`asc` 二进制需单独装，其 go.mod module path 仍是 `github.com/rudrankriyam/App-Store-Connect-CLI`。

---

## 2026-W36 (截至 2026-09-06)

### 新增
- [Skills & Slash Commands] [Anything → NotebookLM](https://github.com/joeseesun/qiaomu-anything-to-notebooklm) — Claude Code 技能，把公众号文章、X 长推、YouTube、播客、PDF/EPUB/Office 文件等 15+ 种来源导入 NotebookLM，生成播客 / PPT 大纲 / 思维导图 / Quiz。MIT，5.9k star。
- [Tools & Utilities] [OpenDesign](https://github.com/nexu-io/open-design) — 本地优先的开源设计桌面应用，通过 BYOK 把 Claude Code 等 20+ 个 Agent CLI 当作设计引擎，产出 HTML/PDF/PPTX/MP4 真实文件。Apache-2.0。
- [Tools & Utilities] [Skills Manager](https://github.com/xingkongliang/skills-manager) — 技能管理桌面应用，解决「技能从哪加载、全局/项目里埋了多少、上游更新不同步」三个问题，支持 50+ 编码工具。MIT，Rust。

---

## 2026-W35 (截至 2026-08-30)

### 新增
- [Skills & Slash Commands] [ELI5](https://github.com/anthropics/claude-plugins-community/tree/main/eli5) — Anthropic 员工 Thariq Shihipar 开发的技能，`/eli5 <主题>` 生成图多字少的 HTML 讲解页，已开源到社区插件市场（非 claude-plugins-official 官方市场）。

---

## 2026-W34 (截至 2026-08-23)

### 新增
- [Skills 与斜杠命令] [suede-creator-skills](https://github.com/JasonColapietro/suede-creator-skills) — 面向 Claude Code 与 Codex 的开源 Agent Skills 合集，覆盖代码质量、AI 评测、设计、增长与应用发布工作流。

---

## 2026-W33 (截至 2026-08-16)

### 新增
- [Skills & Slash Commands] [Agent Skills](https://github.com/addyosmani/agent-skills) — Addy Osmani 的工程技能集，24 个按生命周期阶段组织的生产级技能，MIT 协议，实测 87,910 star。

---

## 2026-W32 (截至 2026-08-09)

> 补更：W31 断更一周，本次合并处理。本周主题是「补可信度」而非扩容——把 README 里违反自身 quality bar（每条必须有可点击有效链接、不收凑数条目）的地方清掉。

### 新增
- [Official Resources] [Claude Plugins Directory](https://github.com/anthropics/claude-plugins-official) — Anthropic 官方维护的插件目录。Superpowers 条目里早就写了 `/plugin install superpowers@claude-plugins-official`，但一直没链接到市场本身，补上。
- [IDE Integrations] [claudecode.nvim](https://github.com/coder/claudecode.nvim) — Coder 出品的 Neovim 插件。原文写「社区插件 `claudecode.nvim`（见下方社区链接）」，但下方并不存在该链接，属于悬空引用，现补实。

### 更新 / 修正
- **RTK 条目补上仓库链接**：原条目标注「仓库尚未公开」，实际已开源在 [rtk-ai/rtk](https://github.com/rtk-ai/rtk)（Apache-2.0）。核实依据：该仓库 README 的 logo alt text 为 "RTK - Rust Token Killer"，`rtk gain` / `rtk discover` / `rtk proxy` 命令与本地在用版本一致，并同样带有与 crates.io 上另一个 "rtk"（Rust Type Kit）的重名警告。
- **删除 Skills 分区 4 条凑数条目**（TDD Workflow / Systematic Debugging / Code Review / Git Commit）：4 条全部指向同一个通用文档页 `docs/claude-code/skills`，既非独立资源也无独立链接。改为一句说明，指明本分区只收录可安装的社区技能集，自带技能与 `SKILL.md` 写法见官方文档。
- **「CLAUDE.md Templates」改名为「CLAUDE.md Essentials / CLAUDE.md 写法要点」**：原分区 4 条「模板」无任何链接，形式上伪装成收录条目，实为写法说明。改名并显式声明是写法指南、无物可装；目录锚点同步更新。
- **5 个 MCP 条目标注停止维护**（PostgreSQL / SQLite / Brave Search / Slack / Google Drive）：均位于 `modelcontextprotocol/servers-archived`，该仓库 GitHub 状态为 archived、自述「Reference MCP servers that are no longer maintained」、最后 push 停在 2025-05-28。链接仍可访问，故保留条目但明确标注仅作参考实现。
- **全量链接校验**：README 中 61 个 URL 逐个 curl 跟随重定向，60 个返回 200；唯一非 200 是 `reddit.com/r/ClaudeAI` 的 403（反爬拦截，浏览器正常访问），判定为有效，不作处理。本周无失效链接。

### 本周学习随记
- awesome-list 腐坏不是从死链开始的，是从「无链接的条目」开始的——死链至少能被脚本查出来，凑数条目只能靠人肉复查。以后新增时先问一句：这条有独立的、可点击的、指向它自己的链接吗？没有就不该长成条目的样子。

---

## 2026-W30 (截至 2026-07-21)

### 更新 / 修正
- Vercel Geist 条目补充深色主题文件地址 [design.dark.md](https://vercel.com/design.dark.md)：与 `/design.md` 同一套 token 名，只是深色取值，文档内自述「This is the Dark theme. The Light theme uses the same token names with different values and lives at `/design.md`」。因属同一设计系统的两个主题文件，并入现有条目而非新开一行。

---

## 2026-W29 (截至 2026-07-14)

### 新增
- 新增分区「DESIGN.md — Design Context for Agents」，收录 DESIGN.md（给编码 Agent 的持久化设计上下文）相关的 3 条资源：
  - [DESIGN.md Specification](https://github.com/google-labs-code/design.md) — Google Labs 的格式规范本身。
  - [Vercel Geist (DESIGN.md)](https://vercel.com/design.md) — Vercel Geist 设计系统的真实范例。
  - [awesome-design-md](https://github.com/VoltAgent/awesome-design-md) — 各品牌 DESIGN.md 合集清单。

- Skills & Slash Commands 分区新增 2 个开源技能集：
  - [Skills for Real Engineers](https://github.com/mattpocock/skills) — Matt Pocock 出品，代表技能 `grill-me`（编码前反复追问对齐需求），另含 to-spec / tdd / code-review 等。`(Community)`
  - [Superpowers](https://github.com/obra/superpowers) — Jesse Vincent 出品，把 AI 编程纳入工程流程（brainstorming、TDD、系统化调试、写计划、子代理开发、代码审查）。`(Community)`

### 更新 / 修正
- 语言拆分：README 从单页双语混排改为「双文件 + 顶部互链」——`README.md`（纯英文）与 `README.zh-CN.md`（纯中文），两份顶部各放 `English | 简体中文` 切换链接。GitHub README 不执行 JS，无法做原地页签，双文件互链是可用的等效方案。
- 修正 Superpowers 条目：原链接误指向 `anthropics/skills` 并标注 `(Official)`，实际为 Jesse Vincent（obra）的社区项目，已改为正确仓库 `obra/superpowers` 并改标 `(Community)`。
- 关闭 PR #7（OpenAgentRelay）：作者自荐、仓库当天新建、0 star、Alpha 阶段，暂不符合收录标准；已记入 `INBOX.md` 待查观察。

### 本周学习随记
- DESIGN.md 是 CLAUDE.md 的「设计版」——把设计系统写成 Agent 可读的持久化上下文，正在成为独立的资源品类。

---

## 2026-W25 (截至 2026-06-21)

### 新增
- 新增分区「Articles & Deep Dives / 中文深度文章」，按主题归类收录 mufeng.blog 的 16 篇 Claude Code 深度文章（入门 / CLAUDE.md & 权限 / Skills & 工作流 / 源码与架构 / 技巧 & 工具）。`(Chinese)`

### 更新 / 修正
- 新增运营 SOP（`OPERATIONS.md`）、暂存区（`INBOX.md`）、收录规范（`CLAUDE.md`）。
- 建立每周更新节奏：每周日 21:00 前完成并 push。
- 修正 RTK 文章链接（去掉 URL 前多余的空格转义 `%20%20`）。
- INBOX 中 mufeng.blog 系列文章去重精简：合并主题重叠项（Superpowers、/insight、源码泄露各保留其一），剔除弱相关项（RSS、Mac 定时关机、zshrc 配置等）。

### 本周学习随记
- 把「记录 Claude Code 学习」沉淀成 awesome-list，关键在固定周更节奏 + 只收录亲自用过的资源。

---

<!--
新增条目模板，复制到最上方使用：

## YYYY-WXX (截至 YYYY-MM-DD)

### 新增
- [分区] [Name](url) — 一句话描述。`(标记)`

### 更新 / 修正
- 修正失效链接 / 移除过期内容：xxx

### 本周学习随记
- 一句话本周最大的收获。
-->
