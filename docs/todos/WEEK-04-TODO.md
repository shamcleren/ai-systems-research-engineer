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

- [x] Done

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
   LLM 的固定长度上下文窗口限制了长对话和长文档分析，MemGPT 研究如何在不扩展窗口的情况下，通过模拟操作系统的内存管理，让 LLM 具备看似无限的上下文。
   ```

2. 为什么这个问题重要:

   ```text
   直接扩展上下文窗口有二次方计算成本，且 Lost in the Middle 已证明窗口变长不等于模型能用好。需要一种替代方案：不是让窗口更大，而是让有限窗口里的信息更智能地流动。
   ```

3. 作者大概怎么做:

   ```text
   借鉴 OS 虚拟内存机制（paging），设计 memory hierarchy：main context（类比物理内存）和 external context（类比磁盘）。让 LLM 通过 function call 自己管理记忆——写入、搜索、更新外部存储，在不同 memory tier 之间搬运信息，用 interrupts 管理控制流。在超长文档分析和多轮对话 agent 两个场景评测。
   ```

---

### Step 2: First Keywords / 第一批关键词

- [x] Done

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
| context window | 上下文窗口：LLM 一次推理能处理的最大 token 数（如 GPT-4 的 8k、GPT-4 Turbo 的 128k）。MemGPT 把它类比为操作系统的"物理内存"——有限且珍贵。 |
| main context | 主上下文：LLM 当前能看到的 prompt tokens，类比 OS 的物理内存/RAM。在 MemGPT 中分为三段：system instructions（只读）、working context（可读写）、FIFO queue（滚动消息队列）。 |
| external context | 外部上下文：存放在 LLM 上下文窗口之外的所有信息，类比 OS 的磁盘。必须通过 function call 显式搬进 main context 才能被 LLM 看到。 |
| virtual context management | 虚拟上下文管理：MemGPT 的核心技术。借鉴 OS 虚拟内存的 paging 机制，在 main context 和 external context 之间搬运数据，让 LLM 产生"上下文是无限的"错觉。 |
| memory hierarchy | 记忆层级：不同速度和容量的记忆层级的组合。MemGPT 设计了两层——main context（快但小）和 external context（慢但大），类比 OS 的内存/磁盘层级。 |
| working context | 工作上下文：main context 中的可读写区域，通过 function call 写入。在对话场景中用于存储用户关键信息、偏好、重要事实，保证 agent 跨对话保持一致。 |
| recall memory | 召回记忆：MemGPT 的外部存储之一，存储完整的对话历史消息（所有 user message + agent response）。通过 function call 搜索后可将历史消息重新插入 FIFO queue。类比"聊天记录数据库"。 |
| archival memory | 归档记忆：MemGPT 的外部存储之一，用于存储任意长度的文本对象（如文档、Wikipedia 文章）。支持向量搜索（pgvector），LLM 可自主搜索、分页浏览结果。 |
| FIFO queue | 先进先出消息队列：main context 中的滚动消息历史。新消息追加到队尾，满时触发 eviction——队首消息被移出并压缩为递归摘要。被移出的消息存入 recall storage 供后续检索。 |
| conversation history | 对话历史：agent 与用户之间的多轮和多会话交互记录。MemGPT 将其存储在 recall storage 中，可以被搜索检索回 main context。与"只存在于当前 FIFO queue"的历史不同——它跨会话持久化。 |
| function call | 函数调用：LLM 输出被解析为结构化函数调用（如搜索外部存储、写入 working context），由 function executor 执行后结果回传。这是 LLM 自主管理记忆的关键机制——LLM 决定何时搜索、写入、更新。 |
| memory retrieval | 记忆检索：LLM 通过 function call 从 external context（recall/archival storage）中搜索并取回相关信息的过程。支持分页（pagination），避免一次检索结果溢出上下文窗口。 |
| memory update | 记忆更新：LLM 自主修改 main context 中的 working context 内容（如 Figure 4 中将"boyfriend James"更新为"ex-boyfriend James"）。使 agent 的知识随对话推进而演进。 |
| interrupt / memory pressure | 中断/内存压力：当 FIFO queue 接近上下文窗口上限时（如 70%），queue manager 插入系统警告提醒 LLM 即将触发 eviction。LLM 可在被强制 evict 之前主动把重要信息搬到 working context 或 archival storage。 |

---

### Step 3: Problem Definition / 问题定义

- [x] Done

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
LLM 的上下文窗口是一个固定长度的受限资源：GPT-4 只有 8k token，最多容纳约 140 条短消息，远不足以支撑长对话或长文档分析。

直接扩展上下文窗口不是好方案——transformer 自注意力机制的计算成本随长度二次增长，且 Lost in the Middle 已经证明：即使窗口变大，模型也未必能用好长上下文中的信息。

但实际应用需要超长交互：对话 agent 要记住几周甚至几个月前的对话内容；文档分析要处理远超窗口大小的文件（如 SEC 财报可达百万 token）。

这暴露了"信息生命周期"问题——有些信息不应该每次都全部塞进 prompt，而应该被系统持久保存、按需检索、适时更新、自动淘汰。

MemGPT 的答案是不扩展窗口本身，而是把外部存储接入 LLM——让 LLM 通过 function call 自主管理自己的上下文，像 OS 管理虚拟内存一样在"快但小"的 main context 和"慢但大"的 external storage 之间搬运数据。

核心概念：有限的 context window 是物理内存；external storage（recall + archival）是磁盘；function call 是 paging 机制；interrupt 是内存压力信号。LLM 不再被动接受 prompt，而是主动管理自己的"记忆工作区"。
```

