---
id: HUB-LEARNING
type: dashboard
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Learning Hub
tags:
  - dashboard
cssclasses:
  - research-dashboard
---

# 🧠 Learning Hub

> [!abstract] Học để tạo capability
> Mục tiêu không phải “đọc xong”, mà đi từ nhận diện → giải thích → tự triển khai → đo đạc/phản biện.

## Mastery scale

| Level | Capability | Evidence |
|---:|---|---|
| 0 | Chưa biết | Chưa mô tả được |
| 1 | Nhận diện | Nhận ra thuật ngữ/ví dụ |
| 2 | Giải thích | Dạy lại bằng mental model |
| 3 | Triển khai | Tự code/làm bài/lab |
| 4 | Đo và phản biện | Benchmark, failure mode, trade-off |

## Courses

| Systems foundation | Network/telecom | Research foundation |
|---|---|---|
| [[./ET4291 - Operating Systems\|ET4291 — OS]] | [[./ET4230 - Computer Networks\|ET4230 — Networks]] | [[./Statistics and Experimental Design\|Statistics]] |
| [[./Systems Programming\|Systems Programming]] | [[./ET4070 - Data Communication\|ET4070 — Data Communication]] | [[./Research Methodology\|Research Methodology]] |
| [[./Computer Architecture\|Computer Architecture]] | [[./ET4250 - Telecommunication and 5G\|ET4250 — Telecom & 5G]] |  |
| [[./Algorithms and Data Structures\|Algorithms & DS]] | [[./ET3310 - Cryptography\|ET3310 — Cryptography]] |  |

## Review queue

![[./90-dashboards/Learning Review.base#Review Queue|90-dashboards/Learning Review.base > Review Queue]]

## Project-critical concepts

- [[./Cache Line|Cache Line]]
- [[./Slab Allocator|Slab Allocator]]
- [[./Tail Latency|Tail Latency]]
- [[./Amdahl's Law|Amdahl's Law]]

## Learning loop

~~~mermaid
flowchart LR
  M[Module] --> C[Concept note]
  C --> T[Self-test]
  T --> L[Lab]
  L --> P[Project mapping]
  P --> R[Reflection + review date]
~~~

## Open learning tasks

~~~query
task-todo: path:"20-learning"
~~~

> [!tip] Promotion rule
> Insight có giá trị lâu dài phải được tách khỏi daily note thành concept. Một concept chỉ lên mastery 3–4 khi có evidence từ implementation/lab, không dựa vào cảm giác.