---
id: CRS-ARCH
type: course
status: active
project: "[[./Project VstState|Project VstState]]"
code: ""
areas:
  - computer-architecture
mastery: 0
review_on: 2026-09-23
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# Computer Architecture

> [!abstract] Exit capability
> Giải thích performance qua cache, branch, instruction và memory behavior. ^course-contract

## Module map

| Module | Topic | Status |
|---|---|---|
| M01 | CPU Pipeline | planned |
| M02 | Cache Hierarchy | planned |
| M03 | Cache Line | planned |
| M04 | TLB | planned |
| M05 | Branch Prediction | planned |
| M06 | Memory Ordering | planned |
| M07 | Performance Counters | planned |

> [!tip] Link only when real
> Khi bắt đầu một module, tạo concept note thật bằng template rồi thêm link vào phần Concepts; không tạo ghost link hàng loạt.

## Concepts in this course

~~~base
filters:
  and:
    - 'type == "concept"'
    - 'course == this.file'
properties:
  mastery:
    displayName: Mastery
  review_on:
    displayName: Review
  status:
    displayName: Status
views:
  - type: table
    name: Concepts
    order:
      - file.name
      - mastery
      - review_on
      - status
~~~

## Project bridge

> [!tip]
> Mỗi module phải dẫn tới ít nhất một component, RQ, experiment hoặc design decision của [[./Project VstState|VstState]].

## Exit criteria

- [ ] Giải thích được mental model cốt lõi.
- [ ] Tự làm được lab/bài tập.
- [ ] Chỉ ra failure modes và trade-off.
- [ ] Áp dụng vào project.
- [ ] Có ít nhất một evidence nâng mastery lên 3 hoặc 4.

## Primary sources

- Chưa xử lý; tạo source note khi bắt đầu học.
