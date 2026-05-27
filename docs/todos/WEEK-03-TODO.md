# Week 3 TODO: Context Compression and Noise / 第 3 周 TODO:上下文压缩与噪声

## How to Use This TODO / 如何使用这份 TODO

中文:你只需要在本文件里一步步填写答案。不要来回翻 paper note、glossary 或其他文档。你完成后,把本文件交给 mentor review;mentor 再负责把稳定内容整理到 paper note、glossary 和 TRI note。

English: Fill answers step by step in this file only. Do not jump between the paper note, glossary, or other documents. After you finish, send this TODO to the mentor for review; the mentor will organize stable content into the paper note, glossary, and TRI note.

## Goal / 目标

中文:本周训练的研究能力是理解 context quality:为什么 context 会太长、有噪声、冗余、过期或位置不佳。本周不是为了掌握所有 prompt compression 算法,而是为了产出一份能区分 context selection、context compression、context use 的研究笔记。

English: This week trains context quality reasoning: why context can be too long, noisy, redundant, stale, or poorly positioned. The goal is not to master every prompt-compression algorithm, but to produce a research note that separates context selection, context compression, and context use.

## Source / 阅读材料

中文:只读本地 PDF,不需要自己判断读哪个链接。官方链接只用于来源追溯。

English: Read the local PDF only. You do not need to decide which link to use. The official links are kept only for source traceability.

- Local PDF: `docs/papers/2024.acl-long.91-longllmlingua.pdf`
- Source traceability / 来源追溯: https://aclanthology.org/2024.acl-long.91/
- Official PDF / 官方 PDF: https://aclanthology.org/2024.acl-long.91.pdf
- Paper: `LongLLMLingua: Accelerating and Enhancing LLMs in Long Context Scenarios via Prompt Compression`
- Authors: Huiqiang Jiang, Qianhui Wu, Xufang Luo, Dongsheng Li, Chin-Yew Lin, Yuqing Yang, Lili Qiu
- Venue: ACL 2024
- Optional reference / 可选参考: `docs/notes/papers/2026-05-14-lost-in-the-middle.md` and `docs/todos/WEEK-02-TODO.md`, only when you need to connect Week 1 and Week 2.

## Paper Brief and Current Impact / 论文简介与当前影响

中文:这一节是阅读前导读,帮你先知道这篇论文在讲什么、为什么值得读、现在有哪些技术或能力吸收了它的思路。它不是 claim audit 的直接证据;正式写 claim 时仍要回到论文实验和原文。

English: This section is a pre-reading guide. It explains what the paper is about, why it is worth reading, and which current technologies or capabilities use related ideas. It is not direct evidence for claim audit; formal claims still need to be grounded in the paper's experiments and text.

### 中文简介

中文:LongLLMLingua 研究的是长上下文场景里的 prompt compression。它的出发点很工程化:把更多文档、更多历史、更多工具输出塞进 prompt,并不等于模型一定更好。长上下文会带来更高 cost / latency,也会把噪声、冗余、位置偏差一起带进来。论文希望在保留问题相关关键信息的前提下压缩 prompt,让 LLM 更容易看到真正有用的信息。

中文:这篇论文适合 Week 3,因为它正好连接 Week 1 和 Week 2。Week 1 的 Lost in the Middle 告诉我们:关键信息即使已经在上下文里,模型也可能因为位置问题用不好。Week 2 的 RAG 告诉我们:retriever 决定哪些材料进入上下文。LongLLMLingua 进一步追问:这些材料进来以后,哪些应该保留、哪些应该删掉、是否需要重新排序、压缩后会不会丢掉证据链。

English: LongLLMLingua studies prompt compression for long-context scenarios. It connects Week 1 and Week 2: after context is selected, the system still needs to reduce noise, preserve key information, handle position bias, and avoid information loss.

### 当前影响 / Current Impact

中文:这篇论文的影响不只是"一个压缩算法",而是把 prompt compression 变成 RAG、agent、长上下文应用里的一个系统组件。现在可以从几个方向看到它的影响:

1. 中文:RAG pipeline 里的 context compression。LangChain 已经提供 `LLMLinguaCompressor`,可以和 `ContextualCompressionRetriever` 组合,在 retriever 返回文档后、LLM 生成前压缩上下文。
   English: RAG pipelines can use context compression between retrieval and generation. LangChain provides `LLMLinguaCompressor` with `ContextualCompressionRetriever`.
