---
id: HUB-LIBRARY
type: dashboard
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Library Hub
tags:
  - dashboard
cssclasses:
  - research-dashboard
---

# 📚 Library Hub

> [!abstract]
> Source note không chỉ lưu link: nó ghi chất lượng nguồn, method, scope, claim và tác động lên project.

## Source library

![[./90-dashboards/Source Library.base#Sources|90-dashboards/Source Library.base > Sources]]

## Priority reading

| Area | Sources |
|---|---|
| OS/Systems | OSTEP · CS:APP · Systems Performance · Linux man/perf |
| Networking | Kurose/Ross · RFCs · Wireshark |
| Measurement | Raj Jain · experimental design/statistics |
| 5G | 3GPP TS 23.501 · TS 29.244 |
| OSS | [[./Open5GS\|Open5GS]] · [[./free5GC\|free5GC]] · [[./OAI CN5G UPF VPP\|OAI]] |
| State engines | [[./FASTER\|FASTER]] · related papers |

## Source processing flow

~~~mermaid
flowchart LR
  I[Inbox source] --> A[Assess quality]
  A --> E[Extract evidence]
  E --> C[Concept/claim link]
  C --> X[Experiment/design impact]
~~~

## Rule

> [!warning]
> Link/bookmark chưa được xử lý không phải evidence. Phải biết nguồn nói gì, dựa trên method nào và áp dụng trong scope nào.