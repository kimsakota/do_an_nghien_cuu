---
id: M-{{date:YYYYMMDD}}-{{time:HHmm}}
type: milestone
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
sequence: 0
start: ""
due: ""
owner: ""
success_criteria: ""
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!abstract] Gate
> Capability hoặc evidence phải tồn tại khi milestone đóng. ^milestone-gate

## Objective

...

## Exit criteria

- [ ] ...
- [ ] ...
- [ ] ...

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

- Concepts:
- Labs:
- Can explain/implement/measure:

## Risks and dependencies

- [[|]]

## Review

> [!question] Gate decision
> **Pass / conditional / fail:**  
> **Evidence:**  
> **Debt carried forward:**