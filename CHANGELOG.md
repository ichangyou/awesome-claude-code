# Changelog

> 本仓库每周更新一次。最新更新在最上方。
> 想只看增量内容，看这里即可。

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
