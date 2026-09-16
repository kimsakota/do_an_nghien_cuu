---
id: RQ-02-LEGACY
type: research-question
status: merged
project: "[[10-project/Project VstState|Project VstState]]"
merged_into: "[[./RQ-01 - Dynamic State Trade-off|RQ-01]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - merged
---

# RQ-02 — Dynamic Workload Trade-offs

> [!info] Merged
> Nội dung này là sub-analysis **mutation mix** của [[./RQ-01 - Dynamic State Trade-off|RQ-01]]. Không còn là primary RQ độc lập.

## Preserved question

Read/update/insert/delete mix làm thay đổi relative throughput, p99 và memory behavior của VstState so với baseline như thế nào?

## Operationalization

Được trả lời bằng ba workload đã khóa trong [[./EXP-001 - Baseline Throughput and Latency|EXP-001]]: lookup-only, read-heavy và churn.
