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

### 先认识 Obsidian 和 Agent

这个项目需要两个角色共同工作：

- **Obsidian 是阅读和浏览工具**：用来打开 Markdown 文件、点击双链、查看论文卡片和知识网络。
- **Agent 是实际维护 Wiki 的 AI 助手**：它会读取论文和项目规则，查重、提取证据、创建或更新 Markdown 页面，并维护双链、`index.md` 和 `log.md`。

这里的 **Agent** 不是某一个特定产品。它可以是 Claude Code、OpenAI Codex、WorkBuddy，或者其他能够直接读取和修改本地工作目录的 AI 工作助手。无论使用哪一种，关键是让它获得整个 `research_wiki/` 文件夹的读写权限，而不只是把一篇 PDF 单独上传到普通聊天窗口。

如果一个 AI 工具只能阅读聊天附件、不能打开本地文件夹，它可以帮你总结论文，但无法可靠地维护这个 Wiki 的目录、双链、索引和日志。

### 第 1 步：下载并用 Obsidian 打开

不熟悉 Git 也没有关系：可以在 GitHub 页面点击 **Code → Download ZIP**。解压后的文件夹通常名为 `research-wiki-main/`，也可以把它重命名为 `research_wiki/`。

打开 Obsidian，选择“打开本地仓库”或“将文件夹作为仓库打开”，然后选择整个 `research_wiki/`。不要只打开其中的 `wiki/` 或 `raw/` 子目录。

仓库中已经带有一篇 SAM 3D 论文的完整示例，可以先从 `dashboard.md` 或 `index.md` 点击浏览，理解论文卡片、主张、方法和数据集是怎样连接起来的。

### 第 2 步：让 Agent 打开同一个目录

再用你的 Agent 打开同一个 `research_wiki/` 文件夹，并把它设为当前工作目录、项目目录或 workspace。不同工具的叫法可能不同：

- **Claude Code**：在 Claude Code 中进入或选择这个文件夹，再开始对话。
- **OpenAI Codex**：新建任务时选择这个文件夹作为项目或工作目录。
- **WorkBuddy**：把这个文件夹作为本地项目或 workspace 打开。
- **其他 Agent**：确认它能看到 `AGENTS.md`、`CLAUDE.md`、`raw/`、`wiki/` 和 `templates/`，并拥有修改 Markdown 文件的权限。

如果 Agent 弹出文件访问授权，只需要授权当前 `research_wiki/` 文件夹，不必授予整个磁盘的权限。

第一次连接时，可以先发送下面这段话，让 Agent 熟悉项目而不立即改文件：

```text
请先完整阅读当前目录中的 AGENTS.md、CLAUDE.md 和 index.md，
带我熟悉这个 Research Wiki 的目录、证据规则和工作流程。
暂时不要修改任何文件。
```

### 第 3 步：放入第一篇论文

把准备处理的 PDF 放进 `raw/papers/`。推荐使用稳定、容易识别的文件名，例如：

```text
firstauthor-year-short-title.pdf
```

`raw/` 是原始来源层。Agent 可以读取和引用其中的资料，但默认不会修改、覆盖、移动或删除原始论文。

### 第 4 步：选择快速或深度 Ingest

如果只是想先判断论文值不值得读，对 Agent 说：

```text
快速 ingest raw/papers/firstauthor-year-short-title.pdf
```

快速模式只读取元数据和摘要级信息，建立基础论文卡片，不创建主张页，也不会把粗读结果伪装成全文结论。

如果希望完整阅读并接入知识网络，对 Agent 说：

```text
深度 ingest raw/papers/firstauthor-year-short-title.pdf
```

深度模式会阅读全文，定位关键结论所在的页码、章节、图或表，并判断论文是在支持、反驳还是限定已有主张。

### 第 5 步：确认关键理解

深度 Ingest 不会立刻写入大量页面。Agent 应当先向你展示：

- 它对论文研究问题、方法、主要结果和局限的理解；
- 准备建立或更新的关键主张；
- 每条主张的证据位置和适用边界；
- 与现有 Wiki 页面可能发生的支持、反驳或限定关系。

确认这些内容没有明显误读后，回复“确认写入”。Agent 才会正式建立论文卡片、主张和必要的概念、方法或数据集页面，并同步维护反向链接、`index.md` 和 `log.md`。

### 第 6 步：查看和继续使用

写入完成后，可以从以下两个入口查看结果：

- `dashboard.md`：日常入口；安装 Dataview 后可以显示自动看板，不安装也不影响基本使用。
- `index.md`：完整内容目录，适合按论文、主张、概念、方法或研究问题浏览。

之后可以继续把论文放进 `raw/papers/`，让 Agent 逐篇 Ingest。随着来源增加，同一个 `claim` 页面会逐步汇集支持、反驳和限定证据，而不是为每篇论文重复创建近义结论。

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
