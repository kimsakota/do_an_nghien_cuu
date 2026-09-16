---
id: EXP-001
type: experiment-spec
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
research_question:
  - "[[30-research/research-questions/RQ-01 - Dynamic State Trade-off|RQ-01]]"
hypothesis:
  - "[[30-research/hypotheses/H-01 - Compact Layout Improves Locality|H-01]]"
  - "[[30-research/hypotheses/H-02 - Sorted Layout Pays Mutation Cost|H-02]]"
  - "[[30-research/hypotheses/H-03 - Sharding Improves Scalability|H-03]]"
baselines:
  - Dictionary-single-thread
  - ConcurrentDictionary
  - VstState
metrics:
  - throughput
  - p99
  - memory-per-live-state
owner: Kim Sakota
due: ""
created: 2026-09-16
updated: 2026-09-16
tags:
  - pre-registration
  - needs-advisor-review
---

# EXP-001 — Dynamic State Trade-off

> [!warning] Pre-registered draft
> Thiết kế đã cụ thể nhưng **chưa ready**. Practical thresholds, collector và pilot noise phải được review trước confirmatory run. Không sửa primary outcomes/exclusions sau khi xem confirmatory result; nếu cần thay đổi, tạo protocol amendment có timestamp.

^experiment-contract

## Objective

Characterize same-semantics performance/memory trade-offs across dataset size, mutation mix and worker count. Đây là experiment *what/where*; mechanism claim được kiểm tra riêng ở [[./EXP-003 - Compact Layout Mechanism Ablation|EXP-003]].

## Backend policy

| Backend | 1 worker | 2/4/8 workers | Role |
|---|---:|---:|---|
| Dictionary | ✓ | — | sequential oracle/reference |
| ConcurrentDictionary | ✓ | ✓ | mainstream same-runtime concurrent hash baseline |
| VstState | ✓ | ✓ | treatment |

Mọi adapter tuân [[./ADR-003 - Baseline Semantics and Fairness|ADR-003]] và [[./IStateBackend|IStateBackend]].

## Frozen core matrix

| Dimension | Values |
|---|---|
| Live states | 10,000; 100,000; 1,000,000 |
| Workers | 1; 2; 4; 8, capped by physical/logical host capability |
| Key distribution | uniform over deterministic live-key domain |
| Trace seeds | 20260916; 20260917; 20260918 for pilot; confirmatory seed derived and recorded per repetition |
| Process isolation | fresh process for every cell × repetition |
| Warm-up | 10 s after setup/JIT exercise |
| Measurement | 30 s |
| Confirmatory repetitions | 10 independent process runs per cell |
| Run order | randomized within repetition blocks; realized order preserved |

## Workload contract

| ID | TryGet | TryUpdate | TryAdd | TryRemove | Occupancy |
|---|---:|---:|---:|---:|---|
| W0 — lookup-only | 100% | 0% | 0% | 0% | fixed |
| W1 — read-heavy | 90% | 5% | 3% | 2% | target logged |
| W2 — churn | 50% | 20% | 15% | 15% | paired generator keeps live set within ±2% |

- Operation sequence/generator contract and seed are identical across comparable backends.
- Actual success/failure ratios are output; divergence >0.5 percentage point invalidates cross-backend comparison until explained.
- Setup generates the same logical initial state and checksum.
- Zipf/skew, expiry and larger-than-memory are sensitivity extensions, not core.

## Outcomes and measurement

| Outcome | Operational definition |
|---|---|
| Throughput | acknowledged valid operations / measured second |
| p99 | per-operation latency from deterministic 1-in-256 sampling; one histogram per process run |
| Bytes/live-state | quiescent retained managed heap delta over empty harness after full collection, divided by verified live count |
| Secondary memory | committed managed bytes, private bytes/RSS, reserved capacity |
| Scaling efficiency | throughput(N) / (N × throughput(1)) |
| Runtime | allocations/op, GC counts/pause where collector overhead is validated |

> [!note]
> Run is the statistical unit. Individual operations are not treated as independent replicates.

## Pilot

Three process runs/cell with 5 s warm-up + 10 s measurement on a reduced matrix:

- backends: ConcurrentDictionary, VstState;
- live states: 100K, 1M;
- workloads: W0, W2;
- workers: 1, 8.

Pilot estimates coefficient of variation, collector overhead, thermal drift and whether 30 s reaches steady state. Pilot is never pooled with confirmatory data.

## Statistical plan

- Report every run-level result, median and IQR.
- Compare VstState/baseline using ratio effect sizes.
- Use percentile bootstrap over **run-level values** with 10,000 resamples for 95% confidence intervals.
- Show Pareto front over throughput, p99 and bytes/live-state; no forced single winner.
- Separate each workload/size/thread condition; no averaging away interactions.
- Correctness/validity failures are reported, not silently removed.

## Provisional practical thresholds

These are engineering minimum effects, pending GVHD approval before status becomes ready:

| Outcome | Practically material |
|---|---:|
| Bytes/live-state | ≥15% relative difference |
| Throughput | ≥10% relative difference |
| p99 | ≥10% relative difference |
| Scaling efficiency | ≥10 percentage-point difference |

Threshold crossing is not sufficient alone; confidence interval, consistency and trade-offs must be reported.

## Hypothesis decision rules

- **H-01 performance/memory:** evidence may support compactness benefit when bytes/live-state improves materially without a material p99 regression in a declared region. **Locality wording additionally requires EXP-003 counters.**
- **H-02 mutation cost:** support requires W2 relative p99/throughput degradation versus W0/W1 to be material and repeatable, not just one cell.
- **H-03 scaling:** characterize speedup/efficiency; mechanism attribution requires contention/profiling evidence.
- Refutation/inconclusive outcomes remain publishable and must be retained.

## Pre-registered exclusions

A run may be marked invalid only when:

1. correctness checksum/invariant fails;
2. manifest/raw file is incomplete or corrupted;
3. intended configuration was not applied;
4. external interruption is independently logged;
5. thermal/power policy violation exceeds pilot-defined bound.

A surprising or poor result is never an exclusion reason. Invalid run remains stored with reason; rerun gets a new ID.

## Readiness gate

- [ ] IStateBackend status **frozen**.
- [ ] Sequential + concurrent correctness gate passes.
- [ ] Key/value physical layout documented.
- [ ] Pilot complete and protocol amendment, if any, signed.
- [ ] GVHD approves practical thresholds/statistics.
- [ ] Environment + affinity/power policy captured.
- [ ] Raw schema, checksums and figure scripts ready.
- [ ] Status changed to **ready** before confirmatory execution.

## Outputs

- Run records: [[./README|runs]]
- Analysis: [[./README|analyses]]
- Environment: [[./Benchmark Environment and Provenance|environment]]
- Candidate claim: [[./CLM-001 - Compact Layout Improves Locality|CLM-001]]
