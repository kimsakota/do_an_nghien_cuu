---
id: H-02
type: hypothesis
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
research_question: "[[30-research/research-questions/RQ-01 - Dynamic State Trade-off|RQ-01]]"
confidence: low
areas:
  - performance
created: 2026-09-16
updated: 2026-09-16
tags: []
---

# H-02 — Compact/Sorted Layout Pays Mutation Cost

> [!example] Falsifiable statement
> Relative to lookup-only/read-heavy conditions, churn will degrade VstState throughput or p99 more rapidly than ConcurrentDictionary when layout maintenance/movement becomes material.

^hypothesis-statement

## Operationalization

[[./EXP-001 - Baseline Throughput and Latency|EXP-001]] compares W0/W1/W2 with identical logical traces and reports interaction by workload rather than only aggregate averages.

## Falsification

> [!danger]
> Refute or mark inconclusive if the interaction is absent, inconsistent or explained by unequal success ratios/semantics. One poor cell is insufficient.

^falsification-rule

## Decision

**Current:** proposed  
**Evidence strength:** none  
**Next:** EXP-001.
