---
id: CON-AMDAHL
type: concept
status: learning
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/Computer Architecture|Computer Architecture]]"
areas:
  - concurrency
  - performance
mastery: 1
review_on: 2026-09-23
prerequisites: []
project_relevance: Interpret 1/2/4/8-thread scalability
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Định luật Amdahl
tags: []
---

# Amdahl's Law

> [!abstract]
> Speedup bị giới hạn bởi phần tuần tự và overhead phối hợp; tăng thread không đảm bảo tăng throughput tuyến tính. ^concept-summary

## Model

$$S(N)=\frac{1}{(1-P)+\frac{P}{N}}$$

Trong đó **P** là phần có thể song song hóa và **N** là số processing units.

## Project mapping

- RQ: [[./RQ-03 - Multi-core Scalability|RQ-03]]
- Quan sát thêm: contention, memory bandwidth, cache coherence, partition skew.
- Không dùng Amdahl như lời giải duy nhất; đo CPU utilization và contention evidence.

## Self-test

> [!question]
> Nếu speedup dừng ở 4 threads, làm sao phân biệt serial fraction với memory bandwidth hoặc lock contention?