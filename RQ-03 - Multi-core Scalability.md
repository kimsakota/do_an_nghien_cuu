---
id: RQ-03-LEGACY
type: research-question
status: merged
project: "[[10-project/Project VstState|Project VstState]]"
merged_into: "[[./RQ-01 - Dynamic State Trade-off|RQ-01]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - merged
---

# RQ-03 — Multi-core Scalability

> [!info] Merged
> Nội dung này là sub-analysis **worker scaling** của [[./RQ-01 - Dynamic State Trade-off|RQ-01]]. Không còn là primary RQ độc lập.

## Preserved question

Speedup và scaling efficiency từ 1 → 2 → 4 → 8 workers thay đổi thế nào, và giới hạn đến từ contention, GC hay memory hierarchy?

## Claim rule

Scaling curve mô tả *what*. Muốn nói *why* phải có profiler/counter/ablation phù hợp.
