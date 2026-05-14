# Context Engineering Glossary

This glossary is bilingual. Each entry should explain the term, not only translate it.

| English term | Chinese explanation | Why it matters |
|---|---|---|
| Context Engineering | 上下文工程：选择、组织、压缩、解释和评估上下文，使模型、工具或人类能更可靠地使用信息 | 当前学习主线 |
| Context Package | 上下文包：结构化打包后的事实集合，可包含实体、关系、信号、事件、候选对象、约束和 provenance | TRI 的核心对象 |
| provenance | 来源与生成过程记录，用来说明信息从哪里来、为什么被纳入 | 关系到可解释性和可审计性 |
| context coverage | 上下文覆盖率，衡量相关信息是否被纳入上下文 | TRI EXP-0003 的核心指标之一 |
| context noise | 上下文噪声，指被纳入但不相关或不在 oracle 中的信息 | 用于衡量上下文是否过宽 |
| long context | 长上下文，指模型输入中包含大量 token 或多段信息，现在很多模型达到 1M 上下文窗口 | `Lost in the Middle` 的研究对象 |
| relevant information | 相关信息，完成任务所需的关键证据 | Context Engineering 关心如何保留和暴露它 |
| relevant information position | 有效信息在整个上下文中所处的物理位置，可以简单理解为行或段落的位置 | 本文的核心实验变量，改变位置就能暴露模型的位置偏差 |
| evaluation protocol | 评测协议，定义任务、变量、指标和比较方式 | 决定实验能支持哪些 claim |
| multi-document question answering | 多文档问答，给模型一个问题和多篇文档，只有一篇有答案，专门测试模型能否在长上下文中找到正确答案 | 常见的长上下文使用评测任务 |
| key-value retrieval | 键值检索，通过 key 准确找到 value，要求 value 完全一致不能被模型加工，找不到也不能编造 | 受控诊断任务，可隔离上下文位置影响 |
| primacy bias | 首因偏差，模型对开头的信息记得更牢，类似人类的第一印象 | 解释长上下文模型可能偏向开头证据 |
| recency bias | 近因偏差，模型对结尾的信息记得更牢，结合 primacy bias 类似人类接收持续信息时的状态 | 解释长上下文模型可能偏向结尾证据 |
| U-shaped performance curve | U 型性能曲线，开头和结尾效果最好，中间最差甚至不如不加检索直接查询 | `Lost in the Middle` 的关键观察 |
| distractor | 干扰文档，通过相关性算法检索到的高分段落，但实际不含答案，能有效干扰模型召回 | 用于测试模型是否能区分相关和无关内容 |
| query-aware contextualization | 查询感知上下文化，在 context 末尾重复一遍 query，对 KV 检索效果极好但对多文档问答没用 | 说明模型不是"看不到"中间内容，而是"看不进去" |
| oracle | 标准答案或人工构造的相关集合，用于评估覆盖、召回或正确性 | TRI synthetic / replay-style evaluation 依赖 oracle |

Add new entries weekly.

