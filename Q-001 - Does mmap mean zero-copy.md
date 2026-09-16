---
id: Q-001
type: question
status: active
project: "[[10-project/Project VstState|Project VstState]]"
areas:
  - operating-systems
  - persistence
created: 2026-09-16
updated: 2026-09-16
tags:
  - needs-review
---

# Q-001 — Does mmap mean zero-copy?

> [!question]
> Trong VstState persistence path, mmap loại bỏ những copy nào, vẫn còn page fault/cache movement nào, và “zero-copy” nên được operationalize ra sao? ^question

## Current answer

Chưa kết luận. mmap ánh xạ file vào virtual address space; không tự động loại bỏ mọi data movement hoặc mọi allocation.

## How to answer

- [[./LAB-001 - mmap and Page Faults|LAB-001]]
- OS documentation/source.
- Profile page faults, RSS và copy-related behavior.
- Ghi rõ boundary: kernel/user, page cache, device DMA.

## Promotion

Nếu đủ scope và metric, nâng thành hypothesis hoặc ADR; nếu chỉ là kiến thức nền, hợp nhất vào concept note.