---
id: CON-VIRTUAL-MEMORY
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/ET4291 - Operating Systems|ET4291 - Operating Systems]]"
areas:
  - operating-systems
  - memory-management
mastery: 1
review_on: 2026-09-23
prerequisites: []
project_relevance: Native memory, mmap, page faults, RSS and persistence
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Bộ nhớ ảo
tags: []
---

# Virtual Memory

> [!abstract]
> Virtual memory tách địa chỉ mà process nhìn thấy khỏi physical memory, thông qua page table, TLB và OS policy; mapping không đồng nghĩa page đã resident. ^concept-summary

## Project mapping

- [[./VstState Memory Manager|VstState Memory Manager]]
- [[./LAB-001 - mmap and Page Faults|LAB-001]]
- Metrics: RSS, page faults, TLB/cache behavior.

## Key distinctions

| Concept | Question |
|---|---|
| Reserved | Address range đã được giữ? |
| Committed/backed | Có backing resource? |
| Resident | Page đang ở RAM? |
| Dirty | Page cần write-back? |
| Mapped | File/anonymous region liên kết thế nào? |