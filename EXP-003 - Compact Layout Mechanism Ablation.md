---
id: EXP-003
type: experiment-spec
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
research_question:
  - "[[30-research/research-questions/RQ-01 - Dynamic State Trade-off|RQ-01]]"
hypothesis:
  - "[[30-research/hypotheses/H-01 - Compact Layout Improves Locality|H-01]]"
metrics:
  - bytes-per-state
  - llc-misses-per-op
  - cycles-per-op
  - throughput
  - p99
owner: Kim Sakota
created: 2026-09-16
updated: 2026-09-16
tags:
  - ablation
  - mechanism
---

# EXP-003 — Compact Layout Mechanism Ablation

> [!abstract]
> EXP-001 cho biết *chênh lệch ở đâu*. EXP-003 kiểm tra một cơ chế hẹp: **record footprint / compactness**, không gom index, sharding và algorithm vào cùng một treatment.

## Treatment

Hai VstState variants dùng cùng:

- algorithm, indexing, synchronization and API semantics;
- code path/build flags;
- logical StateKey/StateValue fields;
- workload and worker scheduling.

Khác biệt duy nhất có chủ đích:

- **Compact:** production record layout.
- **Padded control:** thêm inert padding để tăng physical bytes/record; padding size được freeze sau code audit và ghi trong manifest.

## Core matrix

| Dimension | Values |
|---|---|
| Live states | 100K; 1M |
| Workload | W1 read-heavy |
| Workers | 1; 8 |
| Variants | compact; padded-control |
| Warm-up / measurement | 10 s / 30 s |
| Repetitions | 10 fresh processes/cell |

## Outcomes

**Mechanism primary:** LLC misses/op and cycles/op.  
**Supporting:** bytes/live-state, throughput and p99.  
**Sanity:** instructions/op, branch misses/op, checksum and success ratios.

## Decision rule

H-01 locality mechanism receives support only if:

1. compact variant has smaller measured bytes/live-state;
2. LLC misses/op improves consistently in the intended large-working-set cells;
3. throughput/p99 movement is directionally compatible;
4. differences are repeatable with run-level uncertainty.

Memory reduction alone does not prove locality. Wall-clock improvement alone does not prove cache behavior.

## Collector plan

- Prefer Linux perf or an equivalently validated hardware-counter collector.
- Pin workers and record multiplexing/scaling.
- Run instrumentation overhead check.
- If counters are unavailable/unreliable, mark mechanism result **inconclusive**; do not infer from timing.

## Threats

- Padding may change alignment as well as capacity.
- Hardware prefetching can alter results.
- Counter multiplexing and VM/hypervisor may distort events.
- One CPU microarchitecture limits external validity.

## Readiness

- [ ] Variant diff audited to confirm one intended factor.
- [ ] Physical layouts documented.
- [ ] Counter access/accuracy validated.
- [ ] Correctness checks identical.
- [ ] EXP-001 identifies the relevant working-set region.
