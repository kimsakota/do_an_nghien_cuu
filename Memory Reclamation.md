---
id: CON-MEMORY-RECLAMATION
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/Systems Programming|Systems Programming]]"
areas:
  - concurrency
  - memory-management
mastery: 0
review_on: 2026-09-23
prerequisites:
  - "[[20-learning/concepts/Virtual Memory|Virtual Memory]]"
project_relevance: Safe reuse after concurrent remove
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Thu hồi bộ nhớ
tags: []
---

# Memory Reclamation

> [!abstract]
> Reclamation quyết định khi nào vùng nhớ đã remove được phép tái sử dụng mà không còn reader nào truy cập; đây là correctness problem trước khi là performance optimization. ^concept-summary

## Candidate strategies

| Strategy | Strength | Cost/risk |
|---|---|---|
| Lock + ownership | Dễ reason | Contention |
| Reference counting | Local lifetime | Atomic overhead/cycles |
| Epoch/RCU-like | Read path tốt | Delayed reclaim/complexity |
| Hazard pointer | Precise protection | Per-thread metadata |

## Project mapping

- [[./VstState Memory Manager|Memory Manager]]
- ADR cần có trước khi concurrency implementation chốt.