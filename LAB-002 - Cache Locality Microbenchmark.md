---
id: LAB-002
type: lab
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/Computer Architecture|Computer Architecture]]"
concepts:
  - "[[20-learning/concepts/Cache Line|Cache Line]]"
created: 2026-09-16
updated: 2026-09-16
tags: []
---

# LAB-002 — Cache Locality Microbenchmark

> [!example] Objective
> So sánh sequential/random access và layout size, đồng thời thu cycles/cache misses để nối wall-clock với cơ chế CPU. ^lab-objective

## Matrix

| Factor | Values |
|---|---|
| Access | sequential, random |
| Element size | 16B, 32B, 64B, 128B |
| Dataset | fits L1, L2, LLC, exceeds LLC |
| Repetition | ≥ 5 |

## Guardrails

- [ ] Correctness checksum giống nhau.
- [ ] Warmup/JIT tách khỏi measurement.
- [ ] CPU affinity/governor ghi rõ.
- [ ] Không kết luận từ một machine như universal fact.

## Output

- Raw data:
- Plot:
- Analysis:
- Concept mastery evidence: