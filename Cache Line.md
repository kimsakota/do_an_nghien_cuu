---
id: CON-CACHE-LINE
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/Computer Architecture|Computer Architecture]]"
areas:
  - computer-architecture
  - performance
mastery: 1
review_on: 2026-09-23
prerequisites: []
project_relevance: Compact layout, locality, false sharing and hardware counters
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Dòng cache
tags: []
---

# Cache Line

> [!abstract]
> Cache line là đơn vị dữ liệu CPU cache thường nạp/ghi và duy trì coherence; layout tốt hay xấu phụ thuộc access pattern, không chỉ kích thước object. ^concept-summary

## Guiding question

> [!question]
> Vì sao hai cấu trúc có cùng Big-O nhưng throughput và tail latency khác nhau?

## Mental model

~~~mermaid
flowchart LR
  RAM[Main memory] --> L3[L3]
  L3 --> L2[L2]
  L2 --> L1[L1 cache line]
  L1 --> CPU[Core]
~~~

## Invariants / caveats

- 64 bytes là phổ biến trên x86-64 nhưng phải xác minh trên máy benchmark.
- Spatial locality chỉ có lợi khi bytes lân cận thực sự được dùng.
- Hai thread ghi vào cùng line có thể gây false sharing.
- “32-byte layout” không tự động đồng nghĩa “ít cache miss”.

## Project mapping

- RQ: [[./RQ-01 - Dynamic State Trade-off|RQ-01]]
- Hypothesis: [[./H-01 - Compact Layout Improves Locality|H-01]]
- Lab: [[./LAB-002 - Cache Locality Microbenchmark|LAB-002]]
- Metric: cache-misses, LLC-load-misses, cycles/op, bytes/state

## Self-test

> [!question]- Recall
> Cache line khác cache size như thế nào? False sharing là gì?

> [!question]- Transfer
> Khi nào structure-of-arrays tốt hơn array-of-structures cho VstState?