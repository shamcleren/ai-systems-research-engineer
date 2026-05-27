# Week 2 TODO: RAG and Context Selection Basics / 第 2 周 TODO：RAG 与上下文选择基础

## How to Use This TODO / 如何使用这份 TODO

中文：你只需要在本文件里一步步填写答案。不要来回翻 paper note、glossary 或其他文档。你完成后，把本文件交给 mentor review；mentor 再负责把稳定内容整理到 paper note、glossary 和 TRI note。

English: Fill answers step by step in this file only. Do not jump between the paper note, glossary, or other documents. After you finish, send this TODO to the mentor for review; the mentor will organize stable content into the paper note, glossary, and TRI note.

## Goal / 目标

中文：本周目标不是完整掌握所有 RAG 细节，而是理解 retrieval、context selection、generator、grounding/provenance 的基本边界，并能说明 TRI Context Package 和普通 retrieval output 的区别。

English: The goal is not to master every RAG detail. The goal is to understand the basic boundaries of retrieval, context selection, generator, grounding/provenance, and explain how a TRI Context Package differs from raw retrieval output.

## Source / 阅读材料

中文：只读本地 PDF，不需要自己判断读哪个链接。

English: Read the local PDF only. You do not need to decide which link to use.

- Local PDF: `docs/papers/2005.11401-rag-for-knowledge-intensive-nlp.pdf`
- Source traceability / 来源追溯: https://arxiv.org/abs/2005.11401
- Paper: `Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks`
- Authors: Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Kuttler, Mike Lewis, Wen-tau Yih, Tim Rocktaschel, Sebastian Riedel, Douwe Kiela

## Step-by-Step Execution / 一步步执行

### Step 1: Title and Abstract / 标题和摘要

- [ ] Done

#### What to Read / 读什么

中文：打开本地 PDF，只看第一页的标题和 Abstract。你不需要读懂每个英文单词，先借助下面的中文导读完成 3 句话。

English: Open the local PDF and read only the title and Abstract on page 1. You do not need to understand every English word. Use the Chinese guide below to write three sentences.

#### Chinese Reading Guide / 中文导读

标题 `Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks` 可以先理解成：

```text
用 retrieval 增强 generation，解决需要大量外部知识的 NLP 任务。
也就是说，模型不是只靠参数里的记忆回答，而是先检索相关文档，再基于文档生成答案。
```

Abstract 的核心意思可以先这样理解：

1. 中文：纯 parametric model 把知识存进模型参数里，但知识可能不完整、过时，也不容易追溯来源。  
   English: A pure parametric model stores knowledge in model parameters, but that knowledge may be incomplete, stale, or hard to trace.
2. 中文：RAG 把 parametric memory 和 non-parametric memory 结合起来：生成模型负责生成，检索索引负责提供外部知识。  
   English: RAG combines parametric memory and non-parametric memory: the generator produces text, while the retrieval index provides external knowledge.
3. 中文：作者用 knowledge-intensive tasks 评测 RAG，观察检索增强是否能提升答案质量和事实性。  
   English: The authors evaluate RAG on knowledge-intensive tasks to see whether retrieval augmentation improves answer quality and factuality.

#### Your Answer / 你的回答

1. 这篇论文研究什么问题：

   ```text
   TODO: 在这里写 1 句中文。
   ```

2. 为什么这个问题重要：

   ```text
   TODO: 在这里写 1 句中文。
   ```

3. 作者大概怎么做：

   ```text
   TODO: 在这里写 1 句中文。
   ```

---

### Step 2: First Keywords / 第一批关键词

- [ ] Done

#### What to Read / 读什么

中文：仍然只看标题和 Abstract。不要继续读 Method。

English: Still read only the title and Abstract. Do not move to the Method yet.

#### What to Do / 做什么

中文：从下面候选词里选至少 10 个，给每个词写一句中文解释。先写粗糙版本即可。

English: Pick at least 10 terms from the candidates below and write one Chinese explanation for each. Rough explanations are enough.

