---
id: CON-SLAB-ALLOCATOR
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/ET4291 - Operating Systems|ET4291 - Operating Systems]]"
areas:
  - memory-management
  - performance
mastery: 1
review_on: 2026-09-23
prerequisites:
  - "[[Virtual Memory]]"
project_relevance: Fixed-size state allocation and predictable hot-path behavior
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Bộ cấp phát slab
tags: []
---

# Slab Allocator

> [!abstract]
> Slab allocator quản lý các pool object cùng kích thước để giảm metadata, fragmentation và chi phí cấp phát lặp lại; đổi lại cần quản lý lifetime và reclamation rất chặt. ^concept-summary

## Guiding question

> [!question]
> Làm thế nào cấp phát/xóa hàng triệu state mà không phụ thuộc allocation/GC trên hot path?

## Mental model

~~~mermaid
flowchart LR
  PAGE[Pages / large regions] --> SLAB[Slabs]
  SLAB --> SLOT1[Fixed slot]
  SLAB --> SLOT2[Fixed slot]
  SLAB --> FREE[Free list / bitmap]
~~~

## Invariants

- Slot size/alignment cố định trong một class.
- Allocate phải lấy slot chưa dùng đúng một lần.
- Free phải trả đúng ownership, tránh double-free/use-after-free.
- Concurrency/reclamation quyết định correctness trước performance.

## Project mapping

- Component: [[./VstState Memory Manager|VstState Memory Manager]]
- Milestone: [[./M02 - Rebuild Vst Core|M02]]
- Experiment: memory/state, allocation rate, fragmentation, latency

## Common traps

> [!warning]
> - Gọi “zero-GC” khi vẫn allocation ở logging/boxing/closure.
> - Chỉ đo throughput, bỏ leak và long-run stability.
> - So sánh không công bằng vì semantics/lifetime khác nhau.