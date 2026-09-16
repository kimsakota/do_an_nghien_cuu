---
id: LAB-001
type: lab
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
course: "[[20-learning/courses/ET4291 - Operating Systems|ET4291 - Operating Systems]]"
concepts:
  - "[[Virtual Memory]]"
  - "[[Page Fault]]"
created: 2026-09-16
updated: 2026-09-16
tags: []
---

# LAB-001 — mmap and Page Faults

> [!example] Objective
> Quan sát lazy mapping, minor/major page faults và RSS; giải thích vì sao mmap không đồng nghĩa zero-copy. ^lab-objective

## Procedure

- [ ] Tạo file dữ liệu kiểm soát kích thước.
- [ ] mmap nhưng chưa chạm page; ghi RSS/faults.
- [ ] Đọc tuần tự từng page; ghi lại.
- [ ] Đọc ngẫu nhiên; so sánh.
- [ ] Unmap và quan sát.

## Evidence

- Command:
- Environment:
- Raw output:
- Interpretation:

## Reflection

- Điều gì được copy?
- Page cache tham gia thế nào?
- Kết quả ảnh hưởng thiết kế persistence ra sao?