Candidate terms / 候选术语：

```text
retrieval-augmented generation
knowledge-intensive task
parametric memory
non-parametric memory
retriever
generator
dense vector index
Wikipedia passages
latent document
RAG-Sequence
RAG-Token
grounding
provenance
context selection
```

#### Your Answer / 你的回答

| English term | 中文解释 |
|---|---|
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |
| TODO | TODO |

---

### Step 3: Problem Definition / 问题定义

- [ ] Done

#### What to Read / 读什么

中文：读 Introduction 的前半部分，只找一个问题：作者为什么认为只靠模型参数里的知识不够？

English: Read the first half of the Introduction. Look for one question only: why do the authors think knowledge stored only in model parameters is not enough?

#### Chinese Reading Guide / 中文导读

中文：你要找的不是所有模型细节，而是这个判断：模型参数是一种 memory，但它不容易更新、不容易解释来源，也可能缺少细节。检索系统可以把外部知识作为可替换、可追溯的 memory。

English: You are not looking for every model detail. You are looking for this idea: model parameters are a kind of memory, but they are hard to update, hard to trace, and may miss details. Retrieval can provide external, replaceable, traceable memory.

#### Your Answer / 你的回答

```text
TODO: 用中文写 2-3 句话。说明作者认为纯 parametric model 有什么问题，以及 retrieval 为什么有帮助。
```

---

### Step 4: System Model / 系统模型

- [ ] Done

#### What to Read / 读什么

中文：看 Figure 1 和方法部分里对 RAG 的说明。目标是把系统拆成输入、检索、生成、输出。

English: Read Figure 1 and the method description of RAG. The goal is to break the system into input, retrieval, generation, and output.

#### Chinese Reading Guide / 中文导读

RAG 可以先看成这个系统：

```text
input question
  -> retriever 从 Wikipedia index 里选 top-k passages
  -> generator 基于 question + retrieved passages 生成答案
  -> output answer
```

这里的重点不是模型结构细节，而是 context selection boundary：哪些 passage 被选进来，决定了 generator 能看到什么证据。

#### Your Answer / 你的回答

| Item | 中文回答 |
|---|---|
| input / 输入 | TODO |
| retriever 做什么 | TODO |
| selected context 是什么 | TODO |
| generator 做什么 | TODO |
| output / 输出 | TODO |

---

### Step 5: Context Selection Boundary / 上下文选择边界

- [ ] Done

#### What to Read / 读什么

中文：读方法部分中 retriever / latent document / retrieved passages 相关描述。只回答：RAG 的 context 是怎么被选出来的？

English: Read the method description around retriever / latent document / retrieved passages. Answer only this: how does RAG select context?

#### Chinese Reading Guide / 中文导读

中文：Week 1 的论文问的是“信息已经在上下文里，模型能不能用”。Week 2 的 RAG 论文更接近问“哪些信息会先被选进上下文”。这是 context use 和 context selection 的区别。

English: Week 1 asked: once information is already in context, can the model use it? Week 2's RAG paper is closer to asking: which information gets selected into context first? This is the difference between context use and context selection.

#### Your Answer / 你的回答

```text
TODO: 用中文写 3-5 句话。说明 RAG 如何选择 context，以及这个选择边界为什么重要。
```

---

### Step 6: RAG-Sequence vs RAG-Token / 两种 RAG 变体

- [ ] Done

#### What to Read / 读什么

中文：读 RAG-Sequence 和 RAG-Token 的说明。目标不是推公式，而是理解“文档选择粒度”不同。

English: Read the explanation of RAG-Sequence and RAG-Token. The goal is not to derive formulas, but to understand the different granularity of document selection.

#### Chinese Reading Guide / 中文导读

- RAG-Sequence：整段生成过程主要依赖同一批 retrieved documents。
- RAG-Token：生成每个 token 时可以考虑不同的 retrieved documents。

你只需要理解：这是两种把 retrieved context 和 generation 结合的方式。

#### Your Answer / 你的回答

