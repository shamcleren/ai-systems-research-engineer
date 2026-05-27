# Paper Note: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

## Metadata

- Title: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks
- Authors: Patrick Lewis, Ethan Perez, Aleksandra Piktus, Fabio Petroni, Vladimir Karpukhin, Naman Goyal, Heinrich Kuttler, Mike Lewis, Wen-tau Yih, Tim Rocktaschel, Sebastian Riedel, Douwe Kiela
- Source: arXiv:2005.11401
- URL: https://arxiv.org/abs/2005.11401
- Paper type: method / system paper
- Topic tags: retrieval-augmented generation, knowledge-intensive tasks, parametric memory, non-parametric memory, dense retrieval

## One-Sentence Thesis

RAG combines a pre-trained seq2seq generator with a dense retrieval index (DPR + FAISS), showing that retrieval augmentation improves knowledge-intensive NLP tasks over both pure parametric models and pure retrieval models.

中文：RAG 把预训练的 seq2seq 生成器和 dense retrieval 索引结合起来，证明在知识密集型任务上，检索增强优于纯参数模型和纯检索模型。

## Evaluation Model

### Workloads（任务）
- **抽取式 QA**：Natural Questions、TriviaQA
- **生成式任务**：Jeopardy 问题生成、MS MARCO 摘要

### Variable（操控变量）
- **Decoder 架构**：RAG-Sequence vs RAG-Token
- **检索文档数量 k 值**（实验范围 1~5）
- **Retrieval 的使用方式**

### Metrics（指标）
- QA 任务：**Exact Match + F1**（自动指标）
- 生成任务：人工评估（真实性、流畅性）

### Proven（已证明）
- RAG 在知识密集型任务上优于纯参数模型（closed-book）和纯检索模型（retrieval-only）
- RAG 可以通过更新检索索引来更新知识，无需重新训练模型
- RAG-Token 在某些任务上优于 RAG-Sequence

### Modeling Caveat（模型理解校正）
- RAG-Token 不是每个 token 都重新检索文档。它是在同一批 top-k retrieved documents 上,对每个 token 做 document-level marginalization / weighting。
- RAG 使用 DPR + FAISS,但这篇论文不能直接证明 dense retrieval 总是优于 BM25、hybrid retrieval 或 reranker pipeline。

### Not Proven（未证明）

论文没有回答的核心问题：**检索文档数量过多时，效率和成本是否会爆炸增长？**

#### 效率层面
- Decoder 生成时，每个 token 都要 attend 到所有 retrieved documents 的 hidden states
- RAG-Sequence 更夸张——要对每个文档单独跑一遍 full generation，再 marginalize
- k=5 时实验已经能跑，但 k=100 呢？latency 会线性甚至超线性增长

#### 成本层面
- 每次推理都要过 retriever + generator 两个模型
- Retriever 的 dense retrieval 本身就有向量检索开销
- 如果文档库很大，index 维护、embedding 更新都是持续成本

#### 论文为什么没讨论
- 2020 年的论文，RAG 还是新范式，重点是证明"能不能用"而不是"用得多划算"
- 实验设计偏向验证正确性，不是工程可行性
- k 值测试范围是 1~5，区间非常小

#### 工程应对思路
- BM25 粗筛 → dense retriever 精排 → reranker → LLM
- 文档 chunk 策略：切小块而非整篇丢入
- 缓存热点 query 的检索结果
- Reranker（cross-encoder）在生成前做二次过滤

### 补充讨论：BM25 vs Grep

用户提问：grep 和 BM25 的区别？加 grep 是不是会更好？

- **BM25**：信息检索算法，基于 TF-IDF 打分，有相关性排序，会做文档长度归一化
- **Grep**：纯字符串模式匹配，找到就返回，没有打分和排序
- **核心区别**：BM25 有"相关性排序"，grep 只有"有没有出现"
- **结论**：可以加 grep 做最前面的粗筛（极快），但不是关键因素。真正拉开差距的是 dense retriever 的质量和 reranker 的选择

### 补充讨论：Reranker

原始 RAG 论文**没有用 reranker**。检索器是 DPR（Dense Passage Retrieval），bi-encoder 架构：

- Document encoder 把所有文档预计算成向量，存入 FAISS index
- Query encoder 把 query 编码成向量
- 检索 = 向量相似度搜索（内积）

Bi-encoder 的问题：query 和 document 独立编码，没有交互，精度有限。

Reranker（cross-encoder）是后来的方案：
- 把 query + document 拼在一起，送进一个模型做联合编码
- 精度高很多，但每个 candidate 都要跑一遍模型，计算量大
- 常见实现：BGE-Reranker、Cohere Rerank、ColBERT、LLM-based reranker

RAG 论文的检索链路比较粗糙：DPR bi-encoder → top-k → generator。没有 reranker，没有 chunk 策略，没有多路召回。

## System Model

- **Inputs**: question/query
- **Retriever**: DPR bi-encoder，从 Wikipedia passages 索引中检索 top-k 文档
- **Generator**: BART-based seq2seq model，基于 question + retrieved passages 生成答案
- **Output**: generated answer
- **LLM role**: generator 是系统的核心生成组件

## TRI Connection

RAG retrieved passages vs TRI Context Package：

- RAG retrieved passages：按 query 从文档库检索出的文本片段，是 raw retrieval output
- TRI Context Package：结构化上下文，包含实体、关系、信号、事件、候选对象、约束、provenance
- 关键区别：raw retrieval output 更像材料，Context Package 更像经过组织和解释的研究对象

## Claim Audit

| # | Claim | Evidence | Does NOT prove | TRI relevance |
|---|---|---|---|---|
| 1 | RAG 优于 closed-book 和 retrieval-only | 在 NQ、TriviaQA 等任务上 EM/F1 更高 | 不保证在所有任务上都更好 | TRI 可以用 retrieval 增强知识 |
| 2 | RAG 可通过更新索引更新知识 | 实验验证了索引更新后答案变化 | 不保证更新过程无副作用 | TRI 知识库可以是可替换的外部索引 |
| 3 | RAG-Token 某些任务优于 RAG-Sequence | Jeopardy 生成任务上表现更好 | 不证明在所有生成任务上更好 | TRI 可以考虑 token 级别的 context 选择 |
| 4 | RAG 采用 dense retrieval 作为 non-parametric memory | RAG 使用 DPR + FAISS 检索 Wikipedia passages,并在整体任务上优于 closed-book / retrieval-only baseline | 不证明 dense retrieval 总是优于 BM25、hybrid retrieval 或 reranker pipeline | TRI 可以把 dense retrieval 作为候选检索层,但要和 BM25 / hybrid / reranker 做实验证据对比 |
| 5 | 检索增强能提升事实性 | 人工评估显示 RAG 真实性更高 | 不证明没有幻觉 | TRI 需要关注 grounding 和 provenance |

## Open Questions

- k 值增大时效率和成本如何控制？
- Reranker 在 RAG pipeline 中的最优位置？
- TRI Context Package 和 RAG retrieved passages 的融合方式？
- 如何评估检索质量对最终生成的影响？
