---
id: CON-PAGE-FAULT
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/ET4291 - Operating Systems|ET4291 - Operating Systems]]"
areas:
  - operating-systems
mastery: 1
review_on: 2026-09-23
prerequisites:
  - "[[20-learning/concepts/Virtual Memory|Virtual Memory]]"
project_relevance: mmap warmup, latency outliers and RSS behavior
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Lỗi trang
tags: []
---

# Page Fault

> [!abstract]
> Page fault là trap khi translation/access chưa thỏa; minor và major fault có chi phí rất khác, có thể tạo latency spike nếu benchmark không kiểm soát. ^concept-summary

## Project mapping

- Lab: [[./LAB-001 - mmap and Page Faults|LAB-001]]
- Protocol: warmup/residency phải được nêu.
- Metrics: minor faults, major faults, latency distribution.

## Self-test

> [!question]
> Vì sao mmap thành công nhưng lần đọc đầu vẫn có thể chậm?