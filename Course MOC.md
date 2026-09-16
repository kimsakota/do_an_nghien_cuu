---
id: CRS-{{date:YYYYMMDD}}-{{time:HHmm}}
type: course
status: active
project: "[[10-project/Project VstState|Project VstState]]"
code: ""
areas: []
mastery: 0
review_on: ""
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!abstract] Learning contract
> **Why now:** ...  
> **Exit capability:** Sau môn này, tôi có thể giải thích, triển khai và đo đạc ... ^course-contract

## 🧭 Module map

| Module | Core concepts | Practice | Status |
|---|---|---|---|
| M01 | [[|]] | [[|]] | planned |
| M02 | [[|]] | [[|]] | planned |
| M03 | [[|]] | [[|]] | planned |

## 🧠 Concepts

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

## 🧪 Labs and exercises

- [[|]]

## 🎯 Project bridge

> [!tip] Không học tách rời đề tài
> Mỗi module phải link tới ít nhất một component, RQ, experiment hoặc design decision.

## ✅ Exit criteria

- [ ] Giải thích được mental model cốt lõi.
- [ ] Tự làm được bài/lab không nhìn đáp án.
- [ ] Chỉ ra được failure modes.
- [ ] Áp dụng vào VstState/VstUPF-Lab.
- [ ] Đo và phản biện được trade-off.

## 📚 Primary sources

- [[|]]