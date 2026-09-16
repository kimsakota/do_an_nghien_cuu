---
id: CRS-SYSPROG
type: course
status: active
project: "[[./Project VstState|Project VstState]]"
code: ""
areas:
  - systems-programming
mastery: 0
review_on: 2026-09-23
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# Systems Programming

> [!abstract] Exit capability
> Tự triển khai memory structure và quan sát hành vi runtime/OS. ^course-contract

## Module map

| Module | Topic | Status |
|---|---|---|
| M01 | C and C# Memory | planned |
| M02 | Pointers and Unsafe | planned |
| M03 | Syscalls | planned |
| M04 | Files and mmap | planned |
| M05 | Threads and Atomics | planned |
| M06 | Build and Debug | planned |
| M07 | Interop | planned |

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
