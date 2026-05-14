# Paper Note: Lost in the Middle / 论文笔记：Lost in the Middle

## How to Use This Note / 如何使用这份笔记

中文：这不是一份要一次性写完的完整论文精读报告。你应该按 `docs/todos/WEEK-01-TODO.md` 的步骤逐步填写。先用中文写清楚，再保留关键英文术语。

English: This is not a full deep-reading report to complete in one sitting. Fill it step by step using `docs/todos/WEEK-01-TODO.md`. Explain ideas in Chinese first, while keeping key English terms.

## Metadata

- Title: Lost in the Middle: How Language Models Use Long Contexts
- Authors: Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
- Source: arXiv:2307.03172 / TACL 2023
- URL: https://arxiv.org/abs/2307.03172
- Paper type: evaluation / analysis paper
- Topic tags: long context, context use, evaluation protocol, multi-document QA, key-value retrieval

## Bilingual Keyword Table

中文：先不要追求翻译完美。目标是看到英文术语时能知道它在论文论证中扮演什么角色。

English: Do not aim for perfect translation first. The goal is to know what role each English term plays in the paper's argument.

| English term | Chinese explanation | Why it matters |
|---|---|---|
| long context | 长上下文，指模型输入中包含大量 token 或多段信息 | 本文研究模型是否真的能使用长上下文中的相关信息 |
| input context | 输入上下文，传给模型的全部输入材料 | Context Engineering 的核心对象之一 |
| relevant information | 相关信息，回答任务所需的关键证据 | 本文通过改变相关信息位置来测试模型是否使用它 |
| position | 位置，相关信息出现在上下文开头、中间或结尾 | 本文的核心实验变量 |
| multi-document question answering | 多文档问答，需要从多个文档中找证据回答问题 | 用来模拟长上下文中的真实检索和阅读任务 |
| key-value retrieval | 键值检索，根据 key 在长上下文中找到对应 value | 更受控的合成任务，用于隔离位置影响 |
| evaluation protocol | 评测协议，定义任务、变量、指标和比较方式 | 本文贡献之一是提供评测长上下文使用能力的方法 |
| performance degradation | 性能下降 | 用于描述相关信息位置变化后模型表现变差 |
| primacy bias | 首因偏置，对开头信息使用更好 | 解释模型在上下文开头表现更好的现象 |
| recency bias | 近因偏置，对结尾信息使用更好 | 解释模型在上下文结尾表现更好的现象 |
| U-shaped performance | U 形表现，开头和结尾较好，中间较差 | 本文最重要的实验观察之一 |
| robust use | 稳健使用，模型在不同位置都能可靠使用相关信息 | 本文发现当前模型并不总能做到 |
| long-context model | 长上下文模型，支持更大输入窗口的语言模型 | 本文指出窗口变长不等于上下文使用能力稳健 |
| distractor document | 干扰文档，不包含答案但会占据上下文空间 | 用于构造多文档问答中的噪声 |
| oracle document | 包含答案或关键证据的文档 | 其位置变化用于测试模型对上下文位置的敏感性 |

中文：阅读时至少再补 5 个词。

English: Add at least 5 more terms while reading.

## One-Sentence Thesis

中文：这句话是你对论文主张的压缩表达。先照着已有版本理解，之后可以改写成自己的版本。

English: This sentence compresses the paper's main argument. First understand the current version, then rewrite it in your own words.

This paper argues that language models with long input windows do not necessarily use long contexts robustly, because their performance can degrade when relevant information appears in the middle of the input context, as shown by multi-document question answering and key-value retrieval evaluations.

## Problem

中文：论文到底在问什么问题？

English: What question does the paper ask?

```text
When language models are given long contexts, can they reliably identify and use the relevant information regardless of where it appears?
```

## Method

中文：用中文描述作者怎么做实验。不要直接翻译原文，要说清楚“它怎么验证问题”。

English: Describe the method in Chinese. Do not directly translate the paper; explain how the paper tests the problem.

- The paper changes where relevant information appears in the input context.
- It measures model performance when the relevant information is near the beginning, middle, or end.
- It uses both realistic multi-document QA and a more controlled key-value retrieval task.
- It compares model behavior across context lengths and positions.

## System Model

中文：这里训练你把论文看成一个系统：输入是什么、输出是什么、组件是什么、LLM 在哪里。

English: This section trains you to view the paper as a system: inputs, outputs, components, and where the LLM appears.

- Inputs:
  - a question or key;
  - a long context containing relevant and irrelevant information.
- Outputs:
  - an answer or retrieved value.
- Components:
  - language model;
  - constructed input context;
  - evaluation task;
  - scoring metric.
- State:
  - no persistent runtime state is the focus; the focus is the input context layout.
