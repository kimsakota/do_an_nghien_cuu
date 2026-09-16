---
id: RQ-{{date:YYYYMMDD}}-{{time:HHmm}}
type: research-question
status: proposed
project: "[[10-project/Project VstState|Project VstState]]"
priority: high
areas: []
hypotheses: []
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!question] Research question
> Viết một câu hỏi trung lập, không cài sẵn kết luận. ^rq-statement

## Motivation

Vì sao câu hỏi này quan trọng về khoa học và kỹ thuật?

## Scope

**Included:**  
**Excluded:**  
**Unit of analysis:**  
**Population/workload:**  

## Variables

| Role | Variable | Operational definition |
|---|---|---|
| Independent |  |  |
| Dependent |  |  |
| Controlled |  |  |
| Confounder |  |  |

## Answer strategy

~~~mermaid
flowchart LR
  H[Hypotheses] --> S[Specifications]
  S --> R[Runs]
  R --> A[Analysis]
  A --> C[Claims]
~~~

## Acceptance criteria

Cần loại evidence nào và mức nào để coi câu hỏi đã được trả lời?

## Linked hypotheses and evidence

~~~base
filters:
  or:
    - 'research_question == this.file'
    - 'file.hasLink(this.file)'
properties:
  type:
    displayName: Type
  status:
    displayName: Status
  confidence:
    displayName: Confidence
  evidence_level:
    displayName: Evidence
views:
  - type: table
    name: Pipeline
    order:
      - file.name
      - type
      - status
      - confidence
      - evidence_level
~~~

## Current answer

> [!warning] Chỉ điền từ evidence
> **Status:** unanswered  
> **Best current answer:** ...  
> **Uncertainty:** ...

## Limitations

- ...