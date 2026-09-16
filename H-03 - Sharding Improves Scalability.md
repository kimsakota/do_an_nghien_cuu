---
id: H-03
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

# H-03 — Partitioning Changes Scaling Efficiency

> [!example] Falsifiable statement
> VstState partitioning is expected to improve speedup through moderate worker counts, but scaling efficiency will decline when contention, GC or memory hierarchy becomes dominant.

^hypothesis-statement

## Operationalization

EXP-001 reports throughput speedup and efficiency at 1/2/4/8 workers for each size/workload. Profiler evidence is required before attributing a knee to a specific mechanism.

## Falsification

> [!danger]
> Refute/inconclusive if VstState does not improve from 1 worker, loses efficiency earlier than baseline without compensating trade-off, or evidence cannot identify the bottleneck.

^falsification-rule

## Decision

**Current:** proposed  
**Evidence strength:** none  
**Next:** [[./EXP-001 - Baseline Throughput and Latency|EXP-001]].