- LLM role:
  - the LLM is the system under evaluation.

## Evaluation Model

中文：这是最重要的训练部分。研究能力的核心之一是看懂“实验到底证明了什么，以及没有证明什么”。

English: This is the most important training section. A core research skill is understanding what the experiment proves and what it does not prove.

- Workloads:
  - multi-document question answering;
  - key-value retrieval.
- Main variable:
  - position of relevant information in the context.
- Metrics:
  - task performance, such as answer accuracy or retrieval correctness.
- Baseline idea:
  - compare performance across different positions and context lengths.
- What it evaluates:
  - whether models use long context robustly.
- What it does not evaluate:
  - whether retrieved documents are correct before entering the context;
  - whether a context construction system selected the best evidence;
  - whether the model has persistent memory;
  - whether a production agent can solve end-to-end tasks.

## TRI Connection

中文：这里不要强行把所有东西都说成 TRI 的贡献。目标是识别“TRI 现在覆盖了什么问题，还没覆盖什么问题”。

English: Do not force everything into a TRI contribution. The goal is to identify what TRI currently covers and what it does not cover yet.

TRI Paper 3 evaluates context package construction:

```text
Did the Context Generator include relevant entities, relations, signals, events, and candidates?
```

This paper evaluates context use:

```text
Given a long context containing relevant information, does the model actually use the relevant information reliably?
```

This distinction matters because a high-quality Context Package may still fail downstream if the consumer cannot reliably attend to or use the relevant evidence.

For TRI, this suggests a future evaluation separation:

- Context construction quality: coverage, noise, candidate recall, provenance.
- Context consumption quality: whether a downstream scorer, LLM, or human uses the included evidence correctly.

## Claim Audit

中文：Claim audit 是防止过度推断的训练。每个 claim 都必须写“证据是什么”和“不证明什么”。

English: Claim audit trains you to avoid over-inference. Every claim must include evidence and what it does not prove.

| Claim | Supported by what evidence | What it does not prove | TRI relevance |
|---|---|---|---|
| Long context windows do not guarantee robust context use. | Performance changes when relevant information position changes. | Does not prove all long-context models fail in all settings. | TRI should not assume bigger context package is automatically better. |
| Relevant information in the middle can be harder for models to use. | Multi-document QA and key-value retrieval results. | Does not prove the mechanism is fully understood. | TRI should consider evidence placement if using LLM consumers. |
| Evaluation should vary evidence position. | The paper's protocol exposes position sensitivity. | Does not evaluate retrieval quality. | TRI future LLM-consumer eval can include evidence ordering tests. |
| Key-value retrieval is useful as a controlled diagnostic. | It isolates the retrieval-from-context behavior. | Does not fully represent real incident analysis. | TRI can use synthetic diagnostics carefully, with clear boundaries. |
| Context use and context construction are different problems. | The paper assumes the relevant information is present and tests usage. | Does not solve context generation itself. | TRI Paper 3 currently focuses more on construction than consumption. |

## Reusable Idea

The most reusable idea is to vary one controlled property of context while holding other factors stable.

For TRI, a similar experiment pattern could be:

```text
Keep Context Package facts constant, vary evidence ordering or grouping, then test downstream judgement consistency.
```

This should be treated as future work, not as a current Paper 3 claim.

## Open Questions

- Does TRI need a separate "context consumption evaluation" after Paper 3?
- If an LLM consumes a TRI Context Package, should evidence ordering be part of the interface contract?
- How can TRI test context use without turning Paper 3 into an LLM RCA paper?

## Reading Notes

中文：下面这部分由你读论文时填写。每个小节先写中文即可，英文关键词保留原词。

English: Fill the following sections while reading. Chinese notes are enough at first; keep key English terms in English.

### Abstract

中文笔记 / Chinese notes:

English keywords:

### Introduction

中文笔记 / Chinese notes:

English keywords:

### Evaluation Setup

中文笔记 / Chinese notes:

English keywords:

### Main Results

中文笔记 / Chinese notes:

English keywords:

### Limitations

中文笔记 / Chinese notes:

English keywords:

## Beginner Self-Check / 新人自检

完成后回答：

After finishing, answer:

- 中文：我能否用 3 句话解释这篇论文研究什么？
- English: Can I explain what this paper studies in three sentences?
- 中文：我能否说清楚 multi-document QA 和 key-value retrieval 的区别？
- English: Can I explain the difference between multi-document QA and key-value retrieval?
- 中文：我是否知道这篇论文证明了什么、不证明什么？
- English: Do I know what this paper proves and what it does not prove?
- 中文：我是否能说明它和 TRI 的关系，但不过度牵强？
- English: Can I explain its relationship to TRI without forcing the connection?
