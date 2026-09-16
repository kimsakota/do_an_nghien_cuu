---
id: CLM-001
type: claim
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
research_question: "[[./RQ-01 - Dynamic State Trade-off|RQ-01]]"
confidence: low
evidence_level: none
evidence: []
areas:
  - performance
tags:
  - needs-review
created: 2026-09-16
updated: 2026-09-16
---

# CLM-001 — Compact Layout Improves Locality

> [!danger] Locked claim
> Chưa được phép viết như kết luận. Current allowed wording: **“Compact-layout locality is a falsifiable hypothesis tested by EXP-001 and EXP-003.”**

^claim-statement

## Promotion ladder

| Level | Allowed wording | Required evidence |
|---|---|---|
| L0 — current | hypothesis only | spec exists |
| L1 — memory | compact uses fewer bytes/live-state in declared conditions | EXP-001/003 memory result |
| L2 — performance | throughput/p99 differs in declared region | EXP-001 repeated runs |
| L3 — mechanism | difference is consistent with improved cache locality | EXP-003 ablation + reliable counters |
| L4 — transfer | state effect matters end-to-end | EXP-002 |

> [!warning]
> Higher-level wording cannot be inferred from a lower level. In particular, memory savings do not prove locality; microbenchmark speed does not prove UPF benefit.

## Evidence for

None yet.

## Evidence against / anomalies

None yet.

## Required path

[[./RQ-01 - Dynamic State Trade-off|RQ-01]] → [[./H-01 - Compact Layout Improves Locality|H-01]] → [[./EXP-001 - Baseline Throughput and Latency|EXP-001]] + [[./EXP-003 - Compact Layout Mechanism Ablation|EXP-003]] → runs → analysis.
