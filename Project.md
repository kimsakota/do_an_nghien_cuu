---
id: PRJ-{{date:YYYYMMDD}}-{{time:HHmm}}
type: project
status: active
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
owner: ""
start: ""
target: ""
areas: []
aliases: []
tags: []
---

# {{title}}

> [!abstract] Project summary
> Problem, target user/system, intended outcome và evidence of success. ^project-summary-template

## Problem statement

...

## Scope / non-scope

| In scope | Out of scope |
|---|---|
|  |  |

## Success criteria

- [ ] ...
- [ ] ...

## Deliverables

~~~base
filters:
  and:
    - 'type == "deliverable"'
    - 'project == this.file'
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

## Milestones

- [[|]]

## Risks

- [[|]]

## Decision log

- [[|]]

## Stakeholders

| Role | Person/team | Need |
|---|---|---|
|  |  |  |

## Current state

**Now:**  
**Next:**  
**Blocked:**  
**Last evidence:**