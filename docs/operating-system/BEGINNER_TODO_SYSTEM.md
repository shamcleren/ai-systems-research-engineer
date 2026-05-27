# Beginner TODO System / 新人 TODO 系统

## Purpose / 目的

中文：这个文件定义以后所有学习任务应该怎么落到 TODO。你不需要凭记忆推进，只需要每周打开对应 TODO 文档，按步骤完成，然后找 mentor review。

English: This file defines how every learning task should become a TODO document. You should not need to rely on memory. Open the weekly TODO, follow the steps, then ask the mentor for review.

## Core Rule / 核心规则

中文：每个 TODO 都必须做到“只打开这一份 TODO，也知道下一步怎么做”。不能要求执行者自己从仓库结构里推断：读哪个材料、怎么理解英文材料、答案写哪里、完成后做什么、什么时候找 mentor。

English: Every TODO must be executable by opening that TODO file alone. The reader must not have to infer from repository structure which source to read, how to understand English material, where to answer, what to do after finishing, or when to ask the mentor.

## Source Priority / 材料优先级

中文：如果任务包含外部论文、官方文档、本地 note 或模板，TODO 必须明确说明它们的角色。

English: If a task includes external papers, official docs, local notes, or templates, the TODO must clearly state each source's role.

| 材料类型 / Source type | 中文：必须说明 | English: Must explain |
|---|---|---|
| 官方 paper / Official paper | 这是要阅读和引用的主材料 | This is the main source to read and cite |
| 本地 PDF / Local PDF | 如果官方 PDF 可公开下载且适合保存，应下载到 `docs/papers/`，并作为默认阅读入口 | If an official PDF is publicly downloadable and appropriate to store, download it into `docs/papers/` and use it as the default reading entry |
| 官方技术文档 / Official technical doc | 这是事实来源，不要凭记忆改写 | This is the factual source; do not rewrite from memory |
| 本地 TODO / Local TODO | 这是第一写作工作区；学习者先在 TODO 里回答 | This is the first writing workspace; the learner answers in the TODO first |
| 本地 paper note / Local paper note | 这是 mentor review 后的整理沉淀处，不是第一填写入口 | This is the organized note after mentor review, not the first answer entry |
| 本地 glossary / Local glossary | 这是 mentor review 后的术语沉淀处 | This is where terms are organized after mentor review |
| 本地项目文档 / Local project doc | 这是连接 TRI 或个人研究计划的上下文 | This provides context for TRI or the personal research plan |
| 可选参考 / Optional reference | 只在卡住时使用，不是主线任务 | Use only when blocked; it is not the main task |

## Required TODO Fields / TODO 必备字段

每个 TODO 文档必须包含：

Each TODO document must include:

| 字段 / Field | 说明 / Description |
|---|---|
| 目标 / Goal | 本周或本任务要训练什么能力 |
| 背景 / Context | 为什么要做这个任务 |
| 如何使用 / How to Use This TODO | 明确告诉学习者先在 TODO 里回答 |
| 阅读材料 / Source | 要读的 paper、PDF、文档、代码或实验 |
| 论文简介与当前影响 / Paper Brief and Current Impact | 用中文先解释论文讲什么、为什么重要、现在有哪些技术或能力吸收了它的思路；如果涉及最新生态，mentor 必须先核对来源 |
| 每一步怎么执行 / How to Execute Each Step | 每个 step 内部包含读什么、中文导读、怎么写、答案框 |
| 完成标准 / Done Criteria | 做到什么程度算完成 |
| 完成后做什么 / Completion Flow | 填 completion log、发 review prompt、等待 mentor review |
| 交付物 / Artifacts | mentor review 后需要整理到哪些文件 |
| Review Prompt | 完成后复制给 mentor 的 review 请求 |

## Inline Step Rule / Step 内联规则

中文：每个 TODO 的答案必须先写在 TODO 本文件里。不要把“步骤”和“写入位置”拆成两个相距很远的区域。每个 step 内部必须包含：读什么、中文导读或阅读辅助、具体输出形态、答案框。

English: Answers must be written in the TODO file first. Do not split "steps" and "where to write" into distant sections. Each step must include what to read, Chinese reading support, the expected output shape, and an answer box.

Example / 示例：

```text
### Step 1: Title and Abstract / 标题和摘要

#### What to Read / 读什么
中文：只读第一页标题和 Abstract。
English: Read only the title and Abstract on page 1.

#### Chinese Reading Guide / 中文导读
中文：这里给出非逐字翻译的理解提示，帮助英文论文新人进入任务。
English: Provide non-literal reading guidance for a beginner reader of English papers.

#### Your Answer / 你的回答
1. 这篇论文研究什么问题：
   TODO
```

中文：paper note、glossary、research note 是 mentor review 后的整理目标，不是学习者第一时间填写的地方。TODO 的 Review Prompt 可以要求 mentor 把稳定内容整理过去。

English: The paper note, glossary, and research note are organization targets after mentor review, not the learner's first answer locations. The TODO's Review Prompt may ask the mentor to organize stable content into them.

## Local Source Rule / 本地材料规则

中文：如果学习任务依赖一篇公开论文，mentor 应优先把官方 PDF 下载到 `docs/papers/`，并在 TODO 里写清楚本地 PDF 路径。官方 URL 仍然保留，用于来源追溯和版本核对。

