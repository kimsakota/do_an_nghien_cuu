---
id: RQ-04
type: research-question
status: active
project: "[[10-project/Project VstState|Project VstState]]"
priority: high
areas:
  - 5g
  - upf
  - performance
hypotheses:
  - "[[30-research/hypotheses/H-04 - State Access Is a Material UPF Cost|H-04]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - RQ-02 UPF Impact
tags:
  - primary-rq
---

# RQ-02 — UPF-like End-to-End Backend Impact

> [!question] Primary research question
> Khi giữ nguyên parser, rule/action logic và traffic replay, thay duy nhất state backend làm thay đổi packet throughput, end-to-end p99 và CPU cost của pipeline UPF-like bao nhiêu; phần chi phí nào thực sự đến từ state access?

^rq-statement

## Pipeline boundary

GTP-U-like packet → TEID extraction → exact state lookup/update → PDR/FAR-like decision → forward/drop/count.

Đây là **controlled UPF-like case study**, không phải 3GPP-conformant production UPF.

## Counterfactuals

- Null/no-state backend: upper-bound pipeline cost without real state access.
- ConcurrentDictionary: mainstream managed concurrent hash baseline.
- VstState: proposed backend.
- Parser/action/traffic/affinity/runtime giữ nguyên.

## Answer strategy

- [[./EXP-002 - UPF End-to-End Backend Impact|EXP-002]]
- Report absolute result and fraction attributable to state path.
- Relate microbenchmark and end-to-end effect through Amdahl-style reasoning.
- If state is not material, report H-04 as refuted/inconclusive; this is still a valid result.

## Current answer

> [!warning] Unanswered
> VstUPF-Lab và controlled replay chưa tạo verified evidence.

## Acceptance criteria

- [ ] Packet/rule semantics validated.
- [ ] Backend is the only intended factor.
- [ ] Replay hash and manifest are identical.
- [ ] Null-backend decomposition included.
- [ ] At least two state sizes and two control-plane regimes.
- [ ] End-to-end p99 collector does not distort the hot path materially.
