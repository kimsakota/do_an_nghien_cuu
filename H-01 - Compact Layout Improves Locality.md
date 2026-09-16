---
id: H-01
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

# H-01 — Compact Layout Improves Locality

> [!example] Falsifiable statement
> Ở working set lớn dưới read-heavy exact lookup, compact VstState layout sẽ giảm bytes/live-state và LLC misses/op so với padded same-algorithm control; improvement về timing chỉ được gán cho locality khi counter evidence đồng hướng.

^hypothesis-statement

## Why two evidence layers

- EXP-001 compares real systems and identifies performance/memory regions.
- [[./EXP-003 - Compact Layout Mechanism Ablation|EXP-003]] changes one layout factor to test mechanism.
- Hash baseline difference alone cannot isolate locality.

## Falsification

> [!danger]
> H-01 bị refute/inconclusive nếu memory không giảm, LLC misses không cải thiện repeatably, hoặc timing changes contradict the proposed mechanism. A faster wall-clock result alone is insufficient.

^falsification-rule

## Competing explanations

1. Alignment/prefetch/branch behavior.
2. JIT/GC and measurement overhead.
3. Index/concurrency differences rather than record compactness.
4. Counter multiplexing or virtualization noise.

## Decision

**Current:** proposed  
**Evidence strength:** none  
**Next:** EXP-001 → EXP-003.
