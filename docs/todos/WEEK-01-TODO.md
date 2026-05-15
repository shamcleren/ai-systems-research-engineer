# Week 1 TODO: Paper Anatomy and Context Use / 第 1 周 TODO：论文结构与上下文使用

## How to Use This TODO / 如何使用这份 TODO

中文：你只需要在本文件里一步步填写答案。不要来回翻 `paper note`、`glossary` 或其他文档。你完成后，把本文件交给 mentor review；mentor 再负责把稳定内容整理到 paper note 和 glossary。

English: Fill answers step by step in this file only. Do not jump between the paper note, glossary, or other documents. After you finish, send this TODO to the mentor for review; the mentor will organize stable content into the paper note and glossary.

## Goal / 目标

中文：本周目标不是读懂所有英文细节，而是学会把一篇 AI systems paper 拆成：problem、method、evaluation、claim、limitation。

English: The goal is not to understand every English detail. The goal is to learn how to break an AI systems paper into problem, method, evaluation, claim, and limitation.

## Source / 阅读材料

中文：只读本地 PDF，不需要自己判断读哪个链接。

English: Read the local PDF only. You do not need to decide which link to use.

- Local PDF: `docs/papers/2307.03172-lost-in-the-middle.pdf`
- Source traceability / 来源追溯: https://arxiv.org/abs/2307.03172
- Published version / 正式发表版本: https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00638/119630/Lost-in-the-Middle-How-Language-Models-Use-Long

## Step-by-Step Execution / 一步步执行

### Step 1: Title and Abstract / 标题和摘要

- [x] Done

#### What to Read / 读什么

中文：打开本地 PDF，只看第一页的标题和 Abstract。你不需要读懂每个英文单词。先借助下面的中文导读完成 3 句话。

English: Open the local PDF and read only the title and Abstract on page 1. You do not need to understand every English word. Use the Chinese guide below to write three sentences.

#### Chinese Reading Guide / 中文导读

标题 `Lost in the Middle: How Language Models Use Long Contexts` 可以先理解成：

```text
模型在长上下文中使用信息时，可能会“卡在中间”。
也就是说，相关信息出现在上下文开头或结尾时，模型更容易用到；
相关信息出现在中间时，模型表现可能变差。
```

Abstract 的核心意思可以先这样理解：

1. 中文：现在很多语言模型支持更长的输入窗口，但“能放进去很多 token”不等于“模型能稳定使用里面的关键信息”。  
   English: Many language models now support longer input windows, but fitting many tokens does not mean the model can reliably use the key information inside.
2. 中文：作者测试了两类任务：multi-document QA 和 key-value retrieval，用来观察模型是否能从长上下文中找到并使用相关信息。  
   English: The authors test two task types: multi-document QA and key-value retrieval, to observe whether models can find and use relevant information in long contexts.
3. 中文：作者改变相关信息在上下文中的位置，发现模型在信息位于开头或结尾时通常更好，在中间时更差。  
   English: The authors change where the relevant information appears in the context and find that models are usually better when it is near the beginning or end, and worse when it is in the middle.

#### Your Answer / 你的回答

中文：请只写 3 句话。不要追求完美，先写自己的理解。

English: Write only three Chinese sentences. Do not aim for perfection; write your current understanding.

1. 这篇论文研究什么问题：

   ```text
   这篇论文研究长上下文模型是否真的能稳定使用上下文中的相关信息，尤其是相关信息出现在不同位置时模型表现是否会变化。
   ```

2. 为什么这个问题重要：

   ```text
   这个问题重要，因为更大的上下文窗口不等于更可靠的上下文使用能力，实际系统不能只假设“放进去的信息模型就会用”。
   ```

3. 作者大概怎么评测：

   ```text
   作者通过 multi-document QA 和 key-value retrieval 两类任务，改变相关信息在上下文中的位置，观察模型准确率是否出现首尾高、中间低的变化。
   ```

---

### Step 2: First Keywords / 第一批关键词

- [x] Done

#### What to Read / 读什么

中文：仍然只看标题和 Abstract。不要继续读 Introduction。

English: Still read only the title and Abstract. Do not move to the Introduction yet.

#### What to Do / 做什么

中文：从下面候选词里选 10 个，给每个词写一句中文解释。当前草稿来自已经提交的 glossary，可直接修改。

