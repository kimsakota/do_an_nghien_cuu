---
id: H-04
type: hypothesis
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
research_question: "[[30-research/research-questions/RQ-04 - UPF End-to-End Cost|RQ-02]]"
confidence: low
areas:
  - performance
  - upf
created: 2026-09-16
updated: 2026-09-16
tags: []
---

# H-04 — State Access Is a Material UPF-like Cost

> [!example] Falsifiable statement
> In the declared large-session conditions, replacing only the state backend will create a practically material, repeatable change in packet throughput or end-to-end p99; Null-backend decomposition will show that state access is a non-trivial share of pipeline cost.

^hypothesis-statement

## Test

[[./EXP-002 - UPF End-to-End Backend Impact|EXP-002]] holds parser, actions and replay fixed and compares Null/ConcurrentDictionary/VstState.

## Falsification

> [!danger]
> If backend changes microbenchmark behavior but not end-to-end outcomes beyond the pre-approved threshold, H-04 is refuted/inconclusive. The project must report that boundary rather than inflate the claim.

^falsification-rule

## Decision

**Current:** proposed  
**Evidence strength:** none  
**Next:** build/validate UPF-like fixture, then EXP-002.
