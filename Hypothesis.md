---
id: H-{{date:YYYYMMDD}}-{{time:HHmm}}
type: hypothesis
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
research_question: ""
confidence: low
areas: []
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!example] Falsifiable statement
> Nếu **intervention/design** dưới **workload/scope**, thì **metric** sẽ thay đổi so với **baseline** theo hướng/mức đã định. ^hypothesis-statement

## Rationale

Cơ chế nào khiến dự đoán này hợp lý? Link concept/source thay vì chỉ kể intuition.

## Operationalization

| Element | Definition |
|---|---|
| Treatment |  |
| Baseline |  |
| Workload |  |
| Primary metric |  |
| Secondary metrics |  |
| Controls |  |
| Sample/repetition |  |

## Falsification

> [!danger] Điều gì sẽ bác bỏ hypothesis?
> Nêu threshold hoặc pattern quan sát đủ để refute/inconclusive. ^falsification-rule

## Competing explanations

1. ...
2. ...

## Experiments

~~~base
filters:
  and:
    - 'hypothesis == this.file'
    - 'file.inFolder("50-experiments")'
properties:
  status:
    displayName: Status
  specification:
    displayName: Specification
  commit:
    displayName: Commit
views:
  - type: table
    name: Evidence
    order:
      - file.name
      - status
      - specification
      - commit
~~~

## Decision log

| Date | Evidence | Decision | Reason |
|---|---|---|---|
|  |  | proposed |  |