---

### Step 4: Memory Taxonomy / 记忆分类

- [x] Done

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
| retrieval context | 按 query 从外部知识库检索回来、暂时放在 main context 里的文档或段落。LLM 当前推理需要用到的材料。 | 单次推理周期内有效。用完即被 FIFO queue eviction 淘汰，或 LLM 主动清除。 | LLM 通过 function call 触发检索，retriever 执行查询。 | MemGPT 中 LLM 调用 archival_storage.search("nobel physics") 取回的 Wikipedia 段落。 |
| working memory / main context | main context 中可读写的固定大小文本块，存储关于用户和 agent 的关键事实、偏好、目标。类比 OS 的工作内存。 | 跨消息、跨会话持续存在（除非 LLM 主动修改或替换）。不被 FIFO queue 的 eviction 影响。 | LLM 通过 function call（如 working_context.append / replace）自主读写。 | "Birthday is February 7"、"Boyfriend named James" → "Ex-boyfriend named James"（Figure 1/4）。 |
| conversation history | 用户与 agent 的所有历史消息记录。在 MemGPT 中分层存储：当前窗口内消息在 FIFO queue，完整历史在 recall storage。 | FIFO queue 内的消息：当前会话窗口周期，eviction 时被移出。Recall storage 内的消息：跨会话永久保存。 | Queue manager 自动追加新消息；eviction 时自动把旧消息压缩为递归摘要。 | Figure 2：MemGPT 搜索 recall storage 找到六个月前的"six flags"对话记录。 |
| recall memory | MemGPT 的 external storage 之一，专门存储完整对话消息（user + agent + system messages），支持 LLM 通过 function call 按关键词/时间搜索和分页浏览。 | 跨会话永久保存，不会被上下文窗口限制淘汰。 | Queue manager 自动写入每条消息；LLM 通过 recall_storage.search 检索。 | Deep Memory Retrieval 任务：agent 搜索前 5 个 session 的对话内容来回答问题。 |
| archival memory | MemGPT 的 external storage 之一，存储任意长度的文本对象（文档、文章、知识库条目）。支持向量搜索（pgvector + HNSW），LLM 可自主分页浏览结果。 | 跨调用持久化，直到 LLM 或系统主动删除。独立于对话生命周期。 | LLM 通过 function call 写入/搜索；数据由系统预先加载或用户上传。 | Document QA 任务：Wikipedia 全部文章预先存入 archival storage，LLM 调用 archival_storage.search 查找答案。 |
| long-term memory | 广义概念：跨时间、跨任务、跨会话持续存在并可被系统检索和使用的信息。在 MemGPT 中是 recall + archival + working context 的联合效果，不是单独的一个模块。 | 理论上无限期持久化，直到被主动删除或覆写。 | LLM 自主决定何时保存、何时检索。更新通过 function call 完成。 | Multi-session chat 中 agent 记住用户几天前提到的生日和男友名字，在新会话中主动提及。 |
| structured state | 系统显式维护的机器可读状态，如 JSON 对象、数据库记录、任务状态机。不同于非结构化文本——它有明确的 schema 和字段。 | 由系统控制，可以在推理之间、会话之间、任务之间持久化。 | 系统运行时自动更新，不依赖 LLM 的文本理解和 function call。 | MemGPT 中的 queue manager 状态（当前 token 计数、eviction 阈值）、task 的完成状态。注意：MemGPT 论文未强调这个概念，它是 Week 4 引入的分析概念。 |

