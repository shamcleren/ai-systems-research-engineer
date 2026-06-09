# Week 4 TODO: Memory and State / 第 4 周 TODO: 记忆与状态

## Status / 状态

中文：Week 3 已完成并归档。Week 4 正式进入 `Memory and State` 周期。

English: Week 3 is closed and archived. Week 4 starts the `Memory and State` cycle.

## How to Use This TODO / 如何使用这份 TODO

中文：你只需要在本文件里一步步填写答案。不要来回翻 paper note、glossary 或其他文档。你完成后，把本文件交给 mentor review；mentor 再负责把稳定内容整理到 paper note、memory/state taxonomy、month-1 review 和 TRI note。

English: Fill answers step by step in this file only. Do not jump between the paper note, glossary, or other documents. After you finish, send this TODO to the mentor for review; the mentor will organize stable content into the paper note, memory/state taxonomy, month-1 review, and TRI note.

## Goal / 目标

中文：本周训练的研究能力是区分 retrieval context、working memory、long-term memory、conversation history 和 structured state。目标不是掌握所有 agent memory 框架，而是能清楚说明一段信息在系统里到底是临时上下文、可检索记忆、长期记忆，还是显式状态。

English: This week trains memory/state boundary reasoning: distinguishing retrieval context, working memory, long-term memory, conversation history, and structured state. The goal is not to master every agent-memory framework, but to explain what role a piece of information plays inside an AI system.

## Source / 阅读材料

中文：主读 MemGPT。仓库里如果还没有本地 PDF，本周可以先使用官方 PDF；之后再把 PDF 放到 `docs/papers/`。

English: Read MemGPT as the main paper. If the local PDF has not been added to the repository yet, use the official PDF first and add the local copy later.

- Local PDF target / 本地 PDF 目标路径：`docs/papers/2310.08560-memgpt.pdf`
- Source traceability / 来源追溯: https://arxiv.org/abs/2310.08560
- Official PDF / 官方 PDF: https://arxiv.org/pdf/2310.08560
- Paper: `MemGPT: Towards LLMs as Operating Systems`
- Authors: Charles Packer, Vivian Fang, Shishir G. Patil, Kevin Lin, Sarah Wooders, Joseph E. Gonzalez
- Optional reference / 可选参考: `Generative Agents: Interactive Simulacra of Human Behavior`, only when you want a contrast between agent behavior and memory-system design.

## Week 3 to Week 4 Bridge / 从第 3 周到第 4 周

中文：Week 1 关注信息已经在上下文里时，LLM 是否能用好。Week 2 关注哪些信息会被检索进上下文。Week 3 关注被选进来的上下文是否太长、太吵、位置不好。Week 4 继续追问：哪些信息应该跨调用、跨任务、跨会话被保存下来，以及它们应该以什么形式保存。

English: Week 1 studied whether an LLM can use information already in context. Week 2 studied which information gets retrieved into context. Week 3 studied whether selected context is too long, noisy, or poorly positioned. Week 4 asks what information should persist across calls, tasks, and sessions, and in what form.

Core distinction / 核心区分:

```text
context:
  information visible in the current model input

memory:
  information stored, retrieved, updated, and reused by the system

structured state:
  explicit machine-readable state maintained by the system
```

---

## Step-by-Step Execution / 一步步执行

### Step 1: Title and Abstract / 标题和摘要

- [ ] Done

#### What to Read / 读什么

中文：只读标题和 Abstract。不要读方法部分。目标是理解为什么作者把 LLM 类比成 operating system。

English: Read only the title and Abstract. Do not read the method section yet. The goal is to understand why the authors compare LLMs to operating systems.

#### Chinese Reading Guide / 中文导读

中文：标题里的 `Towards LLMs as Operating Systems` 不是说 LLM 真的是操作系统，而是说 LLM 应该像操作系统一样管理有限的上下文窗口、外部存储、函数调用和任务状态。Abstract 的核心是：LLM 的 context window 有限，但实际任务需要更长的历史、更大的文档和更持久的记忆；MemGPT 试图通过 memory hierarchy 和 virtual context management 让 LLM 管理比上下文窗口更大的信息空间。

English: `Towards LLMs as Operating Systems` does not mean an LLM literally becomes an operating system. It means the LLM manages limited context, external storage, function calls, and task state like an operating-system-style controller.

#### What to Write / 写什么

中文：写 3 句话：这篇论文研究什么问题、为什么重要、作者大概怎么做。

