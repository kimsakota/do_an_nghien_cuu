---
id: M04
type: milestone
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
sequence: 4
start: ""
due: ""
owner: Kim Sakota
success_criteria: Correctness ở 1/2/4/8 threads; Linux build/test pass.
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# M04 — Concurrency and Linux

> [!abstract] Gate
> Correctness ở 1/2/4/8 threads; Linux build/test pass. ^milestone-gate

## Objective

Locks/sharding/CAS khi có cơ sở; Linux port và CI.

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