---

### Step 5: System Model / 系统模型

- [x] Done

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
                        ┌─────────────────────────────┐
                        │     LLM Processor           │
                        │  (fixed context window,     │
                        │   e.g. GPT-4 8k tokens)     │
                        └──────────┬──────────────────┘
                                   │
                    reads/writes   │  generates output
                                   │
          ┌────────────────────────┴──────────────────────────┐
          │                                                    │
          ▼                                                    ▼
┌─────────────────────┐                          ┌─────────────────────────┐
│   MAIN CONTEXT      │                          │   FUNCTION EXECUTOR     │
│   (prompt tokens)   │                          │   parses output as      │
│                     │                          │   function calls        │
│ ┌─────────────────┐ │                          └───────────┬─────────────┘
│ │System Instructions│ │                                      │
│ │ (read-only)      │ │                         executes     │
│ ├─────────────────┤ │                         ┌────────────┼────────────┐
│ │Working Context   │◄├── write via functions ──┤            │            │
│ │(read/write)      │ │                         │            │            │
│ ├─────────────────┤ │                         ▼            ▼            ▼
│ │FIFO Queue        │ │              ┌──────────────┐ ┌──────────────┐ ┌──────────┐
│ │(rolling history) │◄├─ append ────│    QUEUE     │ │   RECALL     │ │ ARCHIVAL │
│ └─────────────────┘ │              │   MANAGER    │ │   STORAGE    │ │ STORAGE  │
└─────────────────────┘              │              │ │ (message DB) │ │(doc DB)  │
          ▲                          │ - eviction   │ │              │ │          │
          │                          │ - summary    │ │ search/read  │ │ search/  │
          │                          │ - warnings   │ │ via functions│ │ read/write│
          │                          └──────┬───────┘ └──────┬───────┘ └────┬─────┘
          │                                 │                │              │
          │                                 │                │              │
    ┌─────┴──────┐                    ┌─────┴──────┐         │              │
    │   USER     │                    │  RESPONSE  │         │              │
    │   INPUT    │                    │  to user   │         │              │
    └────────────┘                    └────────────┘         │              │
                                                              │              │
                                              EXTERNAL CONTEXT ("disk")

数据流说明：
1. User input → append to FIFO queue (via queue manager)
2. Queue manager concatenates main context → LLM processor reads
3. LLM generates output → function executor parses
4. If output is a function call → execute (search/update recall or archival),
   result fed back to main context → chain or yield to user
5. If output is a yield → response delivered to user
6. Queue manager monitors token count → triggers memory pressure warning
   at ~70% full, triggers eviction + recursive summary at ~100% full
```

---

### Step 6: Method Boundary / 方法边界

- [x] Done

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
   不需要。MemGPT 完全是一个 inference-time 的系统层封装，不改动底层 LLM 的权重或架构。它通过精心设计的 system instructions + function schema，让已有的 LLM（GPT-4、GPT-3.5 等）学会像 OS 一样管理自己的记忆。本质是 prompt engineering + 外部存储编排，不是模型训练。
   ```

