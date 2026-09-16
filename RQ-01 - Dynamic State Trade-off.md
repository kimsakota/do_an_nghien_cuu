---
id: RQ-01
type: research-question
status: active
project: "[[10-project/Project VstState|Project VstState]]"
priority: high
areas:
  - performance
  - state-management
hypotheses:
  - "[[30-research/hypotheses/H-01 - Compact Layout Improves Locality|H-01]]"
  - "[[30-research/hypotheses/H-02 - Sorted Layout Pays Mutation Cost|H-02]]"
  - "[[30-research/hypotheses/H-03 - Sharding Improves Scalability|H-03]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - RQ-01 Compact Layout
tags:
  - primary-rq
---

# RQ-01 — Dynamic State Trade-off and Mechanism

> [!question] Primary research question
> Dưới cùng state semantics, VstState tạo trade-off nào về **bytes/live-state, throughput và p99 operation latency** so với concurrent hash baseline khi dataset size, mutation mix và worker count thay đổi; và layout/concurrency mechanism nào giải thích phần chênh lệch quan sát được?

^rq-statement

## Why this is one RQ

Dynamic workload và thread scaling là các biến độc lập của cùng một systems trade-off. Tách chúng thành nhiều RQ dễ tạo nhiều biểu đồ nhưng không tạo nhiều contribution độc lập.

## Core population and boundary

- Managed .NET runtime, in-process, exact-key per-flow state.
- Dataset: 10K, 100K, 1M live keys.
- Workloads: lookup-only, read-heavy, churn.
- Concurrent backends: ConcurrentDictionary và VstState.
- Dictionary: single-thread correctness/performance reference only.
- Uniform key selection là core; Zipf là sensitivity extension.
- Không suy rộng sang persistence, distributed store, SmartNIC hay production traffic.

## Outcomes

| Role | Measure |
|---|---|
| Co-primary | throughput, p99 operation latency, bytes/live-state |
| Secondary | p50/p95, allocations/op, GC pause/count, scaling efficiency |
| Mechanism | cycles/op, instructions/op, cache misses/op, contention |
| Validity | success ratios, checksum, occupancy, runtime/environment |

## Answer strategy

1. [[./EXP-001 - Baseline Throughput and Latency|EXP-001]] characterizes the trade-off.
2. [[./EXP-003 - Compact Layout Mechanism Ablation|EXP-003]] isolates compact layout.
3. Run-level effect sizes + bootstrap confidence intervals.
4. Result is reported as a Pareto frontier and boundary, not a single winner.

## Claim boundary

> [!warning]
> EXP-001 có thể hỗ trợ claim hiệu năng/bộ nhớ. Chỉ EXP-003 cùng counters phù hợp mới hỗ trợ claim về **locality mechanism**.

## Current answer

> [!warning] Unanswered
> Protocol đã cụ thể hóa nhưng chưa có confirmatory raw data. Mọi con số legacy vẫn là unverified.

## Acceptance criteria

- [ ] Same-semantics correctness gate pass.
- [ ] Pilot noise study and exclusions frozen.
- [ ] Confirmatory matrix executed with 10 independent runs/cell.
- [ ] All co-primary metrics reported, including regressions.
- [ ] Mechanism claim has ablation/counters or is marked inconclusive.
- [ ] Limitations and non-dominant regions are explicit.
