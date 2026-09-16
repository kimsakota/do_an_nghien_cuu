---
id: H-05
type: hypothesis
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
research_question: "[[30-research/research-questions/RQ-05 - Hybrid Architecture|RQ-05]]"
confidence: low
areas:
  - performance
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# H-05 — Hybrid Balances Lookup and Memory

> [!example] Falsifiable statement
> Hybrid hash index + compact store sẽ nằm trên Pareto frontier lookup/update/memory/tail latency so với pure designs trong ít nhất một workload mục tiêu. ^hypothesis-statement

## Rationale

Cơ chế dự kiến phải được nối với concept, design và counter quan sát được; không support hypothesis chỉ bằng wall-clock.

## Operationalization

| Element | Definition |
|---|---|
| Treatment | pending specification |
| Baseline | Dictionary / ConcurrentDictionary hoặc baseline phù hợp |
| Workload | được freeze trong experiment spec |
| Primary metric | được freeze trước run |
| Controls | machine, runtime, commit, seed, command |
| Repetition | đủ để ước lượng uncertainty |

## Falsification

> [!danger]
> Nếu hybrid bị một pure design dominate trên tất cả primary metrics hoặc overhead complexity không được biện minh. ^falsification-rule

## Competing explanations

1. JIT/GC/warmup.
2. Cache state, branch behavior hoặc allocator overhead.
3. Baseline semantics/configuration không tương đương.
4. Lock contention hoặc partition skew.

## Evidence

~~~base
filters:
  and:
    - 'hypothesis == this.file'
    - 'file.inFolder("50-experiments")'
properties:
  status:
    displayName: Status
  commit:
    displayName: Commit
  dataset:
    displayName: Dataset
views:
  - type: table
    name: Evidence
    order:
      - file.name
      - status
      - commit
      - dataset
~~~

## Decision

**Current:** proposed  
**Evidence strength:** none  
**Next experiment:** [[|]]