English: If a learning task depends on a public paper, the mentor should prefer downloading the official PDF into `docs/papers/` and writing the local PDF path in the TODO. Official URLs should still be kept for source traceability and version checking.

中文：如果 PDF 是付费、访问受限、版权状态不清楚，或者不适合放入仓库，就不要复制到本地；TODO 必须明确说明“只能通过官方链接阅读”。

English: If the PDF is paywalled, access-restricted, unclear in copyright status, or inappropriate to store in the repo, do not copy it locally. The TODO must explicitly say "read through the official link only."

## Step Style / 步骤风格

中文：每一步都要足够小，适合纯新人执行。不要写“理解论文”这种抽象任务，要写“读 abstract，根据中文导读，用中文写 3 句话说明论文想解决什么问题”。如果源材料是英文论文，step 内必须给中文导读或关键词解释，不能只让学习者直接读英文。

English: Every step should be small enough for a beginner. Do not write abstract tasks like "understand the paper." Write concrete tasks like "read the abstract, use the Chinese guide, and write three Chinese sentences explaining the problem." If the source is an English paper, the step must include Chinese reading support or keyword explanations, not only ask the learner to read English directly.

## Bilingual Completeness Rule / 双语完整性规则

中文：所有 mentor-facing TODO 必须 section-level bilingual。尤其是完成标准、review prompt、completion log、每一步要求，不能只翻译标题；具体细项也必须有中文和英文。

English: All mentor-facing TODOs must be bilingual at the section level. In particular, done criteria, review prompts, completion logs, and step requirements must not only translate headings; each concrete subitem must have both Chinese and English.

Good / 好：

```text
- [ ] 中文：glossary 至少有 20 个术语，并且每个术语都有中文解释。
      English: The glossary has at least 20 terms, and each term has a Chinese explanation.
```

Bad / 不好：

```text
- [ ] Glossary has at least 20 terms.
```

## Default Learning Flow / 默认学习流程

```text
1. 读标题和摘要 / Read title and abstract
2. 抽关键词 / Extract key terms
3. 写中文问题定义 / Write the problem in Chinese
4. 看方法图或系统结构 / Inspect method figure or system structure
5. 抽实验设置 / Extract evaluation setup
6. 写 claim audit / Write claim audit
7. 连接 TRI / Connect to TRI
8. 找 mentor review / Ask mentor for review
```

## Completion Flow / 完成后流程

中文：每个 TODO 都必须明确“完成后做什么”。默认流程如下：

English: Every TODO must clearly say what to do after finishing. The default flow is:

1. 中文：更新当前 TODO 的 checkbox。  
   English: Update the checkboxes in the current TODO.
2. 中文：填写当前 TODO 的 `Completion Log / 完成记录`。  
   English: Fill the current TODO's `Completion Log / 完成记录`.
3. 中文：把 TODO 中的 `Review Prompt / 复盘请求` 发给 mentor。  
   English: Send the TODO's `Review Prompt / 复盘请求` to the mentor.
4. 中文：等待 mentor review；如果 mentor 要求修改，先修改本周产物；如果 mentor 明确同意，再进入下一周。  
   English: Wait for mentor review. If the mentor asks for revision, revise the current week's artifacts first. Move to the next week only after mentor approval.

## TODO Quality Gate / TODO 质量门禁

中文：创建或更新 TODO 后，必须用下面清单自检。任一项为否，就不能认为 TODO 已完成。

English: After creating or updating a TODO, check it against the list below. If any item is no, the TODO is not complete.

- [ ] 中文：只打开这份 TODO，是否知道第一步打开哪个材料？  
      English: By opening only this TODO, can the reader tell which source to open first?
- [ ] 中文：是否区分了“要读的原始材料”和“mentor review 后整理的长期笔记”？  
      English: Does it distinguish the original source to read from the local note to organize after review?
- [ ] 中文：每一步是否在 step 内部就包含答案框？  
      English: Does every step include its answer box inside the step itself?
- [ ] 中文：每一步是否说明了答案形态，例如 3 句话、5 行表格、至少 5 条 claim audit？  
      English: Does every step specify the expected answer shape, such as three sentences, a five-row table, or at least five claim-audit rows?
- [ ] 中文：如果源材料是英文论文，是否提供了中文导读或关键词解释？  
      English: If the source is an English paper, does it provide Chinese reading guidance or keyword explanations?
- [ ] 中文：是否在正式阅读步骤前提供了中文论文简介、当前影响，以及哪些现代技术或能力吸收了论文思路？
      English: Before the reading steps, does it provide a Chinese paper brief, current impact, and which modern technologies or capabilities have absorbed the paper's ideas?
- [ ] 中文：完成标准的每个细项是否都有中文和英文？  
      English: Does every done-criteria subitem have both Chinese and English?
- [ ] 中文：完成后是否知道要填 completion log、发 review prompt、等待 review？  
      English: After finishing, does the reader know to fill the completion log, send the review prompt, and wait for review?
- [ ] 中文：是否避免了“理解、研究、思考”这类没有输出形态的抽象动词？  
      English: Does it avoid abstract verbs such as "understand," "research," or "think" without an output shape?

## Weekly Habit / 每周习惯

中文：每周开始先看 `docs/todos/`；每周结束把完成情况写回同一个 TODO 文件，不另开散乱笔记。

English: Start each week from `docs/todos/`. At the end of the week, write completion notes back into the same TODO file instead of scattering notes elsewhere.
