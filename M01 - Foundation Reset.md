---
id: M01
type: milestone
status: active
project: "[[10-project/Project VstState|Project VstState]]"
sequence: 1
start: ""
due: ""
owner: Kim Sakota
success_criteria: Tự implement và giải thích memory + lookup basics; Research OS vận hành được.
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# M01 — Foundation Reset

> [!abstract] Gate
> Tự implement và giải thích memory + lookup basics; Research OS vận hành được. ^milestone-gate

## Objective

Architecture, OS, unsafe C#, algorithms và statistics; build mini allocator/hash/sorted array.

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