English: Write three sentences: what problem the paper studies, why it matters, and roughly what the authors do.

#### Your Answer / 你的回答

1. 这篇论文研究什么问题:

   ```text
   TODO
   ```

2. 为什么这个问题重要:

   ```text
   TODO
   ```

3. 作者大概怎么做:

   ```text
   TODO
   ```

---

### Step 2: First Keywords / 第一批关键词

- [ ] Done

#### What to Read / 读什么

中文：读 Abstract 和 Introduction。先不要深入算法，只抽关键词。

English: Read the Abstract and Introduction. Do not go deep into algorithms yet; extract terms first.

#### Chinese Reading Guide / 中文导读

中文：本周关键词分四类：memory 层级、state 边界、系统机制、评估任务。每个词先写粗糙中文解释即可。

English: This week's terms fall into four groups: memory hierarchy, state boundaries, system mechanisms, and evaluation tasks. Rough explanations are enough for now.

Candidate terms / 候选术语:

```text
context window
main context
external context
virtual context management
memory hierarchy
working memory
recall memory
archival memory
long-term memory
conversation history
structured state
memory retrieval
memory update
function call
interrupt
system state
agent state
task state
persona
human memory
paging
```

#### What to Write / 写什么

中文：至少选 14 个术语，每个写一句中文解释。

English: Pick at least 14 terms and write one Chinese explanation for each.

#### Your Answer / 你的回答

| English term | 中文解释 |
|---|---|
| context window | TODO |
| main context | TODO |
| external context | TODO |
| virtual context management | TODO |
| memory hierarchy | TODO |
| working memory | TODO |
| recall memory | TODO |
| archival memory | TODO |
| long-term memory | TODO |
| conversation history | TODO |
| structured state | TODO |
| memory retrieval | TODO |
| memory update | TODO |
| function call | TODO |

---

### Step 3: Problem Definition / 问题定义

- [ ] Done

#### What to Read / 读什么

中文：读 Introduction，只找一个问题：为什么仅靠把更多内容塞进 context window 不够？

English: Read the Introduction and answer one question: why is stuffing more content into the context window not enough?

#### Chinese Reading Guide / 中文导读

中文：Week 3 的压缩是处理“当前 prompt 太长”。Week 4 的 memory 是处理“信息生命周期太长”。有些信息不应该每次都全部塞进 prompt，而应该被系统保存、检索、更新、淘汰或结构化维护。

English: Week 3 compression handled prompts that are too long. Week 4 memory handles information whose lifecycle is longer than one prompt. Some information should be stored, retrieved, updated, evicted, or maintained as structured state rather than always stuffed into the prompt.

#### What to Write / 写什么

中文：用 5-7 句话说明 MemGPT 的问题定义。必须包含 `limited context window`、`long-running interaction`、`external storage`、`state management` 四个概念。

English: In 5-7 sentences, explain MemGPT's problem definition. Include `limited context window`, `long-running interaction`, `external storage`, and `state management`.

#### Your Answer / 你的回答

```text
TODO
```

---

### Step 4: Memory Taxonomy / 记忆分类

- [ ] Done

#### What to Read / 读什么

中文：读方法中 memory hierarchy / context management 相关部分。目标是分类，不是复现实现细节。

English: Read the method sections about memory hierarchy and context management. The goal is taxonomy, not implementation reproduction.

#### Chinese Reading Guide / 中文导读

中文：不要把所有“能被模型看到的信息”都叫 memory。当前 prompt 里的 retrieved passages 是 context；对话日志是 history；跨会话保存并可检索的信息更接近 long-term memory；系统显式维护的 JSON、数据库记录、任务状态更接近 structured state。

English: Do not call every visible piece of information memory. Retrieved passages in the current prompt are context. Chat logs are history. Persisted and retrievable cross-session information is closer to long-term memory. Explicit JSON/database/task state is closer to structured state.

#### What to Write / 写什么

中文：完成下面表格。重点写“生命周期”和“谁负责更新”。

English: Complete the table below. Focus on lifecycle and who updates it.

#### Your Answer / 你的回答

| Type | 中文定义 | 生命周期 | 谁负责更新 | 例子 |
|---|---|---|---|---|
| retrieval context | TODO | TODO | TODO | TODO |
| working memory / main context | TODO | TODO | TODO | TODO |
| conversation history | TODO | TODO | TODO | TODO |
| recall memory | TODO | TODO | TODO | TODO |
| archival memory | TODO | TODO | TODO | TODO |
| long-term memory | TODO | TODO | TODO | TODO |
| structured state | TODO | TODO | TODO | TODO |

