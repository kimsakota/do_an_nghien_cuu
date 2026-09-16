---
id: EXP-002
type: experiment-spec
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
research_question:
  - "[[30-research/research-questions/RQ-04 - UPF End-to-End Cost|RQ-02]]"
hypothesis:
  - "[[30-research/hypotheses/H-04 - State Access Is a Material UPF Cost|H-04]]"
baselines:
  - Null-backend-ablation
  - ConcurrentDictionary
  - VstState
metrics:
  - packet-throughput
  - end-to-end-p99
  - cpu-per-packet
owner: Kim Sakota
created: 2026-09-16
updated: 2026-09-16
tags:
  - upf
  - end-to-end
  - pre-registration
---

# EXP-002 — UPF-like End-to-End Backend Impact

> [!warning] Planned
> Chỉ chạy sau EXP-001 core và UPF-like correctness fixtures. Null backend là cost-decomposition ablation, không phải same-semantics production baseline.

## Objective

Measure whether a backend difference survives in a controlled packet pipeline when parser, rules, traffic, runtime and scheduling remain fixed.

## System under test

```mermaid
flowchart LR
  R[Hashed packet replay] --> P[GTP-U-like parser]
  P --> T[TEID]
  T --> S[State lookup / counter update]
  S --> A[PDR/FAR-like action]
  A --> O[Forward / Drop / Count]
```

No kernel/NIC throughput claim is made: the core experiment uses an in-process deterministic replay so backend is isolatable.

## Factors

| Dimension | Core values |
|---|---|
| Backend | Null cost ablation; ConcurrentDictionary; VstState |
| Live sessions | 100K; 1M |
| Packet payload | 128 B; 1200 B |
| Worker count | 1; 8 |
| Control regime | stable rules; 99 packet operations : 1 rule insert/update/delete |
| Warm-up / measurement | 10 s / 30 s |
| Repetitions | 10 fresh processes/cell |
| Replay | identical packet/rule hash and seed |

Every packet performs TEID extraction, state access, action selection and accounting. Exact counter semantics must be identical for the two real backends.

## Primary outcomes

- packet throughput (packets/s);
- end-to-end p99 processing latency;
- CPU time/cycles per packet where collector support is reliable.

Secondary: drop/forward counts, checksum, allocation/GC, percentage gap from Null ablation.

## Analysis

- Run-level median/IQR + 95% bootstrap CI over 10 runs.
- Backend effect is shown both absolute and relative to the non-state portion estimated by Null ablation.
- Relate EXP-001 state-operation cost to end-to-end change using Amdahl-style decomposition.
- If backend effect is below the pre-approved practical threshold, H-04 is refuted/inconclusive rather than reframed.

## Validity controls

- Same parser/action binary and rule fixture.
- Same replay order/hash.
- Same logical outputs and final checksum.
- Collector overhead measured with instrumentation on/off.
- No claim of 3GPP conformance or line-rate NIC behavior.
- Packet generation is outside timed processing unless the design explicitly times both for every backend.

## Readiness

- [ ] UPF-like functional tests pass.
- [ ] Rule/action semantics documented.
- [ ] Backend adapters pass ADR-003 contract.
- [ ] Replay fixture + expected outputs versioned.
- [ ] Null ablation cannot be confused with correctness baseline.
- [ ] Practical threshold approved before run.