2. MemGPT 的 memory operation 是在什么时候发生的?

   ```text
   在每次 LLM 推理周期中发生。LLM 读取 main context → 生成输出 → function executor 解析。如果输出是 function call（如搜索 archival storage、更新 working context），executor 执行操作并将结果反馈回 main context，触发下一轮推理（function chaining）。此外，queue manager 在检测到 token 超过阈值时（70% 警告、100% eviction）也会自动执行 memory operation（递归摘要、移出旧消息）。
   ```

3. 哪些信息留在 main context?

   ```text
   三段：① System Instructions（只读）：MemGPT 的行为规则、memory hierarchy 说明、function schema；② Working Context（可读写）：用户关键事实、偏好、agent 的当前目标和 persona 信息；③ FIFO Queue（滚动窗口）：最近的用户消息、agent 回复、系统消息和 function call 结果的滚动历史。
   ```

4. 哪些信息应该进入 external memory?

   ```text
   两类：① Recall Storage：全部对话历史消息（所有 session 的所有 user/agent/system message），被 FIFO queue evict 后的消息永久存于此；② Archival Storage：任意长度的文档、文章、知识库条目（如 Wikipedia dump），可通过向量搜索按语义查找。关键原则：当前不需要但将来可能需要的信息 → external memory；当前推理直接需要的信息 → main context。
   ```

5. function call 在系统里扮演什么角色?

   ```text
   Function call 是 MemGPT 的核心机制，扮演三个角色：① Paging 机制——在 main context 和 external storage 之间搬运数据（类比 OS 的 page fault / page swap）；② 自主决策接口——LLM 自己决定何时搜索、写入、更新记忆，不需要外部调度器；③ 控制流管理——通过 function chaining（request_heartbeat）连续执行多步操作，通过 yield 交还控制权给用户。简言之，function call 让 LLM 从"被动接受 prompt 的回答者"变成"主动管理自己记忆的操作系统"。
   ```

---

### Step 7: Evaluation Model / 评估模型

- [x] Done

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
| workloads / 任务 | 两大领域：(1) 对话 agent——Deep Memory Retrieval（跨 5 个 session 后回答关于早期对话的问题）+ Conversation Opener（基于长期记忆生成个性化开场白）；(2) 文档分析——Document QA（NaturalQuestions-Open，K 篇 Wikipedia 文档中找答案）+ Nested KV Retrieval（多层嵌套 key-value 查找，测试多跳检索能力）。 |
| baselines / baseline | 固定上下文 baseline：直接用 GPT-3.5/4/4-Turbo 的原始上下文窗口（不带 MemGPT），对话任务中给一个 lossy 的递归摘要替代完整历史；文档任务中用截断（truncation）塞入更多文档。另外 Zero-shot（无 context）和 Original Prompt（完整 context）作为上下界参考。 |
| variables / 变量 | (1) 底层模型：GPT-3.5 vs GPT-4 vs GPT-4 Turbo；(2) 文档数量 K：从 10 到 200；(3) 嵌套层级：1-3 层 KV 嵌套；(4) 是否使用 MemGPT memory management。 |
| metrics / 指标 | (1) 准确率（LLM-judge：GPT-4 判断回答是否与 gold answer 一致）；(2) ROUGE-L recall（对话回答与标准答案的重叠度，容忍回答比标准答案更冗长）；(3) CSIM（对话开场白与 persona 的语义相似度）。 |
| what it proves / 能证明什么 | (1) MemGPT 在固定上下文模型上叠加 memory management 后，文档 QA 准确率不随文档数量增加而下降（而固定上下文 baseline 需要截断，准确率下降）；(2) 对话 agent 的 deep memory retrieval 准确率显著提升（GPT-4 + MemGPT 达 92.5% vs 纯 GPT-4 的 32.1%）；(3) MemGPT 能从多个数据源 collate 信息（嵌套 KV 任务上唯一能完成 3 层嵌套的方案）；(4) LLM 可以自主管理记忆，不需要人工设计记忆检索策略。 |
| what it does not prove / 不能证明什么 | (1) 不能证明 OS 类比是最优设计——只证明了 memory hierarchy + function call 有效，未对比其他记忆架构（如 RAG 的 retriever-reader、Recurrent Memory Transformer 等）；(2) 不能证明成本效率——多步 function chaining 增加推理轮次，latency 和 API 费用可能更高；(3) 不能证明在所有文档类型上都有效——只在 Wikipedia 和合成 KV 上测试；(4) 不能证明 LLM 的记忆管理决策总是最优——论文承认 GPT-3.5 的 function calling 能力弱导致 MemGPT 效果差，说明机制有效性依赖底层模型能力；(5) 不能证明"长期记忆"解决了 catastrophic forgetting 或记忆冲突问题。 |