English: Pick 10 terms from the candidates below and write one Chinese explanation for each. The current draft is migrated from the committed glossary and can be edited directly.

#### Your Answer / 你的回答

| English term | 中文解释 |
|---|---|
| long context | 长上下文，指模型输入中包含大量 token 或多段信息，现在很多模型达到 1M 上下文窗口 |
| relevant information | 相关信息，完成任务所需的关键证据 |
| relevant information position | 有效信息在整个上下文中所处的物理位置，可以简单理解为行或段落的位置 |
| evaluation protocol | 评测协议，定义任务、变量、指标和比较方式 |
| multi-document question answering | 多文档问答，给模型一个问题和多篇文档，只有一篇有答案，专门测试模型能否在长上下文中找到正确答案 |
| key-value retrieval | 键值检索，通过 key 准确找到 value，要求 value 完全一致不能被模型加工，找不到也不能编造 |
| primacy bias | 首因偏差，模型对开头的信息记得更牢，类似人类的第一印象 |
| recency bias | 近因偏差，模型对结尾的信息记得更牢，结合 primacy bias 类似人类接收持续信息时的状态 |
| U-shaped performance curve | U 型性能曲线，开头和结尾效果最好，中间最差甚至不如不加检索直接查询 |
| distractor | 干扰文档，通过相关性算法检索到的高分段落，但实际不含答案，能有效干扰模型召回 |

---

### Step 3: Introduction / 引言

- [x] Done

#### What to Read / 读什么

中文：读 PDF 的 Introduction。只找一个问题：作者认为大家对 long-context model 可能有什么误解？

English: Read the Introduction in the PDF. Look for one thing only: what misunderstanding do the authors identify about long-context models?

#### Chinese Reading Guide / 中文导读

中文：你要找的不是所有技术细节，而是这个判断：更长的 context window 不自动等于更强的 context use 能力。

English: You are not looking for every technical detail. You are looking for this idea: a longer context window does not automatically mean stronger context-use ability.

#### Your Answer / 你的回答

```text
作者在 introduction 里指出的关键风险是，大家都在追求“上下文窗口能塞多长”，但没有认真验证“塞进去之后模型到底用不用得好”。窗口变长不等于模型能可靠使用其中的信息。
```

---

### Step 4: Main Experimental Variable / 主要实验变量

- [x] Done

#### What to Read / 读什么

中文：看论文里关于 relevant information position 的说明。重点看作者如何改变相关信息在上下文里的位置。

English: Read the part about relevant information position. Focus on how the authors change where the relevant information appears in the context.

#### What to Do / 做什么

中文：用一句话回答：为什么“相关信息的位置”是一个好的实验变量？

English: Answer in one sentence: why is "the position of relevant information" a good experimental variable?

#### Your Answer / 你的回答

```text
实验设计的核心是控制变量法：固定其他变量，只动信息位置，观察 U 型曲线是否稳定出现；唯一一致变化的因素是位置，所以位置是因果变量，也是一个有限可枚举、可控、能揭示本质的好实验变量。
```

---

### Step 5: Two Tasks / 两个任务

- [x] Done

#### What to Read / 读什么

中文：读 multi-document QA 和 key-value retrieval 的任务设置。目标不是理解所有数据集细节，而是知道这两个任务分别在测什么。

English: Read the task setup for multi-document QA and key-value retrieval. The goal is not to understand every dataset detail, but to know what each task measures.

#### Chinese Reading Guide / 中文导读

- multi-document QA：给模型多个文档和一个问题，答案藏在某个相关文档里，看模型能不能从长上下文里找到证据并回答。
- key-value retrieval：给模型很多 key-value 对，再问某个 key 对应的 value，看模型能不能从长上下文里精确取回目标值。

#### Your Answer / 你的回答

multi-document QA：

```text
Multi-document QA 是更接近真实场景的任务：模型拿到一个问题和多篇文档，只有部分文档包含答案。它测试的不只是“看到关键词”，还包括从长上下文里定位证据、理解问题、再组织答案。
```

key-value retrieval：

```text
Key-value retrieval 是更受控的最简诊断任务：上下文里有很多 key-value 对，模型需要根据 key 精确取回对应 value。它要求答案完全匹配，不能加工、不能编造，因此更适合测试模型是否能在长上下文中精确使用目标信息。
```

---

### Step 6: One-Sentence Thesis / 一句话 thesis

