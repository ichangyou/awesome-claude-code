# CLAUDE.md — Awesome Claude Code 仓库维护规则

本仓库是一份精选 Claude Code 资源清单（awesome-list），双语（English / 中文）。
本文件用于让 Claude 在协助维护时自动遵守收录格式与分区规则。

## 项目性质

- 这是一份 awesome-list，主清单是双语双文件：`README.md`（英文）与 `README.zh-CN.md`（中文），两份内容平行、顶部互链切换。
- 核心属性：「记录 Claude Code 学习」，每周更新一次。
- 运营流程见 `OPERATIONS.md`；周中暂存见 `INBOX.md`；更新记录见 `CHANGELOG.md`。

## 收录格式（强制）

每条收录使用统一格式：

```
- [Name](URL) — One-line description. `(标记)`
```

规则：
- 破折号用 ` — `（em dash，前后各一个空格）。
- 描述一句话讲清「它是什么 / 解决什么」，不堆形容词。
- 分区内尽量**按字母序**排列。
- 标记可选，取值：`(Official)` `(Chinese)` `(Paid)` `(Community)`。可叠加。

## 分区（README 现有结构，新增条目归入对应分区）

Official Resources / MCP Servers / Skills & Slash Commands / Hooks & Automation /
CLAUDE.md Templates / Prompting Guides / Workflows / IDE Integrations /
Agent SDK / Tools & Utilities / Tutorials & Videos / Community

- MCP Servers 内部再分：Development / Data & Storage / Search & Knowledge / Productivity & Collaboration。
- 不确定归到哪个分区时，先问，不要新建分区。

## 双语双文件同步（强制）

- 清单有两份平行文件：`README.md`（纯英文）与 `README.zh-CN.md`（纯中文）。**任何增删改都必须同时落到两份**，不允许只改一份。
- 两份的分区、条目顺序、链接、标记（`(Official)` 等）必须一一对应；只有描述语言不同（英文 vs 中文）。
- 顶部语言切换行不要动：`README.md` 顶部是 `**English** | [简体中文](README.zh-CN.md)`，`README.zh-CN.md` 顶部是 `[English](README.md) | **简体中文**`。
- 「中文深度文章」区块：两份都保留；文章标题保持中文原样，英文版描述用英文并标 `(Chinese)`，中文版描述用中文。
- GitHub README 不执行 JS，无法做原地页签，双文件互链是唯一可用的等效方案——不要尝试引入 JS/HTML 伪页签。

## 质量标准（不可妥协）

- 只收录**亲自用过/读过并觉得有价值**的资源。来源不明、纯凑数的不收。
- 每条必须有可点击且当前有效的链接。
- 教程/视频类必须能看出发布时间（Claude Code 更新快，过期内容要标注或删除）。

## 维护动作

- 新增条目时：同时在 `CHANGELOG.md` 顶部加一条本周记录。
- 修正失效链接、移除过期内容也要记进 `CHANGELOG.md` 的「更新 / 修正」。
- 周中临时想到的素材先记 `INBOX.md`，不要直接塞进 README。
- 提交前自查：确认 `INBOX.md`、`OPERATIONS.md` 未被 staged（二者是本地自用文件，已在 `.gitignore` 忽略）。避免用 `git add -A`/`git add .` 盲加；`.gitignore` 里这两行不要注释掉——一旦忽略失效被误提交，之后 `.gitignore` 也拦不住已跟踪的文件。

## 约束

- **不要自动 commit 或 push**。改完文件就停，由维护者决定何时提交。
- 不删除 LICENSE、不改动 Awesome badge。
- 保持双语风格与 README 既有语气一致，不重写已有条目除非被要求。
