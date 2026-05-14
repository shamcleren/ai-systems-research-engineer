# Context Engineering Glossary

This glossary is bilingual. Each entry should explain the term, not only translate it.

| English term | Chinese explanation | Why it matters |
|---|---|---|
| Context Engineering | 上下文工程：选择、组织、压缩、解释和评估上下文，使模型、工具或人类能更可靠地使用信息 | 当前学习主线 |
| Context Package | 上下文包：结构化打包后的事实集合，可包含实体、关系、信号、事件、候选对象、约束和 provenance | TRI 的核心对象 |
| provenance | 来源与生成过程记录，用来说明信息从哪里来、为什么被纳入 | 关系到可解释性和可审计性 |
| context coverage | 上下文覆盖率，衡量相关信息是否被纳入上下文 | TRI EXP-0003 的核心指标之一 |
| context noise | 上下文噪声，指被纳入但不相关或不在 oracle 中的信息 | 用于衡量上下文是否过宽 |
| long context | 长上下文，指模型输入中包含大量 token 或多段信息 | `Lost in the Middle` 的研究对象 |
| relevant information | 相关信息，完成任务所需的关键证据 | Context Engineering 关心如何保留和暴露它 |
| evaluation protocol | 评测协议，定义任务、变量、指标和比较方式 | 决定实验能支持哪些 claim |
| multi-document question answering | 多文档问答，需要从多个文档中定位证据并回答问题 | 常见的长上下文使用评测任务 |
| key-value retrieval | 键值检索，根据 key 从上下文中找出对应 value | 受控诊断任务，可隔离上下文位置影响 |
| primacy bias | 首因偏置，对开头信息更敏感或使用更好 | 解释长上下文模型可能偏向开头证据 |
| recency bias | 近因偏置，对结尾信息更敏感或使用更好 | 解释长上下文模型可能偏向结尾证据 |
| U-shaped performance | U 形表现，开头和结尾表现较好，中间较差 | `Lost in the Middle` 的关键观察 |
| distractor | 干扰项，出现在上下文中但不支持正确答案的信息 | 用于测试模型是否能区分相关和无关内容 |
| oracle | 标准答案或人工构造的相关集合，用于评估覆盖、召回或正确性 | TRI synthetic / replay-style evaluation 依赖 oracle |

Add new entries weekly.

