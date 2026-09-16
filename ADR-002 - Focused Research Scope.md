---
id: ADR-002
type: adr
status: accepted
project: "[[10-project/Project VstState|Project VstState]]"
date: 2026-09-16
decision_makers:
  - Kim Sakota
created: 2026-09-16
updated: 2026-09-16
tags:
  - scope
  - research-design
---

# ADR-002 — Focused Research Scope

> [!success] Decision
> Thesis có **hai primary RQs**: (1) dynamic state-store trade-off/mechanism; (2) transfer to a controlled UPF-like pipeline. Dynamic workload và multi-core là sub-analysis của RQ-01. Hybrid, persistence, DPDK và full 5G core là extensions.

## Context

Scaffold cũ có năm RQs, nhiều backend, workload và technology track. Với ET4920, breadth này làm tăng nguy cơ prototype rộng nhưng evidence nông, khiến contribution khó bảo vệ.

## Decision drivers

1. Mỗi RQ phải có experiment và claim boundary riêng.
2. Core phải hoàn tất được với repetitions, correctness và reproducibility.
3. Case study phải kiểm tra external relevance nhưng không biến thành full 5G implementation.
4. Negative result phải vẫn tạo contribution khoa học.

## Consequences

**Positive**

- Thesis kể một argument liền mạch.
- EXP-001/003 trả lời *what/why*; EXP-002 trả lời *so what*.
- Giảm baseline không công bằng và scope creep.
- Có thời gian cho correctness, uncertainty và writing.

**Trade-offs**

- Không tuyên bố production-grade UPF.
- Hybrid/FASTER/DPDK có thể chỉ xuất hiện trong related work/future work.
- Một số milestone cũ cần diễn giải lại theo core scope.

## Revisit condition

Chỉ mở extension nếu G3–G8 trong [[./Excellence Gate - ET4920|Excellence Gate]] đều xanh và còn ít nhất 20% quỹ thời gian.
