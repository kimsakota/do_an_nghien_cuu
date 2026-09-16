---
id: SYS-WORKFLOW
type: guide
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - system
  - workflow
---

# Workflow — Research OS

## End-to-end map

~~~mermaid
flowchart TD
  IN[Inbox / Question] --> TRIAGE{Triage}
  TRIAGE -->|Knowledge| C[Concept]
  TRIAGE -->|Work| D[Deliverable]
  TRIAGE -->|Scientific| RQ[Research Question]
  TRIAGE -->|Design| ADR[ADR]

  C --> H[Hypothesis]
  RQ --> H
  H --> SPEC[Experiment Specification]
  SPEC --> RUN[Experiment Run]
  RUN --> ANA[Analysis]
  ANA --> CLM[Claim]
  CLM --> WRITE[Thesis / Paper]
  ADR --> IMPL[Implementation]
  D --> IMPL
  IMPL --> RUN
~~~

## Capture → Clarify → Connect → Commit

> [!note] Capture
> Ghi nhanh vào **01-inbox** hoặc Daily note. Chưa cần hoàn hảo.

> [!question] Clarify
> Đây là concept, task, source, decision, observation hay claim?

> [!link] Connect
> Thêm project, parent, RQ/hypothesis, source và outgoing links.

> [!success] Commit
> Chuyển vào folder chuẩn, đặt status, next action và review date.

## Scientific state machine

~~~mermaid
stateDiagram-v2
  [*] --> Proposed
  Proposed --> Testing
  Testing --> PartiallySupported
  Testing --> Supported
  Testing --> Refuted
  Testing --> Inconclusive
  PartiallySupported --> Supported
  PartiallySupported --> Refuted
  Supported --> [*]
  Refuted --> [*]
  Inconclusive --> Testing
~~~

## WIP policy

- Tối đa 3 deliverable ở trạng thái **doing**.
- Mỗi experiment chỉ **running** khi spec đã ready.
- Không mở implementation P2/P3 khi P0 còn thiếu.
- Blocker quá 3 ngày phải thành Risk hoặc quyết định rõ.

## Promotion rules

| Từ | Thành | Điều kiện |
|---|---|---|
| Daily observation | Concept | có giá trị tái sử dụng |
| Question | Research Question | rõ scope và cách trả lời |
| Idea | Hypothesis | falsifiable, có metric/baseline |
| Run result | Analysis | có provenance và so sánh |
| Analysis | Claim | evidence đủ và scope/limitation rõ |
| Discussion | ADR | có lựa chọn, trade-off và hậu quả |
| Task | Deliverable | kéo dài nhiều phiên hoặc tạo artifact |

## Definition of clean handoff

- current focus rõ;
- file đang làm có link;
- quyết định mới đã ghi;
- blocker và next action có owner;
- điều không được giả định được nêu;
- không để kết quả chỉ nằm trong chat.