---

### Step 8: Claim Audit / 主张审计

- [x] Done

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
   Claim: 在 LLM 推理时叠加 memory hierarchy 和 function-call-based memory management，可以让固定上下文模型处理远超其窗口大小的信息量。
   Evidence: Document QA 任务中，MemGPT + GPT-4 在 K=200 时准确率不下降，而固定上下文 baseline 随着文档增加需要截断、准确率持续下降（Figure 5）。嵌套 KV 任务中，MemGPT 是唯一能完成 3 层嵌套的方案（Figure 7）。
   Does NOT prove: 不能证明这是处理超长上下文的最优方案；论文未对比其他长上下文技术（如 LongLoRA、RingAttention、prompt compression）。
   ```

2. ```text
   Claim: 跨会话记忆检索（recall storage search）能显著提升对话 agent 的一致性和知识回忆能力。
   Evidence: Deep Memory Retrieval 任务中，GPT-4 + MemGPT 准确率达 92.5%，远超固定上下文 GPT-4 的 32.1%（Table 2）。Conversation Opener 任务中 MemGPT 生成的个性化开场白语义相似度达到甚至超过人类手写水平（Table 3）。
   Does NOT prove: 只在 5 个 session 的 MSC 数据集上测试，不能证明在数十个 session 后记忆检索仍然有效；不能证明跨多月/多年的记忆衰减问题已解决。
   ```

3. ```text
   Claim: LLM 可以自主管理自己的记忆——无需人工设计记忆检索策略或外部调度器。
   Evidence: MemGPT 的 function call 完全由 LLM 自主触发（Figure 1、2、4、6、8），LLM 自己决定何时搜索 recall/archival storage、何时更新 working context、何时 yield 给用户。
   Does NOT prove: 不能证明 LLM 的记忆管理决策总是最优——GPT-3.5 版本效果显著差于 GPT-4 版本，说明自主管理能力高度依赖底层模型的 function calling 和推理能力。
   ```

Overclaim risks / 容易过度泛化的主张:

1. ```text
   危险说法: "MemGPT 让 LLM 拥有了真正的长期记忆。"
   为什么是过度泛化: MemGPT 的"长期记忆"本质上是 recall storage（对话数据库）+ archival storage（文档数据库）+ working context（可读写文本块）的组合，依赖 LLM 在推理时主动搜索和搬运。它没有训练出参数化的长期记忆，也没有解决记忆冲突、记忆淘汰、记忆一致性等 long-term memory 的核心难题。更保守的说法是"MemGPT 提供了跨会话的持久化信息存储和按需检索机制"。
   ```

2. ```text
   危险说法: "MemGPT 证明 LLM 可以作为操作系统。"
   为什么是过度泛化: OS 类比是一个概念启发，不是严格的系统等价。真正的 OS 需要管理硬件资源、进程调度、文件系统、安全隔离、并发控制等。MemGPT 只借鉴了虚拟内存 paging 这一个概念，用于上下文管理。更好的说法是"MemGPT 受 OS 虚拟内存机制启发，实现了 LLM 上下文的 tiered management"。
   ```

3. ```text
   危险说法: "有了 MemGPT，LLM 上下文窗口大小不再重要。"
   为什么是过度泛化: MemGPT 并没有消除上下文窗口限制——它只是更智能地使用有限窗口。窗口大小仍然影响：① working context 容量（能同时记住多少用户事实）；② FIFO queue 长度（最近多少轮对话能直接在窗口里看到，不需要搜索）；③ 单次检索结果能放多少内容。更大的窗口会让 MemGPT 更轻松，窗口太小则频繁触发 eviction 和检索。
   ```

---

### Step 9: TRI Connection / 连接 TRI

- [x] Done

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
| TRI Context Package 是 retrieval context 吗? | 是最接近的类型，但比普通 retrieval context 更结构化。RAG 返回的是原始文档片段，TRI CP 返回的是有 schema 的实体/关系/信号/事件/候选对象。可以叫 "structured retrieval context"——本质是 retrieval 的结果，但经过了组织和解释。 |
| TRI Context Package 是 working memory 吗? | 功能上有重叠——都在一次推理中承载当前任务所需的关键信息。但 MemGPT 的 working context 是非结构化文本块（"Birthday is Feb 7"），TRI CP 有明确的 schema、provenance、evidence 字段。如果 TRI 持久化了 CP 作为"当前实验状态"，那它就是 working memory 的角色。 |
| TRI Context Package 是 long-term memory 吗? | 不是。Long-term memory 的核心特征是"跨时间、跨任务积累并随系统演进"。TRI CP 本质上是"对当前查询生成的上下文对象"，即使被持久化到数据库，也不是系统在长期交互中逐渐积累的知识——它更像一份"按需生成的报告"。 |
| TRI Context Package 是 structured state 吗? | 最接近 structured state 的定义——它有明确的 schema、字段、provenance、metadata，是机器可读的结构化对象。区别在于：structured state 通常由系统持续维护和更新（如数据库记录），而 TRI CP 更多是"按查询生成 + 可选持久化"。如果 TRI 未来在多次实验之间共享和更新同一 CP，它就变成了 structured state。 |
| 最保守的命名是什么? | **Structured retrieval context**（结构化检索上下文）。它本质上是 retrieval 的产物，但有 schema、有 provenance、有质量元数据。与 RAG raw passages 的区别是"经过了组织"，与 long-term memory 的区别是"服务于当前任务而非跨时间积累"。 |

TRI note draft / TRI 笔记草稿:

```text
TRI Context Package 不应该被简单归类为"长期记忆"。从 MemGPT 的记忆分类角度看，它最接近 structured retrieval context：由检索和生成流程产生，有明确的 schema、provenance、evidence 和 metadata，服务于当前实验或当前回答。