---

### Step 5: System Model / 系统模型

- [ ] Done

#### What to Read / 读什么

中文：看论文里的 system / architecture 图和方法描述。目标是把系统拆成组件和数据流。

English: Read the system/architecture figure and method description. Break the system into components and data flow.

#### Chinese Reading Guide / 中文导读

中文：MemGPT 可以先看成一个 memory manager。LLM 不只是回答用户，还可以通过函数调用管理外部记忆：搜索、写入、更新、把信息搬入或搬出 main context。这里的关键边界是：什么东西在当前 context window 里，什么东西在外部 storage 里，什么机制决定信息何时进入 context。

English: MemGPT can be viewed as a memory manager. The LLM does not only answer the user; it can use function calls to manage external memory: search, write, update, and move information into or out of the main context.

#### What to Write / 写什么

中文：画一个纯文本系统图。必须包含 user input、LLM processor、main context、memory functions、recall storage、archival storage、response。

English: Draw a text-only system diagram. Include user input, LLM processor, main context, memory functions, recall storage, archival storage, and response.

#### Your Answer / 你的回答

```text
TODO
```

---

### Step 6: Method Boundary / 方法边界

- [ ] Done

#### What to Read / 读什么

中文：读方法部分里 function call、memory operation、event loop 或 control flow 相关描述。不要纠结每个函数名，先找边界。

English: Read the method description around function calls, memory operations, event loop, or control flow. Do not focus on every function name; identify boundaries.

#### Chinese Reading Guide / 中文导读

中文：这一步要回答：MemGPT 到底是在训练一个新模型，还是在 inference time 用系统机制管理 memory？它的核心机制是让 LLM 通过外部函数和 memory tiers 交互，不是把所有长期信息直接塞到 prompt 里。

English: Answer whether MemGPT trains a new model or uses inference-time system mechanisms to manage memory. Its key mechanism is interaction between the LLM and memory tiers through external functions, not stuffing all long-term information into the prompt.

#### What to Write / 写什么

中文：回答下面 5 个问题。

English: Answer the five questions below.

#### Your Answer / 你的回答

1. MemGPT 是否需要训练一个新的 base LLM?

   ```text
   TODO
   ```

2. MemGPT 的 memory operation 是在什么时候发生的?

   ```text
   TODO
   ```

3. 哪些信息留在 main context?

   ```text
   TODO
   ```

4. 哪些信息应该进入 external memory?

   ```text
   TODO
   ```

5. function call 在系统里扮演什么角色?

   ```text
   TODO
   ```

---

### Step 7: Evaluation Model / 评估模型

- [ ] Done

#### What to Read / 读什么

中文：读 Experiments / Evaluation。只回答：作者用什么任务证明 memory management 有用？baseline 是什么？metric 是什么？

English: Read Experiments / Evaluation. Answer only: what tasks show memory management is useful? What are the baselines? What are the metrics?

#### Chinese Reading Guide / 中文导读

中文：不要只写“MemGPT 效果更好”。要拆成 workload、baseline、metric 和 claim boundary。memory 系统最容易过度声称“长期记忆有效”，但评测通常只覆盖特定任务、特定数据和特定交互长度。

English: Do not only write "MemGPT works better." Break evaluation into workload, baseline, metric, and claim boundary. Memory systems are easy to overclaim; evaluations usually cover specific tasks, data, and interaction lengths.

#### What to Write / 写什么

中文：完成下面表格。

English: Complete the table below.

#### Your Answer / 你的回答

| Evaluation item | 中文回答 |
|---|---|
| workloads / 任务 | TODO |
| baselines / baseline | TODO |
| variables / 变量 | TODO |
| metrics / 指标 | TODO |
| what it proves / 能证明什么 | TODO |
| what it does not prove / 不能证明什么 | TODO |

---

### Step 8: Claim Audit / 主张审计

- [ ] Done

#### What to Read / 读什么

中文：回看 Abstract、Conclusion、Evaluation。找 3 个可以被实验支持的 claim，再找 3 个不能过度泛化的 claim。

English: Revisit Abstract, Conclusion, and Evaluation. Find three claims supported by experiments and three claims that should not be overgeneralized.

#### Chinese Reading Guide / 中文导读

