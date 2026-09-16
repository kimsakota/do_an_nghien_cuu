---
id: TEST-STRATEGY
type: test-plan
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
areas:
  - correctness
tags: []
---

# Test Strategy

> [!abstract]
> Correctness gate đứng trước benchmark. Mỗi backend phải thỏa cùng behavioral contract trước khi so hiệu năng. ^test-gate

## Test pyramid

| Layer | Purpose | Examples |
|---|---|---|
| Unit | Local invariant | slot/free list, hash, key equality |
| Property/model | Compare reference model | random operation sequence |
| Concurrency | Race/linearization symptoms | add/update/remove contention |
| Stress/soak | Leak/liveness | hours, high churn |
| Integration | API + persistence/UPF | packet → state → action |
| Reproducibility | Clean machine path | clone/build/test/run |

## Required oracles

- Reference Dictionary model for single-thread semantics.
- Operation trace + seed.
- Invariant counters.
- Leak/resource accounting.
- Deterministic failure reproduction.

## Pre-benchmark checklist

- [ ] Release build.
- [ ] Unit/property tests pass.
- [ ] Concurrency stress pass.
- [ ] Same semantics across baselines.
- [ ] No diagnostic behavior unique to one backend.
- [ ] Dataset integrity checked.