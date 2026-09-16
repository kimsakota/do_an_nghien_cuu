---
id: METH-BENCHMARK
type: methodology
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
areas:
  - performance
  - statistics
tags: []
---

# Benchmark Methodology

> [!abstract]
> Benchmark là một phép đo có contract, không phải chạy stopwatch. Contract gồm semantics, workload, environment, collection, analysis và provenance. ^benchmark-contract

## Fairness

- Cùng correctness semantics.
- Cùng key/value representation khi có thể.
- Cùng dataset/seed/operation trace.
- Build mode/runtime settings được ghi.
- Warmup và measurement tách rõ.
- Logging/diagnostics không làm lệch một backend.
- Baseline được tune hợp lý nhưng không cherry-pick.

## Measurement layers

| Layer | Metrics | Purpose |
|---|---|---|
| Correctness | pass/fail, invariant | Không benchmark code sai |
| Application | ops/s, p50/p95/p99 | User-visible behavior |
| Runtime | allocations, GC | Managed-runtime mechanism |
| OS | CPU, faults, RSS | System behavior |
| Hardware | cycles, instructions, cache/branch | Causal explanation |

## Required matrix

- Dataset: 10K, 100K, 1M hoặc rationale khác.
- Workload: read-only, read-heavy, mixed, churn, expiry.
- Threads: 1, 2, 4, 8+ theo machine.
- Backends: Dictionary, ConcurrentDictionary, VstState; Hybrid nếu ready.
- Repetition: freeze trong spec; report uncertainty.

## Analysis guardrails

- Báo distribution/percentile, không chỉ mean.
- Effect size + uncertainty trước p-value.
- Không chọn chỉ subset thuận lợi.
- Phân biệt warmup, steady state, long-run.
- p99.9 chỉ khi sample/collector đủ.
- Tách observation khỏi causal claim.

## Reproducibility bundle

- commit/tag;
- clean/dirty state;
- command;
- config;
- machine/OS/runtime;
- seed/dataset hash;
- raw output/checksum;
- analysis script version;
- generated figure provenance.