它和 RAG 输出的区别是结构化程度——RAG 返回文档片段，TRI CP 返回实体/关系/事件等有组织的研究对象。它和 long-term memory 的区别是生命周期——TRI CP 是为特定查询按需生成的，不是系统在长期交互中逐渐积累和演进的知识。

如果 TRI 未来需要持久化 CP 并在多次实验间共享和更新，它就进入了 working memory / structured state 的范畴。但当前阶段，最保守且最准确的命名是 structured retrieval context：retrieval 是它的来源，structured 是它区别于 raw passages 的核心价值。

这一定位对 TRI 的工程决策很重要：如果 CP 是 retrieval context，那评测应该关注检索质量（recall、precision、noise ratio）；如果 CP 是 long-term memory，那评测还需要关注记忆一致性、更新冲突、信息淘汰策略——这些目前不是 TRI 需要承担的责任。
```

---

### Step 10: Month-1 Review / 第一个月复盘

- [x] Done

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
模型能不能用好已经在上下文里的信息，取决于信息放在什么位置。信息在开头和结尾时模型表现最好，在中间时大幅下降——这是"位置偏差"问题，不是"信息量"问题。关键教训：上下文窗口变大不等于模型用得好，评测必须变化信息位置。对 TRI 的启示：即使 Context Generator 把关键信息都放了进去，消费方（LLM）可能因为位置问题而忽略它。
```

Week 2: Context Selection / RAG