- [x] Done

#### What to Do / 做什么

中文：用下面格式写一句话。可以很朴素，不需要像论文一样正式。

English: Use the format below to write one sentence. It can be plain; it does not need to sound like a paper.

```text
这篇论文认为 <问题> 可以通过 <评测方法> 暴露出来，证据是 <主要现象>。
```

#### Your Answer / 你的回答

```text
这篇论文认为长上下文模型的注意力会随信息位置变化而丢失，可以通过改变关键信息在上下文中的位置暴露出来，证据是准确率呈现 U 型曲线：首尾高、中间低，中间位置甚至不如不给文档的 closed-book baseline。
```

---

### Step 7: Evaluation Model / 评测模型

- [ ] Done

#### What to Do / 做什么

中文：把论文评测拆成 5 个格子。先用中文短语即可。

English: Break the evaluation into five slots. Short Chinese phrases are enough.

#### Your Answer / 你的回答

| Item | 中文回答 |
|---|---|
| workload / 任务负载 | TODO |
| variable / 变量 | TODO |
| metrics / 指标 | TODO |
| what it proves / 它能证明什么 | TODO |
| what it does not prove / 它不能证明什么 | TODO |

---

### Step 8: TRI Connection / 连接 TRI

- [ ] Done

#### What to Do / 做什么

中文：回答下面这个问题：TRI Paper 3 是在评估“上下文构造质量”，这篇论文是在评估“上下文使用质量”，两者有什么区别？

English: Answer this question: TRI Paper 3 evaluates context construction quality, while this paper evaluates context use quality. What is the difference?

#### Chinese Hint / 中文提示

- context construction quality：有没有把相关信息放进 Context Package。
- context use quality：相关信息已经在上下文里时，模型能不能稳定使用它。

#### Your Answer / 你的回答

```text
TODO: 用中文写 3-5 句话。
```

---

### Step 9: Claim Audit / 主张审计

- [ ] Done

#### What to Do / 做什么

中文：写至少 5 行。每行只要朴素清楚，不要扩大论文结论。

English: Write at least five rows. Keep each row plain and conservative; do not overstate the paper's conclusion.

#### Your Answer / 你的回答

| Claim / 主张 | Evidence / 证据 | What it does not prove / 不证明什么 | TRI relevance / 和 TRI 的关系 |
|---|---|---|---|
| TODO | TODO | TODO | TODO |
| TODO | TODO | TODO | TODO |
| TODO | TODO | TODO | TODO |
| TODO | TODO | TODO | TODO |
| TODO | TODO | TODO | TODO |

---

### Step 10: Completion and Mentor Review / 完成并找 mentor review

- [ ] Done

#### Completion Log / 完成记录

| Item | Answer |
|---|---|
| Date / 日期 | TODO |
| Time spent / 耗时 | TODO |
| Hardest part / 最难的地方 | TODO |
| One question / 一个问题 | TODO |

#### Review Prompt / 复盘请求

中文：完成后，把下面这段发给 mentor。mentor 会先 review 本 TODO，再把稳定内容整理到 paper note 和 glossary。

English: After completion, send the prompt below to the mentor. The mentor will review this TODO first, then organize stable content into the paper note and glossary.

```text
请你按研究 mentor 的标准 review 我 Week 1 的 Lost in the Middle TODO 答案，重点看：
1. 我是否抓住了 problem / method / evaluation / claim；
2. 关键词解释是否准确；
3. TRI connection 是否牵强；
4. claim audit 有没有过度推断；
5. 请把稳定内容整理到 paper note 和 glossary；
6. 下一周我应该补哪块能力。

Please review my Week 1 Lost in the Middle TODO answers as a research mentor. Focus on:
1. whether I captured problem / method / evaluation / claim;
2. whether the keyword explanations are accurate;
3. whether the TRI connection is forced;
4. whether the claim audit over-infers;
5. please organize stable content into the paper note and glossary;
6. what capability I should improve next week.
```

## Done Criteria / 完成标准

- [ ] 中文：Step 1-10 都已经填写或勾选。  
      English: Steps 1-10 are filled or checked.
- [ ] 中文：所有答案都先写在本 TODO 文件里。  
      English: All answers are written in this TODO file first.
- [ ] 中文：你已经把 Review Prompt 发给 mentor。  
      English: You have sent the Review Prompt to the mentor.