RAG-Sequence：

```text
TODO: 用中文写 1-2 句话。
```

RAG-Token：

```text
TODO: 用中文写 1-2 句话。
```

---

### Step 7: Evaluation Model / 评测模型

- [ ] Done

#### What to Read / 读什么

中文：看 Experiments / Results。只抽取任务、baseline、metrics、证明什么、不证明什么。

English: Read Experiments / Results. Extract only tasks, baselines, metrics, what it proves, and what it does not prove.

#### Your Answer / 你的回答

| Item | 中文回答 |
|---|---|
| workloads / 任务 | 抽取式 QA（Natural Questions、TriviaQA）；生成式任务（Jeopardy 问题生成、MS MARCO 摘要） |
| baselines / 对比对象 | closed-book（纯参数模型）、retrieval-only（纯检索模型）、RAG-Sequence、RAG-Token |
| metrics / 指标 | QA：Exact Match + F1（自动指标）；生成：人工评估（真实性、流畅性） |
| what it proves / 它能证明什么 | RAG 在知识密集型任务上优于 closed-book 和 retrieval-only；可通过更新索引更新知识 |
| what it does not prove / 它不能证明什么 | 效率和成本（k 增大时 latency/cost 是否爆炸）；检索质量对生成的影响；reranker 的作用 |

---

### Step 8: TRI Connection / 连接 TRI

- [ ] Done

#### What to Do / 做什么

中文：回答这个问题：RAG 的 retrieved passages 和 TRI 的 Context Package 有什么不同？

English: Answer this question: how are RAG retrieved passages different from a TRI Context Package?

#### Chinese Hint / 中文提示

- RAG retrieved passages：通常是按 query 从文档库里检索出的文本片段。
- TRI Context Package：应该是结构化上下文，可能包含实体、关系、信号、事件、候选对象、约束、provenance。
- 关键区别：raw retrieval output 更像材料，Context Package 更像经过组织和解释的研究对象。

#### Your Answer / 你的回答

```text
TODO: 用中文写 3-5 句话。
```

---

### Step 9: Claim Audit / 主张审计

- [ ] Done

#### What to Do / 做什么

中文：写至少 5 行。每行都要有 claim、证据、不证明什么、和 TRI 的关系。

English: Write at least five rows. Each row must include claim, evidence, what it does not prove, and TRI relevance.

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

中文：完成后，把下面这段发给 mentor。mentor 会先 review 本 TODO，再把稳定内容整理到 paper note、glossary 和 TRI note。

English: After completion, send the prompt below to the mentor. The mentor will review this TODO first, then organize stable content into the paper note, glossary, and TRI note.

```text
请你按研究 mentor 的标准 review 我 Week 2 的 RAG TODO 答案，重点看：
1. 我是否抓住了 retrieval / context selection / generation 的边界；
2. 关键词解释是否准确；
3. 我是否说清楚 RAG retrieved passages 和 TRI Context Package 的区别；
4. evaluation model 是否区分了证明什么和不证明什么；
5. claim audit 有没有过度推断；
6. 请把稳定内容整理到 paper note、glossary 和 TRI note；
7. 下一周我应该补哪块能力。

Please review my Week 2 RAG TODO answers as a research mentor. Focus on:
1. whether I captured the boundaries between retrieval / context selection / generation;
2. whether the keyword explanations are accurate;
3. whether I explained the difference between RAG retrieved passages and TRI Context Package;
4. whether the evaluation model separates what is proven from what is not proven;
5. whether the claim audit over-infers;
6. please organize stable content into the paper note, glossary, and TRI note;
7. what capability I should improve next week.
```

## Done Criteria / 完成标准

- [ ] 中文：Step 1-10 都已经填写或勾选。
      English: Steps 1-10 are filled or checked.
- [ ] 中文：所有答案都先写在本 TODO 文件里。
      English: All answers are written in this TODO file first.
- [ ] 中文：你已经把 Review Prompt 发给 mentor。
      English: You have sent the Review Prompt to the mentor.

