---
id: CODEMAP-VSTHELPER
type: code-map
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
repository: VstHelper
relative_path: ../../Research/VstHelper
commit: ""
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags:
  - needs-review
---

# VstHelper Codebase Map

> [!warning] Legacy map
> Đây là navigation scaffold, chưa xác nhận symbol/commit hiện tại. Khi đọc code phải điền commit và verify từng row. ^codemap-warning

## Repository

- Registry: [[./Repository Registry|Repository Registry]]
- Source note: [[./VstHelper|VstHelper]]
- Root: **../../Research/VstHelper**
- Commit: pending

## Component map

| Concern | Path/symbol | Status | Notes |
|---|---|---|---|
| Memory | pending | unverified | [[40-engineering/components/VstState Memory Manager|Memory Manager]] |
| State API | pending | unverified | [[40-engineering/interfaces/IStateBackend|IStateBackend]] |
| Index | pending | unverified | sorted/hash/hybrid |
| Concurrency | pending | unverified | locks/sharding/CAS |
| Tests | pending | unverified | correctness before benchmark |
| Benchmark | pending | unverified | manifest/raw output required |

## Audit tasks

- [ ] Record HEAD commit.
- [ ] Identify solution/projects.
- [ ] Map public API and ownership.
- [ ] Locate tests and benchmark entry points.
- [ ] Mark legacy results as unverified.
- [ ] Create ADRs for retained/rejected design.