2. 中文:LlamaIndex 里的 postprocessor。LlamaIndex 提供 `LongLLMLinguaPostprocessor`,用于压缩检索出的 nodes,说明这类方法已经被吸收到 RAG 框架的后处理层。
   English: LlamaIndex provides `LongLLMLinguaPostprocessor`, showing that this idea has become a post-retrieval processing component in RAG frameworks.
3. 中文:LLMLingua 方法家族。Microsoft 的 LLMLingua repo 把 LLMLingua、LongLLMLingua、LLMLingua-2、KV-cache compression、SecurityLingua 放在同一条 prompt-compression / efficient inference 方向上,说明这个方向已经扩展到 task-agnostic compression、推理加速和安全防护。
   English: Microsoft's LLMLingua repo positions LLMLingua, LongLLMLingua, LLMLingua-2, KV-cache compression, and SecurityLingua as a broader prompt-compression / efficient-inference family.
4. 中文:更近的系统评测开始追问"压缩到底什么时候真的省时间"。2026 年的 `Prompt Compression in the Wild` 研究把压缩开销、解码延迟、质量、硬件条件分开评估,说明 prompt compression 已经从算法问题变成系统 trade-off 问题。
   English: Recent systems evaluation asks when compression really saves time. The 2026 `Prompt Compression in the Wild` study evaluates compression overhead, decoding latency, quality, and hardware conditions separately.
5. 中文:对 TRI 的启发是:不要只问 context 是否足够多,还要问 context 是否足够干净、关键信息密度是否够高、位置是否合适、压缩是否损失 provenance。
   English: For TRI, the lesson is not only whether context is sufficient, but whether it is clean, dense in key information, well positioned, and still preserves provenance after compression.

### 当前生态来源 / Current Ecosystem Sources

中文:下面来源用于核对"当前影响",不是论文原始 claim 的直接证据。

English: The sources below verify current impact. They are not direct evidence for the paper's original claims.

- LongLLMLingua ACL paper: https://aclanthology.org/2024.acl-long.91/
- Microsoft LLMLingua repository: https://github.com/microsoft/LLMLingua
- LlamaIndex `LongLLMLinguaPostprocessor`: https://developers.llamaindex.ai/python/framework-api-reference/postprocessor/longllmlingua/
- LangChain `LLMLinguaCompressor`: https://docs.langchain.com/oss/python/integrations/retrievers/llmlingua/
- `Prompt Compression in the Wild` (ECIR 2026 accepted, arXiv): https://arxiv.org/abs/2604.02985

## Step-by-Step Execution / 一步步执行

### Step 1: Title and Abstract / 标题和摘要

- [ ] Done

#### What to Read / 读什么

中文:打开本地 PDF,只看第一页的标题和 Abstract。不要读方法部分。

English: Open the local PDF and read only the title and Abstract on page 1. Do not read the method section yet.

#### Chinese Reading Guide / 中文导读

中文:标题里的 `Long Context Scenarios` 指长上下文场景,例如多文档问答、长文档摘要、代码补全。`Prompt Compression` 不是简单把文本变短,而是在尽量保留任务相关信息的前提下减少 token。Abstract 的核心是:长上下文会带来三个问题:成本更高、性能下降、position bias;作者提出 LongLLMLingua,希望压缩 prompt,提高关键信息密度,同时降低 cost 和 latency。

English: `Long Context Scenarios` means tasks such as multi-document QA, long-document summarization, and code completion. `Prompt Compression` is not just making text shorter; it tries to reduce tokens while preserving task-relevant information. The abstract's core idea is that long context brings three problems: higher cost, lower performance, and position bias. LongLLMLingua tries to compress the prompt, increase key-information density, and reduce cost and latency.

#### What to Write / 写什么

中文:写 3 句话:这篇论文研究什么问题、为什么重要、作者大概怎么做。

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

中文:仍然只看标题、Abstract 和 Introduction 前两页。不要急着读公式。

English: Still read only the title, Abstract, and the first two pages of the Introduction. Do not rush into formulas.

#### Chinese Reading Guide / 中文导读

