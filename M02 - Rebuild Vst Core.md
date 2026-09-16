---
id: M02
type: milestone
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
sequence: 2
start: ""
due: ""
owner: Kim Sakota
success_criteria: Correctness/stress tests pass cho core memory structures.
created: 2026-09-16
updated: 2026-09-16
aliases: []
tags: []
---

# M02 — Rebuild Vst Core

> [!abstract] Gate
> Correctness/stress tests pass cho core memory structures. ^milestone-gate

## Objective

Native memory, slab, raw list, key/hash và correctness tests.

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
