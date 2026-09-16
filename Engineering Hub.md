---
id: HUB-ENGINEERING
type: dashboard
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Engineering Hub
tags:
  - dashboard
cssclasses:
  - research-dashboard
---

# 🧱 Engineering Hub

> [!abstract]
> Engineering notes giải thích **hệ thống đang là gì và vì sao**; code vẫn là source of truth cho implementation.

## Map

| Layer | Note | Question |
|---|---|---|
| Architecture | [[./System Architecture\|System Architecture]] | Boundary và data flow là gì? |
| Interface | [[./IStateBackend\|IStateBackend]] | Backend phải cung cấp semantics nào? |
| Component | [[./VstState Memory Manager\|Memory Manager]] | Ownership/lifetime/allocation hoạt động ra sao? |
| Code map | [[./VstHelper Codebase Map\|VstHelper Codebase Map]] | Symbol nằm ở repository/commit nào? |
| Test | [[./Test Strategy\|Test Strategy]] | Làm sao biết code đúng trước benchmark? |
| Decision | [[./ADR-001 - Vault as Knowledge Control Plane\|ADR-001]] | Trade-off nào đã được chấp nhận? |

## Engineering lifecycle

~~~mermaid
flowchart LR
  R[Requirement] --> ADR[ADR]
  ADR --> API[Interface]
  API --> IMP[Implementation]
  IMP --> T[Test]
  T --> BENCH[Experiment]
  BENCH --> ADR
~~~

## Open engineering tasks

~~~query
task-todo: path:"40-engineering"
~~~

> [!warning]
> Benchmark không thay thế correctness test. “Nhanh” nhưng sai semantics không phải baseline hợp lệ.