中文:本周关键词分三类:问题类、方法类、评估类。先写粗糙解释即可,mentor review 后再整理进 glossary。

English: This week's terms fall into three groups: problem terms, method terms, and evaluation terms. Rough explanations are enough for now; the mentor will organize stable terms into the glossary after review.

Candidate terms / 候选术语:

```text
long context
prompt compression
context noise
redundant information
key information
key information density
position bias
lost in the middle
compression ratio
question-aware compression
coarse-to-fine compression
document reordering
dynamic compression ratio
post-compression recovery
latency
cost reduction
information loss
```

#### What to Write / 写什么

中文:至少选 12 个术语,每个写一句中文解释。

English: Pick at least 12 terms and write one Chinese explanation for each.

#### Your Answer / 你的回答

| English term | 中文解释 |
|---|---|
| TODO | TODO |

---

### Step 3: Problem Definition / 问题定义

- [ ] Done

#### What to Read / 读什么

中文:读 Introduction 中关于三个挑战的段落,重点找:cost / latency、noise / redundancy、position bias。

English: Read the Introduction paragraphs about the three challenges. Focus on cost / latency, noise / redundancy, and position bias.

#### Chinese Reading Guide / 中文导读

中文:Week 1 问的是"信息已经在长上下文里,模型能不能用";Week 2 问的是"哪些信息会被检索进上下文";Week 3 问的是"选进来的上下文质量如何,是否太长、太吵、位置太差"。这三个问题不要混在一起。

English: Week 1 asked: once information is already in long context, can the model use it? Week 2 asked: which information is retrieved into context? Week 3 asks: what is the quality of selected context, and is it too long, too noisy, or poorly positioned? Keep these three questions separate.

#### What to Write / 写什么

中文:填写下面 4 行表格。每一行都要写"问题是什么"和"为什么会影响生成结果"。

English: Fill the four-row table below. Each row should explain what the problem is and why it affects generation.

#### Your Answer / 你的回答

| Problem / 问题 | What it means / 含义 | Why it matters / 为什么重要 |
|---|---|---|
| Cost / latency | TODO | TODO |
| Noise / redundancy | TODO | TODO |
| Position bias | TODO | TODO |
| Information loss after compression | TODO | TODO |

---

### Step 4: Context Pipeline Boundary / 上下文流水线边界

- [ ] Done

#### What to Read / 读什么

中文:快速回看 Week 1 和 Week 2 的结论,再读本论文 Introduction 的问题设定。不要读新章节。

English: Briefly revisit the conclusions from Week 1 and Week 2, then read this paper's problem framing in the Introduction. Do not read new sections yet.

#### Chinese Reading Guide / 中文导读

中文:你要建立一个三段式边界:

```text
context selection: 选什么进来
context compression: 进来以后保留什么、删掉什么、如何排序
context use: 模型最终是否真的用了关键信息
```

Week 3 的关键词是中间这段:context compression / context quality。

English: Build a three-part boundary:

```text
context selection: what gets included
context compression: what to keep, remove, and reorder after inclusion
context use: whether the model actually uses the key information
```

Week 3 focuses on the middle part: context compression / context quality.

#### What to Write / 写什么

中文:用 3 行表格说明 Week 1、Week 2、Week 3 分别在问什么问题。

English: Use a three-row table to explain what Week 1, Week 2, and Week 3 each ask.

#### Your Answer / 你的回答

| Week | Main question / 核心问题 | TRI relevance / 和 TRI 的关系 |
|---|---|---|
| Week 1: Context use | TODO | TODO |
| Week 2: Context selection | TODO | TODO |
| Week 3: Context compression and noise | TODO | TODO |

---

### Step 5: System Model / 系统模型

- [ ] Done

#### What to Read / 读什么

中文:看 Figure 1、Figure 2 和方法部分开头。目标是把系统拆成 input、compressor、compressed prompt、target LLM、output。

English: Read Figure 1, Figure 2, and the beginning of the method section. The goal is to break the system into input, compressor, compressed prompt, target LLM, and output.

#### Chinese Reading Guide / 中文导读

中文:LongLLMLingua 可以先看成这个系统:

