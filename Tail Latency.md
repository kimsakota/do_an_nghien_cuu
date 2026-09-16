---
id: CON-TAIL-LATENCY
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/Statistics and Experimental Design|Statistics and Experimental Design]]"
areas:
  - performance
  - statistics
mastery: 1
review_on: 2026-09-23
prerequisites: []
project_relevance: p95/p99/p99.9 behavior under contention, GC and churn
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Độ trễ đuôi
tags: []
---

# Tail Latency

> [!abstract]
> Tail latency mô tả phần chậm của phân phối, thường qua percentile; nó cho thấy jitter, contention, pause và outlier mà average có thể che giấu. ^concept-summary

## Key rules

- p99 nghĩa là 99% observations không vượt giá trị đó trong sample đã đo.
- Percentile cần đủ sample và phương pháp histogram rõ.
- p99.9 không có ý nghĩa nếu sample quá nhỏ.
- Phải phân biệt service time, response time và coordinated omission.

## Project mapping

- RQ: [[./RQ-02 - Dynamic Workload Trade-offs|RQ-02]]
- Protocol: [[./Core Benchmark Protocol|Core Benchmark Protocol]]
- Metrics: p50, p95, p99; p99.9 chỉ khi sample đủ và collector phù hợp.

## Self-test

> [!question]
> Hai backend cùng average nhưng p99 khác 10× nói lên điều gì?