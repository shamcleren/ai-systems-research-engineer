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

- [x] Done

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
   这篇论文研究长上下文场景下 prompt 太长、噪声太多、关键信息位置不好导致成本升高和模型表现下降的问题。
   ```

2. 为什么这个问题重要:

   ```text
   这个问题重要是因为 RAG、ICL、agent、多文档 QA 都会把 prompt 变长，但更长不等于更有用，可能增加 latency、cost 和干扰信息。
   ```

3. 作者大概怎么做:

   ```text
   作者提出 LongLLMLingua，用 question-aware compression、document reordering、dynamic compression ratio 和 subsequence recovery 来提高关键信息密度，并在若干长上下文 benchmark 上降低成本、减少延迟、改善或保持生成效果。
   ```

---

### Step 2: First Keywords / 第一批关键词

- [x] Done

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
| long context | 指 token 数量很长的输入场景（几千到几万 token），如多文档问答、长文档摘要、代码补全。长上下文不等于高质量上下文，可能引入噪声、冗余和位置偏差。 |
| prompt compression | 在尽量保留任务相关信息的前提下，减少 prompt 中的 token 数量。目标不是简单截断，而是提高关键信息密度。 |
| key information density | prompt 中与问题/任务相关信息的占比。密度越高，模型越容易找到有用信息，生成质量越好。 |
| position bias | LLM 对关键信息在 prompt 中的位置敏感。放在开头或结尾的信息比放在中间的信息更容易被模型利用（Lost in the Middle 效应）。 |
| question-aware compression | 压缩时考虑问题内容，根据问题与文档的相关性决定保留哪些信息。与 question-agnostic 的方法（如 LLMLingua 原版）相对。 |
| coarse-to-fine compression | 先在文档级别粗筛（coarse），再在 token 级别细压（fine）的两阶段压缩策略。 |
| contrastive perplexity | 用 perplexity(xi|x<i) - perplexity(xi|xque, x<i) 来衡量 token 与问题的关联度。等价于条件逐点互信息（PMI），能更好区分问题相关和无关的 token。 |
| document reordering | 根据文档与问题的相关性分数，重新排列压缩后文档的顺序，把最相关的放到开头，缓解 position bias。 |
| dynamic compression ratio | 不同文档使用不同的压缩率：与问题相关度高的文档保留更多 token，相关度低的压缩更狠。通过粗筛阶段的重要性分数指导细压阶段的 budget 分配。 |
| subsequence recovery | 压缩后恢复被截断的实体名称。利用原始 prompt、压缩 prompt 和 LLM 输出之间的子序列关系，把截断的 token 替换回完整原文。 |
| compression ratio | 原始 prompt token 数与压缩后 token 数的比值。如 4x 表示压缩到原来的 1/4。比值越高压缩越狠，但可能损失更多信息。 |
| information loss | 压缩过程中不可避免地会丢失一些信息。关键风险是丢失了对回答问题至关重要的证据链，导致 LLM 无法生成正确答案。 |

---

### Step 3: Problem Definition / 问题定义

- [x] Done

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
| Cost / latency | token 数量越多，API 调用费用越高，推理延迟越大。论文数据显示 LooGLE 原始 prompt 平均 ~30k token，费用 $93.6/千样本。 | 直接影响实际部署的经济可行性和用户体验。长 prompt 的延迟可能比短 prompt 高 2-3 倍。 |
| Noise / redundancy | 更多文档/历史被塞进 prompt，其中大量内容与当前问题无关（噪声）或重复（冗余）。论文 Figure 1a 显示文档数从 1 增加到 20 时，归一化性能从 ~95% 下降到 ~85%。 | 噪声会分散模型注意力，降低生成质量。即使关键信息在 prompt 里，噪声也可能淹没它。 |
| Position bias | 关键信息放在 prompt 开头时模型表现最好，放在中间时显著下降。论文 Figure 1b 显示原始 prompt 中答案在第 1 位时准确率 ~73%，在第 10 位时降到 ~54%。 | 即使关键信息已经被检索进上下文，如果位置不好，模型也可能用不好它。这直接连接 Week 1 的 Lost in the Middle。 |
| Information loss after compression | 压缩可能截断或删除对回答问题至关重要的 token。论文 Figure 4/6 显示高压缩率下实体名被截断（如 Wilhelm Conrad Röntgen 变成 Wilhelmgen）。 | 如果压缩丢掉了关键证据，压缩后的 prompt 比原始 prompt 更差。需要 subsequence recovery 等机制来补救。 |

---

### Step 4: Context Pipeline Boundary / 上下文流水线边界

- [x] Done

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
| Week 1: Context use | 信息已经在长上下文里，模型能不能用好？关键是位置偏差——信息放在中间时模型最容易忽略。 | TRI 的时间线查询结果即使被检索到，如果放在 prompt 中间位置，模型也可能用不好。需要考虑结果排序策略。 |
| Week 2: Context selection | 哪些信息应该被检索进上下文？RAG 的 retriever 决定哪些文档进入 prompt。 | TRI 的 retriever 需要从多个时间源中选出与查询最相关的事件。检索质量直接决定后续压缩的起点。 |
| Week 3: Context compression and noise | 选进来的上下文质量如何？是否太长、太吵、位置太差？压缩后是否丢掉关键信息？ | TRI 的上下文可能包含大量无关时间事件。需要在压缩时保留时间因果链的关键信息，同时减少噪声。压缩后重排序也很重要。 |

---

### Step 5: System Model / 系统模型

- [x] Done

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
| input / 输入 | question（问题）+ long prompt（长上下文，包含 instruction + K 个文档 + question 本身）。论文实验中 prompt 长度从 ~2.4k 到 ~30k token 不等。 |
| compressor 做什么 | 用小模型（LLaMA-2-7B-Chat）做三步压缩：(1) 粗筛：用 question-aware 的 perplexity 计算每个文档与问题的相关性 rk，保留 top-K' 文档并重排序；(2) 细压：用 contrastive perplexity 在 token 级别压缩，不同文档用不同压缩率；(3) 子序列恢复：把压缩后截断的实体名恢复为原文。 |
| compressed context 是什么 | 压缩后的 prompt，token 数大幅减少（2x-10x），但关键信息密度更高。论文示例：~13k token 压缩到 ~2k token。压缩后的文本不一定是完整句子，可能是截断的 token 序列（如 "Wilhelmdrad"）。 |
| target LLM 做什么 | 基于压缩后的 prompt 生成回答。论文用 GPT-3.5-Turbo 和 LongChat-13B-16k 作为目标 LLM。压缩后的 prompt 直接替代原始 prompt 送入。 |
| output / 输出 | LLM 生成的回答。如果用了 subsequence recovery，会把回答中被截断的实体替换回完整原文（如 "Wilhelmdrad" -> "Wilhelm Conrad Röntgen"）。 |
| main risk / 主要风险 | (1) 压缩可能丢失关键信息，特别是多跳推理中需要的中间证据；(2) 压缩后的截断文本可能影响 LLM 理解；(3) question-aware 压缩不能复用——同一 context 不同 question 需要重新压缩，增加计算开销；(4) 小模型（7B）的 perplexity 估计可能不准确，导致误删重要 token。 |

---

### Step 6: Method Components / 方法组件

- [x] Done

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
| Question-aware coarse-to-fine compression | 解决传统压缩方法（如 LLMLingua、Selective Context）不考虑问题内容的缺陷。用 p(xque\|xdoc_k) 衡量文档与问题的相关性做粗筛，用 contrastive perplexity（等价于 PMI）在 token 级别保留问题相关 token。 | (1) 需要为每个问题重新压缩，无法复用 context；(2) 小模型的 perplexity 估计可能不准确，尤其在复杂推理场景；(3) 粗筛的 restrictive statement（"We can get the answer..."）依赖 prompt engineering。 |
| Document reordering | 解决 position bias（Lost in the Middle）。粗筛后按重要性分数 rk 重排文档，把最相关的放到开头，让 LLM 更容易利用。 | (1) 重排序可能破坏文档间的时序或逻辑关系（论文实验显示 timeline 任务不受影响，但更复杂的因果链可能受影响）；(2) 依赖粗筛阶段的重要性分数准确性。 |
| Dynamic compression ratio | 解决不同文档信息密度不同但压缩率一刀切的问题。相关度高的文档保留更多 token，相关度低的压缩更狠。用线性调度器根据粗筛排名分配细压 budget。 | (1) 压缩率分配依赖粗筛阶段的排名准确性；(2) 线性调度器可能不是最优分配策略；(3) 超参数 δτ 需要调优。 |
| Post-compression recovery | 解决压缩截断实体名称导致 LLM 输出不完整的问题。利用原始 prompt、压缩 prompt 和 LLM 输出之间的子序列关系，把截断 token 替换回完整原文。 | (1) 只能恢复原始 prompt 中存在的子序列，不能恢复被完全删除的内容；(2) 依赖 LLM 输出中包含压缩 prompt 中的 token（LLM 可能改写而非复制）；(3) 增加后处理复杂度。 |

---

### Step 7: Evaluation Model / 评测模型

- [x] Done

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
| workloads / 任务 | 5 个 benchmark：NaturalQuestions（多文档 QA，~3k token）、LongBench（6 类长上下文任务，~10k token）、ZeroSCROLLS（摘要+QA+排序，~10k token）、MuSiQue（多跳 QA，~2.5k token）、LooGLE（长依赖 QA，~30k token）。覆盖多文档 QA、摘要、代码补全、few-shot、多跳推理等场景。 |
| baselines / 对比对象 | 两组：(1) 检索方法：BM25、Gzip、SBERT、OpenAI Embedding、LongLLMLingua rk（仅粗筛）；(2) 压缩方法：Selective Context、LLMLingua。另外有 Zero-shot（无 context）和 Original Prompt（完整 context）作为上下界。 |
| variables / 操控变量 | (1) 压缩比：2x、4x、6x、10x；(2) 答案文档位置：1st、5th、10th、15th、20th；(3) 消融实验：逐一移除各组件。 |
| metrics / 指标 | (1) 准确率/F1（生成质量）；(2) token 数/压缩比（成本）；(3) end-to-end latency（延迟，含压缩时间+LLM 推理时间）；(4) inference cost per 1000 samples（经济成本）。 |
| what it proves / 它能证明什么 | (1) 在这些 benchmark 上，question-aware 压缩比 question-agnostic 压缩和纯检索效果更好；(2) 压缩后的 prompt 在多个任务上性能等于或优于原始 prompt；(3) 压缩确实降低了 token 数、延迟和成本；(4) 每个组件（粗筛、细压、重排、动态压缩率、子序列恢复）的消融实验都显示性能下降，证明各组件都有贡献。 |
| what it does not prove / 它不能证明什么 | (1) 不能证明压缩在所有长上下文场景都有效（benchmark 有限，且论文承认复杂关系场景可能失效）；(2) 不能证明压缩一定提升准确率（某些场景如 ZeroSCROLLS 摘要任务效果接近原始 prompt）；(3) 不能证明压缩开销一定值得（压缩本身需要小模型推理，增加计算，论文承认 LongLLMLingua 计算量是 LLMLingua 的 2 倍）；(4) 不能证明在更复杂推理（如多跳、长因果链）上压缩不会丢失关键中间证据。 |

---

### Step 8: TRI Connection / 连接 TRI

- [x] Done

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
| context_noise_ratio | 上下文中与问题/任务无关的 token 占比。可以反映 retriever 的噪声水平，也可以作为压缩前后的对比指标。 | 不能测量噪声的具体影响——即使噪声比例高，如果关键信息在好位置且密度够高，模型仍可能表现好。也不能区分“冗余但无害”和“有害噪声”。 | key_information_recall（确认关键信息还在）+ position_of_key_information（确认位置是否好） |
| key_information_recall | 压缩/筛选后保留了多少对回答问题必需的关键信息。论文用 recall@k 评估粗筛方法，LongLLMLingua rk 的 recall 在各 k 值上都最高。 | 不能测量关键信息的质量（可能是关键但过时的信息）、位置（recall 高但放在中间仍可能被忽略）、或完整性（部分关键信息丢失仍算 recall）。 | position_of_key_information + answer_grounding_rate（确认模型实际用了这些信息） |
| compression_ratio | 原始 prompt 与压缩后 prompt 的 token 数比值。反映成本节省程度。 | 不能测量压缩质量——高压缩比可能意味着丢失了关键信息。也不能等同于性能提升——论文显示 4x 压缩时某些任务性能反而提升，但某些任务（如摘要）效果接近原始。 | key_information_recall + answer_quality（压缩后的实际生成质量） |
| position_of_key_information | 关键信息在 prompt 中的位置。论文通过固定答案文档在不同位置来评估 position bias。重排后所有位置性能一致（76.2%）。 | 不能单独解释性能——位置好但信息不完整、位置好但噪声太多、位置好但模型理解不了，都会导致性能差。也不能反映多条关键信息的相对位置关系。 | key_information_recall + context_noise_ratio |
| answer_grounding_rate | LLM 的回答是否基于 prompt 中的证据生成（vs. 幻觉或基于参数知识）。Subsequence recovery 就是一种 grounding 机制。 | 不能测量答案正确性（grounded 但可能 grounded 到错误信息）。也不能区分“基于 prompt 回答”和“基于参数知识回答”——两者可能给出相同答案。 | answer_correctness + evidence_traceability（答案可追溯到具体哪条证据） |

---

### Step 9: Claim Audit / 主张审计

- [x] Done

#### What to Do / 做什么

中文:写至少 5 行。每行都要有 claim、证据、不证明什么、和 TRI 的关系。

English: Write at least five rows. Each row must include claim, evidence, what it does not prove, and TRI relevance.

#### Chinese Hint / 中文提示

中文:特别注意不要把"在某些 benchmark 上有效"写成"所有长上下文场景都应该压缩"。也不要把"降低 token 数"直接等同于"一定更准确"。

English: Be careful not to turn "works on some benchmarks" into "all long-context scenarios should use compression." Also do not equate "fewer tokens" with "always more accurate."

#### Your Answer / 你的回答

| Claim / 主张 | Evidence / 证据 | What it does not prove / 不证明什么 | TRI relevance / 和 TRI 的关系 |
|---|---|---|---|
| Question-aware 压缩比 question-agnostic 压缩效果好 | NaturalQuestions 上 LongLLMLingua（77.2%）远超 LLMLingua（39.7%）和 Selective Context（45.4%），2x 约束下。消融实验显示去掉 question-awareness 后降到 42.1%。 | 不能证明 question-aware 压缩在所有任务上都优于 question-agnostic。摘要和代码任务中差距较小。也不能证明 question-awareness 是唯一原因——对比 perplexity 计算方式、restrictive statement 等也有影响。 | TRI 如果做上下文压缩，应该考虑查询感知，而不是盲目压缩所有 context。但需要验证在时间推理场景中 question-aware 是否足够。 |
| 压缩后的 prompt 性能可以等于或优于原始 prompt | NaturalQuestions 4x 压缩：LongLLMLingua 75.0% vs 原始 75.7%（接近持平）；LooGLE 上 LongLLMLingua 32.1% vs 原始 22.6%（+9.5%）。LongBench 2k 约束下 48.3% vs 原始 44.0%。 | 不能证明压缩在所有压缩比和所有任务上都保持性能。ZeroSCROLLS 摘要任务上压缩后效果接近原始但未超越。高压缩比（10x+）下未充分测试。也不能证明性能提升来自压缩本身而非位置重排。 | TRI 的压缩策略不能假设“压缩一定更好”，需要在每个子任务上验证。尤其要注意时间线摘要类任务可能对压缩更敏感。 |
| Document reordering 缓解 position bias | 消融实验：NaturalQuestions 上 LongLLMLingua w/ Reorder 所有位置都是 76.2%，而 w/o Reorder 从 77.2%（1st）降到 70.6%（20th）。其他 baseline 加上 reorder 后也有提升。 | 不能证明重排序在所有场景都有效。论文只测试了文档级重排，没有测试段落级或句子级。也不能证明重排序对需要保持时序的任务（如时间线）完全无害——虽然 LooGLE timeline 任务没下降，但样本有限。 | TRI 的时间线查询结果可能需要考虑排序策略。但要小心：如果查询需要时序推理（"A 发生在 B 之前"），重排序可能破坏时序线索。 |
| Dynamic compression ratio 比固定压缩率好 | NaturalQuestions 2x 约束消融：去掉 dynamic ratio 后从 77.2% 降到 44.4%（平均 68.8%）。LongBench 2k 约束下从 48.3% 降到 45.7%。 | 不能证明线性调度器是最优的 budget 分配策略。也不能证明在所有任务上动态压缩率都优于固定压缩率——论文只测试了线性调度。 | TRI 如果做压缩，应该对不同类型的时间事件（高频事件 vs 低频事件）分配不同压缩率。但需要实验验证最优分配策略。 |
| Subsequence recovery 提升实体完整性 | 论文 Figure 4/6 展示了恢复效果："Wilhelmdrad" -> "Wilhelm Conrad Röntgen"。NaturalQuestions 消融：去掉 recovery 从 77.2% 降到 76.7%（影响不大）。但对 LLMLingua 从 39.7% 提升到 43.8%。 | 不能证明 subsequence recovery 在所有场景都有显著提升。在 NaturalQuestions 上提升仅 0.5%。也不能证明它能恢复所有被压缩掉的信息——只能恢复原始 prompt 中存在但被截断的子序列，完全被删除的信息无法恢复。 | TRI 的压缩后处理可以考虑实体恢复机制，尤其在需要精确名称的时间查询中。但不能依赖它作为主要的信息保全手段。 |

---

### Step 10: Completion and Mentor Review / 完成并找 mentor review

- [x] Done

#### Completion Log / 完成记录

| Item | Answer |
|---|---|
| Date / 日期 | 2026-05-28 |
| Time spent / 耗时 | ~2 小时（含读论文） |
| Hardest part / 最难的地方 | 区分 claim 的 evidence 和 does not prove——论文的实验设计很全面，但每个结论都有适用边界，需要仔细想清楚边界在哪里。 |
| One question / 一个问题 | LongLLMLingua 的 contrastive perplexity 等价于 PMI，但 PMI 在稀疏数据上可能不稳定。论文没有讨论这个问题——在实际部署中，如果小模型对某些领域的 token 概率估计很差，contrastive perplexity 的区分度会不会大幅下降？ |

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

- [x] 中文:Step 1-10 都已经填写或勾选。
      English: Steps 1-10 are filled or checked.
- [x] 中文:所有答案都先写在本 TODO 文件里。
      English: All answers are written in this TODO file first.
- [x] 中文:至少写出 12 个术语解释。
      English: At least 12 term explanations are written.
- [x] 中文:claim audit 至少有 5 行,并且每行都写了 evidence 和 does not prove。
      English: The claim audit has at least five rows, and each row includes evidence and does not prove.
- [x] 中文:TRI metric critique 至少覆盖 context_noise_ratio、key_information_recall、compression_ratio、position_of_key_information、answer_grounding_rate。
      English: The TRI metric critique covers at least context_noise_ratio, key_information_recall, compression_ratio, position_of_key_information, and answer_grounding_rate.
- [ ] 中文:你已经把 Review Prompt 发给 mentor,等待 mentor review 后再进入 Week 4。
      English: You have sent the Review Prompt to the mentor and will wait for mentor review before moving to Week 4.