```text
question + long prompt
  -> question-aware compressor 选择和压缩关键信息
  -> document reordering / recovery 调整压缩后的 prompt
  -> target LLM 基于 compressed prompt 回答
  -> output answer
```

重点不是公式,而是 compression boundary:哪些 token / document 被保留,哪些被删掉,删掉以后是否损失关键信息。

English: You can first view LongLLMLingua as this system:

```text
question + long prompt
  -> question-aware compressor selects and compresses key information
  -> document reordering / recovery adjusts the compressed prompt
  -> target LLM answers from the compressed prompt
  -> output answer
```

The focus is not formulas, but the compression boundary: which tokens/documents are kept, which are removed, and whether key information is lost.

#### What to Write / 写什么

中文:填写下面系统模型表。

English: Fill the system model table below.

#### Your Answer / 你的回答

| Item | 中文回答 |
|---|---|
| input / 输入 | TODO |
| compressor 做什么 | TODO |
| compressed context 是什么 | TODO |
| target LLM 做什么 | TODO |
| output / 输出 | TODO |
| main risk / 主要风险 | TODO |

---

### Step 6: Method Components / 方法组件

- [ ] Done

#### What to Read / 读什么

中文:读 Section 4 的小标题和每个小节开头段落。不要推公式,只抽取方法组件。

English: Read the Section 4 headings and the opening paragraph of each subsection. Do not derive formulas; extract the method components only.

#### Chinese Reading Guide / 中文导读

中文:你要找的是几个工程动作:question-aware coarse-to-fine compression、document reordering、dynamic compression ratio、post-compression recovery。先理解它们分别解决什么问题。

English: Look for the engineering actions: question-aware coarse-to-fine compression, document reordering, dynamic compression ratio, and post-compression recovery. First understand what problem each component tries to solve.

#### What to Write / 写什么

中文:填写 4 行表格。每行写组件、它想解决的问题、可能带来的风险。

English: Fill a four-row table. For each component, write what problem it addresses and what risk it may introduce.

#### Your Answer / 你的回答

| Component / 组件 | Problem addressed / 解决什么问题 | Possible risk / 可能风险 |
|---|---|---|
| Question-aware coarse-to-fine compression | TODO | TODO |
| Document reordering | TODO | TODO |
| Dynamic compression ratio | TODO | TODO |
| Post-compression recovery | TODO | TODO |

---

### Step 7: Evaluation Model / 评测模型

- [ ] Done

#### What to Read / 读什么

中文:读 Experiments / Results 的任务、baseline、metrics 和主要结果。只抽取评测结构,不要追所有数字。

English: Read the tasks, baselines, metrics, and main results in Experiments / Results. Extract the evaluation structure only; do not chase every number.

#### Chinese Reading Guide / 中文导读

中文:Abstract 给了几个结果线索:NaturalQuestions 上在约 4x fewer tokens 的情况下性能提升,在 LooGLE 上显著降低 cost,长 prompt 压缩 2x-6x 时 end-to-end latency 提升。你的任务不是背数字,而是区分它能证明什么、不能证明什么。

English: The Abstract gives several result hints: performance improvement on NaturalQuestions with around 4x fewer tokens, major cost reduction on LooGLE, and end-to-end latency acceleration at 2x-6x compression. Your task is not to memorize numbers, but to separate what these results prove from what they do not prove.

#### What to Write / 写什么

中文:填写评测模型表。

English: Fill the evaluation model table.

#### Your Answer / 你的回答

| Item | 中文回答 |
|---|---|
| workloads / 任务 | TODO |
| baselines / 对比对象 | TODO |
| variables / 操控变量 | TODO |
| metrics / 指标 | TODO |
| what it proves / 它能证明什么 | TODO |
| what it does not prove / 它不能证明什么 | TODO |

---

### Step 8: TRI Connection / 连接 TRI

- [ ] Done

#### What to Do / 做什么

中文:不需要打开 TRI 仓库。只基于本周论文回答:如果 TRI 使用 `context_noise_ratio` 这类指标,它可能能衡量什么,不能衡量什么?

English: You do not need to open the TRI repository. Based only on this week's paper, answer: if TRI uses a metric like `context_noise_ratio`, what might it measure, and what might it miss?

#### Chinese Hint / 中文提示

