# 12-Week Context Engineering Research Growth Plan

## Goal

Build the foundation needed to produce paper-style technical reports in AI systems, starting from Context Engineering and AI Evaluation, with TRI as the first practice project.

## Baseline

- Paper-reading habit: not yet established.
- English paper reading: needs Chinese translation and keyword support.
- AI systems concepts: familiar but not systematic.
- Engineering background: strong systems and infrastructure base.
- Weekly time budget: more than 12 hours.

## Target After 12 Weeks

By the end of 12 weeks, the researcher should be able to:

- read an AI systems paper with a structured method;
- produce bilingual paper notes;
- explain context-engineering concepts clearly;
- critique evaluation metrics, baselines, and claim boundaries;
- connect paper ideas to TRI;
- write a technical-report section with conservative claims and limitations.

## Weekly Structure

Every week follows:

```text
Read -> Translate terms -> Extract system model -> Critique evaluation -> Connect to TRI -> Write
```

## Phase 1: Reading Foundation and Vocabulary

### Week 1: Paper Anatomy

Focus:

- learn the structure of AI systems papers;
- practice reading abstract, introduction, method, and evaluation separately.

Outputs:

- one structured paper note;
- first bilingual glossary with at least 30 terms;
- one note explaining the difference between problem, method, experiment, and claim.

TRI connection:

- map TRI Paper 3 into the same paper structure.

### Week 2: RAG and Context Selection Basics

Focus:

- understand retrieval, context selection, grounding, and provenance.

Outputs:

- one paper note;
- one context-selection concept map;
- one TRI note: how Context Package differs from raw retrieval output.

TRI connection:

- review whether TRI's Context Package has clear input, output, and provenance boundaries.

### Week 3: Context Compression and Noise

Focus:

- understand why context can be too large, noisy, stale, or irrelevant.

Outputs:

- one paper note;
- one bilingual glossary update;
- one short note on context noise, compression, and information loss.

TRI connection:

- critique EXP-0003 `context_noise_ratio`: what it measures and what it does not measure.

### Week 4: Memory and State

Focus:

- distinguish retrieval context, working memory, long-term memory, and structured state.

Outputs:

- one paper note;
- one memory/state taxonomy;
- month-1 review.

TRI connection:

- explain whether TRI Context Package should be considered memory, retrieved context, or structured state.

## Phase 2: Evaluation and Claim Discipline

### Week 5: Evaluation Metrics

Focus:

- learn coverage, precision, recall, noise, compactness, and relevance metrics.

Outputs:

- one paper note;
- one metric table;
- one critique of TRI EXP-0003 metrics.

TRI connection:

- rewrite EXP-0003 metric explanations in stricter research language.

### Week 6: Baselines and Ablations

Focus:

- learn how baselines and ablations support or weaken claims.

Outputs:

- one paper note;
- one baseline critique;
- one ablation design note.

TRI connection:

- critique B0-B6 in EXP-0003 and identify the weakest baseline.

### Week 7: Oracle Construction and Validity Threats

Focus:

- understand synthetic oracle, replay-style cases, ground truth, and validity threats.

Outputs:

- one paper note;
- one threats-to-validity section draft;
- one oracle-risk checklist.

TRI connection:

- write a focused critique of TRI's synthetic / replay-style oracle.

### Week 8: Technical Report Structure

Focus:

- learn how to structure a technical report without overclaiming.

Outputs:

- one paper or technical-report note;
- month-2 review;
- draft one improved section for a TRI-related technical report.

TRI connection:

- select one Paper 3 section and rewrite it with clearer claim boundaries.

## Phase 3: Research Artifact Production

### Week 9: Problem Definition

Focus:

- write precise problem definitions.

Outputs:

- one paper note;
- one problem-definition rewrite;
- one list of non-goals.

TRI connection:

- rewrite the Context Generation research question in one strong and one conservative version.

### Week 10: Method and System Diagram

Focus:

- describe systems clearly enough that readers can reproduce the method.

Outputs:

- one paper note;
- one text or Mermaid system diagram;
- one method-section draft.

TRI connection:

- redraw TRI Paper 3 method flow and explain each boundary.

### Week 11: Results and Limitations

Focus:

- write results without overstating evidence.

Outputs:

- one paper note;
- one results paragraph;
- one limitations paragraph;
- one claim audit table.

TRI connection:

- turn EXP-0003 observations into evidence-bound report prose.

### Week 12: Consolidated Technical Report Draft

Focus:

- consolidate reading, evaluation, and writing into one coherent artifact.

Outputs:

- month-3 review;
- one complete mini technical report or extended research note;
- next 12-week plan proposal.

TRI connection:

- produce a TRI Paper 3 evaluation critique or Paper 4 transition note.

## Completion Criteria

The 12-week plan is complete only if it produces:

- at least 8 structured paper notes;
- at least 8 bilingual glossary updates;
- at least 4 TRI evaluation or claim-boundary critiques;
- at least 3 technical-report section drafts;
- one consolidated mini technical report or extended research note.

## Delayed Tracks

Agent Runtime and AI Infra / Serving are intentionally delayed.

They should become secondary tracks only after the researcher has:

- a stable paper-reading routine;
- a working evaluation vocabulary;
- at least one coherent technical-report artifact.

