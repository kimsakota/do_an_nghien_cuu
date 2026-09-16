---
id: M08
type: milestone
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
sequence: 8
start: ""
due: ""
owner: Kim Sakota
success_criteria: Có causal explanation cho các khác biệt chính.
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# M08 — Profiling and Advanced Baseline

> [!abstract] Gate
> Có causal explanation cho các khác biệt chính. ^milestone-gate

## Objective

perf/cache/branch; optional DPDK/Open5GS extract.

## Exit criteria

- [ ] Objective có artifact/evidence rõ.
- [ ] Correctness/quality gate của milestone pass.
- [ ] Handoff và repository documentation cập nhật.
- [ ] Risk/debt mang sang milestone sau được ghi minh bạch.

## Deliverables

~~~base
filters:
  and:
    - 'type == "deliverable"'
    - 'milestone == this.file'
properties:
  status:
    displayName: Status
  priority:
    displayName: Priority
  due:
    displayName: Due
views:
  - type: table
    name: Deliverables
    order:
      - file.name
      - status
      - priority
      - due
~~~

## Knowledge gate

> [!question] Tôi có thể giải thích, triển khai và đo đạc những gì?
> - ...

## Risks / dependencies

- [[./RISK-001 - Legacy Performance Claims|Legacy performance claims]]
- ...

## Gate review

**Decision:** pending  
**Evidence:**  
**Debt carried forward:**  