中文:`context_noise_ratio` 听起来像是在问"上下文里有多少不相关或低价值信息"。但它可能无法单独回答:关键信息是否被保留、位置是否合适、压缩后是否丢失因果链、generator 是否真的使用了证据。

English: `context_noise_ratio` sounds like it asks "how much irrelevant or low-value information is in the context." But by itself it may not answer whether key information is preserved, whether its position is good, whether compression loses causal chains, or whether the generator actually uses the evidence.

#### What to Write / 写什么

中文:写一张 5 行表:metric、可能测量什么、不能测量什么、需要搭配什么指标。

English: Write a five-row table: metric, what it may measure, what it cannot measure, and what companion metric is needed.

#### Your Answer / 你的回答

| Metric / 指标 | May measure / 可能测量 | Cannot measure alone / 单独不能测量 | Companion metric / 搭配指标 |
|---|---|---|---|
| context_noise_ratio | TODO | TODO | TODO |
| key_information_recall | TODO | TODO | TODO |
| compression_ratio | TODO | TODO | TODO |
| position_of_key_information | TODO | TODO | TODO |
| answer_grounding_rate | TODO | TODO | TODO |

---

### Step 9: Claim Audit / 主张审计

- [ ] Done

#### What to Do / 做什么

中文:写至少 5 行。每行都要有 claim、证据、不证明什么、和 TRI 的关系。

English: Write at least five rows. Each row must include claim, evidence, what it does not prove, and TRI relevance.

#### Chinese Hint / 中文提示

中文:特别注意不要把"在某些 benchmark 上有效"写成"所有长上下文场景都应该压缩"。也不要把"降低 token 数"直接等同于"一定更准确"。

English: Be careful not to turn "works on some benchmarks" into "all long-context scenarios should use compression." Also do not equate "fewer tokens" with "always more accurate."

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

中文:完成后,把下面这段发给 mentor。mentor 会先 review 本 TODO,再把稳定内容整理到 paper note、glossary 和 TRI note。

English: After completion, send the prompt below to the mentor. The mentor will review this TODO first, then organize stable content into the paper note, glossary, and TRI note.

```text
请你按研究 mentor 的标准 review 我 Week 3 的 LongLLMLingua TODO 答案,重点看:
1. 我是否区分了 context selection / context compression / context use;
2. 我是否说清楚 long context 的 cost、noise、position bias 三类问题;
3. 关键词解释是否准确;
4. system model 是否抓住 compressor、compressed prompt、target LLM 的边界;
5. evaluation model 是否区分了证明什么和不证明什么;
6. TRI metric critique 有没有过度推断;
7. 请把稳定内容整理到 paper note、glossary 和 TRI note;
8. 下一周我应该补哪块能力。

Please review my Week 3 LongLLMLingua TODO answers as a research mentor. Focus on:
1. whether I separated context selection / context compression / context use;
2. whether I explained the three long-context problems: cost, noise, and position bias;
3. whether the keyword explanations are accurate;
4. whether the system model captures the compressor, compressed prompt, and target LLM boundaries;
5. whether the evaluation model separates what is proven from what is not proven;
6. whether the TRI metric critique over-infers;
7. please organize stable content into the paper note, glossary, and TRI note;
8. what capability I should improve next week.
```

## Done Criteria / 完成标准

- [ ] 中文:Step 1-10 都已经填写或勾选。
      English: Steps 1-10 are filled or checked.
- [ ] 中文:所有答案都先写在本 TODO 文件里。
      English: All answers are written in this TODO file first.
- [ ] 中文:至少写出 12 个术语解释。
      English: At least 12 term explanations are written.
- [ ] 中文:claim audit 至少有 5 行,并且每行都写了 evidence 和 does not prove。
      English: The claim audit has at least five rows, and each row includes evidence and does not prove.
- [ ] 中文:TRI metric critique 至少覆盖 context_noise_ratio、key_information_recall、compression_ratio、position_of_key_information、answer_grounding_rate。
      English: The TRI metric critique covers at least context_noise_ratio, key_information_recall, compression_ratio, position_of_key_information, and answer_grounding_rate.
- [ ] 中文:你已经把 Review Prompt 发给 mentor,等待 mentor review 后再进入 Week 4。
      English: You have sent the Review Prompt to the mentor and will wait for mentor review before moving to Week 4.
