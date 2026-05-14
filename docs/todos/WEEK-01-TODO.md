# Week 1 TODO: Paper Anatomy and Context Use / 第 1 周 TODO：论文结构与上下文使用

## Goal / 目标

中文：本周目标不是“读懂所有细节”，而是学会 AI systems paper 的基本拆解方法：problem、method、evaluation、claim、limitation。

English: The goal is not to understand every detail. The goal is to learn how to break down an AI systems paper into problem, method, evaluation, claim, and limitation.

## Main Paper / 主论文

中文：本周读 `Lost in the Middle: How Language Models Use Long Contexts`。

English: This week, read `Lost in the Middle: How Language Models Use Long Contexts`.

Links:

- arXiv: https://arxiv.org/abs/2307.03172
- TACL: https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00638/119630/Lost-in-the-Middle-How-Language-Models-Use-Long

## Why This Paper / 为什么读这篇

中文：它直接回答一个 Context Engineering 的核心问题：模型拿到长上下文后，是否真的能稳定使用其中的关键信息？

English: It directly asks a core Context Engineering question: after a model receives a long context, can it reliably use the key information inside it?

## Artifacts / 交付物

需要更新：

Update these files:

- `docs/notes/papers/2026-05-14-lost-in-the-middle.md`
- `docs/glossary/context-engineering-glossary.md`
- this TODO file, under `Completion Log / 完成记录`

## Step-by-Step TODO / 一步步执行

- [ ] **Step 1: Read the title and abstract / 阅读标题和摘要**

  中文：只读标题和摘要。用中文写 3 句话：这篇论文研究什么问题、为什么重要、作者大概怎么评测。

  English: Read only the title and abstract. Write three Chinese sentences: what problem the paper studies, why it matters, and roughly how the authors evaluate it.

- [ ] **Step 2: Extract 10 keywords / 抽 10 个关键词**

  中文：从摘要和 introduction 抽 10 个英文关键词，写入 glossary。每个词写中文解释，不要求完美。

  English: Extract 10 English keywords from the abstract and introduction, then add them to the glossary. Give each term a Chinese explanation. It does not need to be perfect.

- [ ] **Step 3: Read introduction / 阅读 introduction**

  中文：读 introduction。写下作者认为“长上下文模型”有什么风险或误解。

  English: Read the introduction. Write what risk or misunderstanding the authors identify about long-context models.

- [x] **Step 4: Find the experiment variable / 找实验变量**

  中文：找出本文最重要的实验变量：相关信息在上下文中的位置。写一句话解释为什么这是一个好变量。

  English: Identify the most important experimental variable: the position of relevant information in the context. Write one sentence explaining why this is a good variable.

- [ ] **Step 5: Understand two tasks / 理解两个任务**

  中文：分别用中文解释 multi-document QA 和 key-value retrieval。每个任务写 2-3 句话。

  English: Explain multi-document QA and key-value retrieval in Chinese. Write 2-3 sentences for each task.

- [ ] **Step 6: Write one-sentence thesis / 写一句话 thesis**

  中文：用这个格式写：这篇论文认为 `<问题>` 可以通过 `<评测方法>` 暴露出来，证据是 `<主要现象>`。

  English: Use this format: This paper argues that `<problem>` can be exposed by `<evaluation method>`, with `<main observation>` as evidence.

- [ ] **Step 7: Fill evaluation model / 填 evaluation model**

  中文：在 paper note 里补充 workload、variable、metrics、what it proves、what it does not prove。

  English: In the paper note, fill workload, variable, metrics, what it proves, and what it does not prove.

- [ ] **Step 8: Connect to TRI / 连接 TRI**

  中文：回答：TRI Paper 3 是在评估“上下文构造质量”，这篇论文是在评估“上下文使用质量”，两者有什么区别？

  English: Answer this: TRI Paper 3 evaluates context construction quality, while this paper evaluates context use quality. What is the difference?

- [ ] **Step 9: Write claim audit / 写 claim audit**

  中文：至少写 5 条 claim audit。每条都要包含：claim、证据、不证明什么、和 TRI 的关系。

  English: Write at least five claim-audit rows. Each row should include claim, evidence, what it does not prove, and TRI relevance.

- [ ] **Step 10: Ask for mentor review / 找 mentor review**

  中文：完成后复制下面的 Review Prompt 给 mentor。

  English: After completion, copy the Review Prompt below to the mentor.

## Done Criteria / 完成标准

中文：完成以下内容才算 Week 1 完成。

English: Week 1 is complete only after the following are done.

- [ ] Paper note has title, problem, method, evaluation, TRI connection, and claim audit.
- [ ] Glossary has at least 20 terms.
- [ ] This TODO file has a completion log.
- [ ] You asked mentor for review.

## Review Prompt / 复盘请求

```text
请你按研究 mentor 的标准 review 我 Week 1 的 Lost in the Middle 笔记，重点看：
1. 我是否抓住了 problem / method / evaluation / claim；
2. bilingual glossary 是否准确；
3. TRI connection 是否牵强；
4. claim audit 有没有过度推断；
5. 下一周我应该补哪块能力。

Please review my Week 1 Lost in the Middle note as a research mentor. Focus on:
1. whether I captured problem / method / evaluation / claim;
2. whether the bilingual glossary is accurate;
3. whether the TRI connection is forced;
4. whether the claim audit over-infers;
5. what capability I should improve next week.
```

## Completion Log / 完成记录

中文：完成后在这里记录日期、耗时、最难的地方、一个问题。

English: After completion, record the date, time spent, hardest part, and one question here.