中文：claim audit 的重点是保守表达。例如可以说“在论文评测任务上，显式 memory management 改善了长交互或长文档处理能力”；不要直接说“MemGPT 解决了 LLM 长期记忆问题”。后者太大。

English: Claim audit requires conservative wording. For example, say "on the paper's evaluated tasks, explicit memory management improves long-interaction or long-document handling"; do not directly say "MemGPT solves long-term memory for LLMs." That is too broad.

#### What to Write / 写什么

中文：完成 6 条 claim audit。

English: Complete six claim-audit items.

#### Your Answer / 你的回答

Supported claims / 有实验支持的主张:

1. ```text
   TODO
   ```
2. ```text
   TODO
   ```
3. ```text
   TODO
   ```

Overclaim risks / 容易过度泛化的主张:

1. ```text
   TODO
   ```
2. ```text
   TODO
   ```
3. ```text
   TODO
   ```

---

### Step 9: TRI Connection / 连接 TRI

- [ ] Done

#### What to Read / 读什么

中文：不用读新材料。回顾 Week 2 和 Week 3 对 TRI Context Package 的判断。

English: No new reading. Revisit the Week 2 and Week 3 interpretation of TRI Context Package.

#### Chinese Reading Guide / 中文导读

中文：本周核心判断：TRI Context Package 不应该直接叫 long-term memory。它更像 structured retrieval context：由检索/生成流程产生，有 schema、provenance、evidence、metadata，服务于当前实验或当前回答。它可能被持久化，但“被持久化”不等于“就是 memory”。

English: The core judgment this week: TRI Context Package should not be directly called long-term memory. It is closer to structured retrieval context: produced by retrieval/generation, with schema, provenance, evidence, and metadata, serving a current experiment or answer. Persistence alone does not make it memory.

#### What to Write / 写什么

中文：完成下面判断表，然后写一个 5 句话的 TRI note 草稿。

English: Complete the judgment table, then write a five-sentence TRI note draft.

#### Your Answer / 你的回答

| Question | 中文判断 |
|---|---|
| TRI Context Package 是 retrieval context 吗? | TODO |
| TRI Context Package 是 working memory 吗? | TODO |
| TRI Context Package 是 long-term memory 吗? | TODO |
| TRI Context Package 是 structured state 吗? | TODO |
| 最保守的命名是什么? | TODO |

TRI note draft / TRI 笔记草稿:

```text
TODO
```

---

### Step 10: Month-1 Review / 第一个月复盘

- [ ] Done

#### What to Read / 读什么

中文：不用读论文。回看 Week 1-4 的 TODO 结论即可。

English: No paper reading. Review the conclusions from Week 1-4 TODOs.

#### Chinese Reading Guide / 中文导读

中文：这个复盘不是流水账。目标是把四周连成一条 context-engineering 主线：context use、context selection、context compression、memory/state。

English: This review is not a diary. Connect the four weeks into one context-engineering path: context use, context selection, context compression, and memory/state.

#### What to Write / 写什么

中文：每周写 2-3 句话，最后写一个“我现在如何理解 Context Engineering”的 5 句话总结。

English: Write 2-3 sentences for each week, then a five-sentence summary of how you now understand Context Engineering.

#### Your Answer / 你的回答

Week 1: Context Use / Lost in the Middle

```text
TODO
```

Week 2: Context Selection / RAG

```text
TODO
```

Week 3: Context Compression / LongLLMLingua

```text
TODO
```

Week 4: Memory and State / MemGPT

```text
TODO
```

Month-1 summary / 第一个月总结:

```text
TODO
```

---

## Completion Checklist / 完成检查清单

中文：完成 Week 4 时，至少应该产出下面 3 个 artifact。先写在本 TODO 里即可，review 后再拆到正式笔记。

English: By the end of Week 4, produce at least the three artifacts below. Write them inside this TODO first; after review, move stable content into formal notes.

- [ ] One MemGPT paper note / 一份 MemGPT paper note
- [ ] One memory/state taxonomy / 一份 memory/state taxonomy
- [ ] One month-1 review / 一份第一个月复盘

## Mentor Review Request / 交给 mentor review 时问什么

中文：完成后，把这 4 个问题发给 mentor:

English: After completion, send these four questions to the mentor:

```text
1. 我对 retrieval context、memory、structured state 的边界是否清楚?
2. 我有没有把 conversation history 错当成 memory?
3. 我对 MemGPT claim 的表述是否过度泛化?
4. TRI Context Package 应该叫 structured retrieval context、working state，还是别的名字?
```
