# Week 1: Paper Anatomy and Context Use / 第 1 周：论文结构与上下文使用

> 中文：如果你只想照着步骤做，优先打开 `docs/todos/WEEK-01-TODO.md`。
>
> English: If you only want executable steps, start with `docs/todos/WEEK-01-TODO.md`.

## Purpose

中文：本周开始建立论文阅读习惯。目标不是掌握所有技术细节，而是学会拆解一篇 AI systems paper：problem、method、experiment、claim、limitation。

English: This week starts the paper-reading habit. The goal is not to master every technical detail, but to learn how to break down an AI systems paper into problem, method, experiment, claim, and limitation.

## Main Paper

```text
Lost in the Middle: How Language Models Use Long Contexts
Nelson F. Liu, Kevin Lin, John Hewitt, Ashwin Paranjape, Michele Bevilacqua, Fabio Petroni, Percy Liang
arXiv:2307.03172
TACL 2023
```

Links:

- arXiv: https://arxiv.org/abs/2307.03172
- TACL: https://direct.mit.edu/tacl/article/doi/10.1162/tacl_a_00638/119630/Lost-in-the-Middle-How-Language-Models-Use-Long

## Why This Paper First

中文：这篇适合做第一篇，因为它讨论的是 context use，而不只是 retrieval 或模型结构。

English: This is a good first paper because it focuses on context use, not only retrieval or model architecture.

It asks a concrete evaluation question:

```text
When a model receives a long context, does it actually use the relevant information reliably?
```

This connects directly to Context Engineering. TRI currently builds Context Packages, but a downstream model, scorer, or human still has to use that context. This paper helps separate two questions:

- Did the system include the relevant context?
- Did the consumer actually use the relevant context?

TRI Paper 3 mostly evaluates the first question. This paper is useful because it trains the second question.

## Reading Scope

中文：按这个顺序读，不要一开始就从头硬啃到尾。

English: Read in this order. Do not force a full linear read from the beginning.

1. Title, abstract, and introduction.
2. Figure 1 and the nearby explanation.
3. Task setup sections for multi-document QA and key-value retrieval.
4. Main result sections.
5. Limitations or discussion.

Do not try to understand every model-specific detail in the first pass.

## Required Outputs

### 1. Structured Paper Note

Fill:

```text
docs/notes/papers/2026-05-14-lost-in-the-middle.md
```

Minimum completion standard:

- metadata completed;
- at least 15 bilingual keywords;
- one-sentence thesis;
- system model;
- evaluation model;
- TRI connection;
- claim audit.

### 2. Glossary Update

Fill:

```text
docs/glossary/context-engineering-glossary.md
```

Add at least 20 terms from this paper.

### 3. TRI Connection Note

In the paper note, answer:

```text
TRI Paper 3 evaluates context package construction. This paper evaluates context use. What is the difference?
```

### 4. Claim Audit

Write at least 5 rows:

```text
Claim | Supported by what evidence | What it does not prove | TRI relevance
```

## Suggested Time Split

- 60 min: abstract + introduction, with translation support.
- 90 min: task setup and figures.
- 90 min: main results.
- 90 min: fill structured note.
- 60 min: glossary.
- 60 min: TRI connection and claim audit.

## Done Criteria

Week 1 is done when:

- the paper note is filled;
- the glossary has at least 20 entries;
- the TRI connection note is written;
- one open question is recorded for next week.

## Mentor Review Prompt

After filling the note, ask:

```text
请你按研究 mentor 的标准 review 我 Week 1 的 Lost in the Middle 笔记，重点看：
1. 我是否抓住了 problem / method / evaluation / claim；
2. bilingual glossary 是否准确；
3. TRI connection 是否牵强；
4. claim audit 有没有过度推断。
```
