# Paper Review Method

Use this method for every main paper.

## Step 1: Metadata

Record:

- title;
- authors;
- venue or source;
- year;
- paper type: system, benchmark, method, survey, position, or technical report;
- topic tags.

## Step 2: Bilingual Keyword Table

Extract at least 15 terms.

Format:

```text
English term | Chinese explanation | why it matters
```

Do not only translate words. Explain why each term matters in the paper's argument.

## Step 3: One-Sentence Thesis

Write one sentence:

```text
This paper argues that <problem> can be improved by <method> under <setting>, as shown by <evidence>.
```

If this sentence cannot be written, the paper has not been understood yet.

## Step 4: System Model

Answer:

- What are the inputs?
- What are the outputs?
- What are the main components?
- What state is stored?
- What is learned, configured, retrieved, generated, or measured?
- Where does the LLM appear, if it appears at all?

## Step 5: Evaluation Model

Answer:

- What datasets or workloads are used?
- What baselines are compared?
- What metrics are reported?
- What ablations are included?
- What does the evaluation actually prove?
- What does it not prove?

## Step 6: Reusable Idea

Extract one reusable idea for the researcher's own projects.

Examples:

- a metric definition;
- an ablation pattern;
- a system boundary;
- a diagram structure;
- a problem framing;
- a limitation-writing pattern.

## Step 7: TRI Connection

For now, connect every main paper to TRI:

- Does it help define Context Package?
- Does it help evaluate context quality?
- Does it challenge TRI's current metrics?
- Does it suggest a better baseline?
- Does it expose a claim boundary?

If the paper does not connect to TRI, explain why it is still useful for the broader learning plan.

