# Research Wiki

一个面向专业科研工作的 LLM Wiki 初版。它不只是保存 PDF 和论文摘要，而是把文献逐步编译成可追溯、可质疑、可继续生长的研究知识网络。

## 核心链路

```text
原始论文（raw）
  → 论文卡片（paper：这篇论文做了什么）
  → 科研主张（claim：它支持、反驳或限定了什么结论）
  → 概念 / 方法 / 数据集 / 实体
  → 研究问题（question）与假设（hypothesis）
  → 跨文献综合（synthesis：目前能得出什么、还不能得出什么）
```

最关键的区分是：

- **paper 是来源单元**：忠实记录单篇论文的问题、方法、结果与限制。
- **claim 是证据单元**：把不同论文对同一可检验命题的支持、反驳和限定放在一起。
- **synthesis 是研究判断**：只在跨来源比较后形成，并明确证据边界和推断。

## 目录

| 路径 | 用途 |
| --- | --- |
| `raw/papers/` | 原始 PDF、论文正文或补充材料，只读 |
| `raw/notes/` | 人工阅读笔记、会议笔记、手写转录，只读 |
| `raw/imports/` | BibTeX、RIS、CSV、Zotero 导出等，只读 |
| `raw/assets/` | 图片、图表和附件 |
| `inbox/` | 尚未决定如何处理的论文、链接和想法 |
| `wiki/papers/` | 一篇论文一张规范化卡片 |
| `wiki/claims/` | 可被多篇论文支持、反驳或限定的原子主张 |
| `wiki/concepts/` | 概念、理论和术语 |
| `wiki/methods/` | 方法、实验设计、指标和分析流程 |
| `wiki/datasets/` | 数据集、队列、语料库和基准 |
| `wiki/entities/` | 作者、实验室、机构、期刊、会议、软件等 |
| `wiki/searches/` | 可复现的文献检索式和筛选记录 |
| `wiki/questions/` | 研究问题及其证据进展 |
| `wiki/hypotheses/` | 可证伪假设及其证据状态 |
| `wiki/projects/` | 具体研究项目的上下文与决策 |
| `wiki/synthesis/` | 主题综述、证据图谱、争议与研究缺口 |
| `wiki/queries/` | 经确认值得保留的查询答案 |
| `templates/` | 各类页面模板 |
| `index.md` | 全库内容目录；查询时先读 |
| `dashboard.md` | Obsidian 入口页和可选 Dataview 看板 |
| `log.md` | 倒序记录每次 ingest、query、lint 和结构变更 |
| `CLAUDE.md` | 全部 schema、判断标准和工作流 |
| `AGENTS.md` | Codex 等 Agent 的入口规范 |

## 第一次使用

1. 用 Obsidian 打开整个 `research_wiki/` 文件夹。
2. 把论文放进 `raw/papers/`；文件名推荐使用 `firstauthor-year-short-title.pdf`。
3. 对 Agent 说：`深度 ingest raw/papers/xxx.pdf`。
4. Agent 会先查重、读取论文并与你确认关键结论，再建立论文卡片和知识关联。
5. 从 `dashboard.md` 或 `index.md` 浏览结果。

如果只想先筛选文献，可以说：`快速 ingest raw/papers/xxx.pdf`。快速模式只建基础论文卡片，不创建主张页，不把粗读结果伪装成深度理解。

## 常用指令

- `快速 ingest [文件]`：只做元数据、问题、摘要级结论和待读判断。
- `深度 ingest [文件]`：完整阅读，建立主张、概念、方法和研究问题链接。
- `这几篇论文对 [[某个主张]] 的证据是否一致？`：按证据关系回答。
- `围绕 [[某个研究问题]] 做一次综合`：生成候选综合，确认后写入 `wiki/synthesis/`。
- `整理 inbox`：逐项建议去向，确认后执行。
- `lint`：只生成健康检查与修复建议，不自动大改。

## 使用边界

- 原始资料永不由 Agent 改写。
- AI 摘要不是证据；关键数字、结论和引文必须能定位到页码、章节、图或表。
- “作者声称”“结果直接显示”“我的推断”必须分开写。
- 预印本、同行评议、勘误、撤稿和版本状态不能凭印象判断；需要时重新核验。
- 参考文献管理器可以继续作为书目主库；本 Wiki 负责的是消化、证据关联和研究判断。

详细规则见 [[CLAUDE]]。
