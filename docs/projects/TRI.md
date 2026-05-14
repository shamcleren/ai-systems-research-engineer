# TRI Project Card

## Project

Name: TRI Research Engineering

Path:

```text
/Users/renjinming/code/github.com/shamcleren/tri-research-engineering
```

## Role in Learning Plan

TRI is the first practice project for training AI systems research ability.

It should be used as a concrete case for Context Engineering, AI Evaluation, research engineering, and technical-report writing. It should not be treated as the entire learning plan.

## Research Topic

Primary topic:

```text
Intent-conditioned temporal context generation over dynamic relation systems
```

Learning-track mapping:

- primary learning track: Context Engineering;
- method track: AI Evaluation;
- delayed secondary track: Agent Runtime or Edge Runtime.

## Current Training Value

TRI already has useful artifacts for research training:

- Context Package boundary;
- Intent Profile;
- ContextConstraintResolver;
- ProblemDrivenContextGenerator;
- CandidateExtractor;
- synthetic / replay-style evaluation;
- context coverage, noise, candidate recall, candidate compactness metrics;
- Paper 3 technical-report material.

## Why TRI Fits the Current Plan

TRI is currently strongest as a context-engineering practice project.

It is not yet the best first vehicle for Agent Runtime or AI Serving training because those parts are less mature than Paper 3's context generation and evaluation artifacts.

## Current Learning Questions

- What makes a Context Package useful?
- How should context quality be evaluated?
- What does synthetic / replay-style evaluation support?
- What claims are blocked by weak baselines or incomplete oracle construction?
- How can Paper 3 become a stronger technical report without overclaiming?

## Next Learning Task

Use TRI Paper 3 as the first technical-report case study:

1. Read one context-engineering or RAG-evaluation paper.
2. Extract the evaluation structure.
3. Compare it with EXP-0003.
4. Write a claim-boundary critique for TRI Paper 3.