```text
哪些信息应该被检索进上下文？RAG 的答案是：用 retriever（DPR）从外部知识库选出 top-k 文档，再用 generator 基于这些文档生成答案。关键边界：context selection（谁进来）和 context use（进来后怎么用）是两个独立问题。对 TRI 的启示：TRI Context Package 是经过结构化组织的检索结果，比 RAG 的 raw passages 更进一步——不仅"选进来"，还"组织好"。
```

Week 3: Context Compression / LongLLMLingua

```text
选进来的上下文质量如何？太长、太吵、位置太差，需要压缩。LongLLMLingua 用 question-aware coarse-to-fine 策略压缩 prompt：粗筛去掉无关文档，细压保留问题相关 token，重排缓解位置偏差。关键教训：context compression 是 context selection 和 context use 之间的独立环节，有自己的评测维度（压缩比、信息损失、位置保持）。对 TRI 的启示：TRI 未来可能需要评估 context_noise_ratio、key_information_recall、position_of_key_information 等指标。
```

Week 4: Memory and State / MemGPT

```text
哪些信息应该跨调用、跨任务、跨会话被保存，以什么形式保存？MemGPT 的答案是 memory hierarchy：main context 是"工作台"（快但小），external storage 是"档案库"（慢但大），LLM 通过 function call 自己在两者之间搬运数据。关键区分：retrieval context（当前任务材料）、working memory（跨消息的关键事实）、long-term memory（跨会话的持久知识）、structured state（系统维护的机器可读状态）是四个不同的概念，不能混为一谈。对 TRI 的启示：TRI Context Package 应定位为 structured retrieval context，不是 long-term memory。
```

Month-1 summary / 第一个月总结:

```text
Context Engineering 不是把更多信息塞进 prompt 的简单加法，而是一条需要分层管理的流水线。第一层是 context selection（选什么进来），第二层是 context compression（进来后清理噪声、提高密度、调整位置），第三层是 context use（模型最终是否用好了关键信息），第四层是 memory/state（哪些信息应该被持久化并在未来被检索）。这四层之间相互独立又相互制约：好的 selection 减少 compression 的压力，好的 compression 提升 use 的效率，好的 memory 让 selection 有更丰富的素材。

一条关键发现贯穿四周："放进去"不等于"用得上"（Week 1），"选进来"不等于"选对了"（Week 2），"压缩了"不等于"没丢失关键信息"（Week 3），"存了"不等于"该存的形式"（Week 4）。Context Engineering 的核心能力不是掌握某个算法或框架，而是在每个环节问对问题：这一层在做什么决策？这个决策的证据是什么？这个证据的边界在哪里？

对 TRI 来说，当前最需要厘清的是 TRI Context Package 在流水线中的定位——它现在是 structured retrieval context（经过组织的检索结果），不是 long-term memory。如果未来 TRI 需要在多次实验间积累和演进知识，就需要引入 memory management 机制；如果 TRI 需要压缩长上下文，就需要评测压缩是否损失了时间因果链。这些不是当前必须做的，但清楚知道自己"没做什么"和清楚"做了什么"同样重要。
```

---

## Completion Checklist / 完成检查清单

中文：完成 Week 4 时，至少应该产出下面 3 个 artifact。先写在本 TODO 里即可，review 后再拆到正式笔记。

English: By the end of Week 4, produce at least the three artifacts below. Write them inside this TODO first; after review, move stable content into formal notes.

- [x] One MemGPT paper note / 一份 MemGPT paper note
- [x] One memory/state taxonomy / 一份 memory/state taxonomy
- [x] One month-1 review / 一份第一个月复盘

## Mentor Review Request / 交给 mentor review 时问什么

中文：完成后，把这 4 个问题发给 mentor:

English: After completion, send these four questions to the mentor:

```text
1. 我对 retrieval context、memory、structured state 的边界是否清楚?
2. 我有没有把 conversation history 错当成 memory?
3. 我对 MemGPT claim 的表述是否过度泛化?
4. TRI Context Package 应该叫 structured retrieval context、working state，还是别的名字?
```
