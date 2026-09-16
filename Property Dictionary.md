---
id: SYS-PROPERTY-DICTIONARY
type: schema
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - system
  - schema
---

# Property Dictionary

> [!abstract] Contract dữ liệu
> Properties là API của vault. Giữ tên phẳng, ổn định và đúng kiểu để Bases, Search, AI và người cùng đọc được.

## Common properties

| Property | Kiểu | Bắt buộc | Ý nghĩa |
|---|---|---:|---|
| id | text | ✓ | ID ổn định, không tái sử dụng |
| type | text | ✓ | Loại note theo taxonomy |
| status | text | ✓ | Trạng thái workflow |
| project | link | khi liên quan | Project cha |
| created | date | ✓ | Ngày tạo |
| updated | date | ✓ | Ngày cập nhật nội dung |
| aliases | list |  | Tên thay thế |
| tags | list |  | Tín hiệu ngang hiếm gặp |
| areas | list |  | systems, networking, 5g, research... |
| summary | text |  | Một câu có thể hiển thị trên dashboard |

## Type taxonomy

**System:** dashboard, guide, schema, ai-context, handoff, template  
**Project:** project, milestone, deliverable, risk  
**Learning:** course, concept, lab, exercise, question  
**Research:** research-question, hypothesis, claim, synthesis, methodology  
**Engineering:** architecture, component, code-map, interface, test-plan, adr  
**Experiment:** protocol, experiment-spec, experiment-run, result, analysis  
**Writing:** thesis-section, paper-section, defense, portfolio  
**Log:** daily, weekly, meeting  
**Library:** source, paper, standard, book, web-source, oss-project

## Status vocabularies

| Context | Allowed status |
|---|---|
| Generic | draft, active, review, done, archived |
| Work | backlog, ready, doing, blocked, done, cancelled |
| Research question | proposed, active, answered, parked |
| Hypothesis | proposed, testing, supported, refuted, inconclusive |
| Claim | proposed, partially-supported, supported, refuted, inconclusive |
| Experiment | planned, ready, running, completed, invalid, archived |
| ADR | proposed, accepted, rejected, superseded |
| Learning | planned, learning, reviewing, mastered, parked |

## Type-specific properties

| Type | Properties bổ sung |
|---|---|
| course | code, mastery, review_on |
| concept | course, mastery, review_on, prerequisites, project_relevance |
| source | citekey, authors, year, doi, url, source_quality |
| research-question | priority, hypotheses |
| hypothesis | research_question, falsification, confidence |
| claim | research_question, confidence, evidence_level, evidence |
| milestone | sequence, due, success_criteria |
| deliverable | milestone, priority, due, owner |
| experiment-spec | research_question, hypothesis, baselines, metrics |
| experiment-run | specification, commit, dataset, seed, environment, raw_data, checksum |
| adr | decision_status, supersedes |
| risk | probability, impact, mitigation, owner |

## Evidence levels

1. **legacy-unverified** — text cũ/chưa tái hiện.
2. **anecdotal** — quan sát không có protocol đầy đủ.
3. **single-run** — một run có provenance.
4. **replicated** — nhiều run nhất quán.
5. **triangulated** — nhiều workload/machine/method hỗ trợ.
6. **externally-supported** — phù hợp nguồn chất lượng cao hoặc tái hiện độc lập.

^evidence-levels

## Tag policy

Chỉ dùng tag khi cần tìm xuyên folder:

- needs-review
- blocked
- external-dependency
- legacy-unverified
- ai-generated
- advisor-question

Không dùng tag để thay cho type, status, course hoặc project.