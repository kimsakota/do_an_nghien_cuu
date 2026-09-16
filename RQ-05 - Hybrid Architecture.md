---
id: RQ-05
type: research-question
status: parked
project: "[[10-project/Project VstState|Project VstState]]"
priority: optional
areas:
  - performance
  - state-management
hypotheses:
  - "[[30-research/hypotheses/H-05 - Hybrid Balances Lookup and Memory|H-05]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - extension
---

# RQ-05 — Hybrid Architecture

> [!example] Parked extension
> Hash index + compact store có thể là future work, nhưng **không nằm trong core ET4920**.

## Unlock condition

Chỉ mở khi correctness, EXP-001, EXP-003, EXP-002 và reproducibility package đã đạt gate; xem [[./ADR-002 - Focused Research Scope|ADR-002]].

## Reason

Thêm một architecture trước khi trả lời hai primary RQs sẽ làm loãng contribution và tăng số cell benchmark vượt quá khả năng kiểm chứng sâu.
