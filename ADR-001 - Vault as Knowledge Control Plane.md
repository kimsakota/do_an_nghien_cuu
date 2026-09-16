---
id: ADR-001
type: adr
status: accepted
decision_status: accepted
project: "[[10-project/Project VstState|Project VstState]]"
areas:
  - research
  - knowledge-management
supersedes: ""
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# ADR-001 — Vault as Knowledge Control Plane

> [!abstract] Decision
> Dùng vault ET4920 làm knowledge/control plane; repository, binary và raw benchmark lớn tiếp tục nằm ngoài vault. ^decision

## Context

Workspace Research chứa nhiều repository và Markdown vendor. Mở toàn bộ workspace thành vault sẽ làm nhiễu search, graph, backlinks và AI context.

## Decision drivers

1. AI cần context nhỏ, có chủ đích.
2. Research cần traceability từ RQ tới raw evidence.
3. Repository phải giữ workflow Git/build riêng.
4. Vault phải portable và dễ backup.

## Considered options

| Option | Pros | Cons | Decision |
|---|---|---|---|
| Mở toàn bộ Research làm vault | Không cần registry | Nhiễu lớn, graph/search kém | rejected |
| Copy code/docs vào vault | Dễ search | Trùng lặp, nhanh stale | rejected |
| Vault riêng + Repository Registry | Sạch, portable, traceable | Cần link/commit discipline | accepted |

## Consequences

### Positive

- Search/backlinks có tín hiệu tốt.
- AI đọc đúng control context.
- Raw data và source không làm vault phình to.

### Negative

- Phải ghi repository/path/commit rõ.
- Link ngoài vault không có backlink tự động.

## Validation

- [x] [[./Repository Registry|Repository Registry]] tồn tại.
- [x] Source notes dùng relative paths.
- [ ] Sau 2 tuần, review độ trơn tru của workflow.