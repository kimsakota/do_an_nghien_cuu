---
id: WRITE-PROPOSAL
type: thesis-section
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - proposal
---

# Proposal Outline

## 30-second pitch

> Stateful network functions repeatedly read and mutate per-flow state. This project builds a semantics-preserving VstState prototype, characterizes its memory/throughput/tail-latency trade-off against a same-runtime concurrent hash baseline, isolates compact-layout effects, and tests whether the difference remains meaningful in a controlled 5G UPF-like pipeline.

## Title

![[./Project VstState#Working title|10-project/Project VstState > Working title]]

## Problem → gap → question

1. **Problem:** dynamic per-flow state is hot, concurrent and memory-sensitive.
2. **Gap:** ![[./Related Work and Research Gap#^gap-statement|30-research/Related Work and Research Gap > ^gap-statement]]
3. **RQ-01:** ![[./RQ-01 - Dynamic State Trade-off#^rq-statement|30-research/research-questions/RQ-01 - Dynamic State Trade-off > ^rq-statement]]
4. **RQ-02:** ![[./RQ-04 - UPF End-to-End Cost#^rq-statement|30-research/research-questions/RQ-04 - UPF End-to-End Cost > ^rq-statement]]

## Contribution package

![[./Project VstState#Defensible contribution package|10-project/Project VstState > Defensible contribution package]]

## Method

- Freeze observable semantics and pass correctness gate.
- Pre-register and pilot the benchmark.
- Run EXP-001 for trade-off, EXP-003 for mechanism.
- Build bounded UPF-like pipeline and run EXP-002.
- Preserve raw data/checksums and use run-level uncertainty.
- Report negative results, limitations and threats.

## Scope

![[./Project VstState#Core scope|10-project/Project VstState > Core scope]]

## Success criterion

> The project succeeds even if VstState is not universally faster, provided it identifies reproducible operating regions, explains at least one mechanism honestly, quantifies end-to-end relevance and delivers a rerunnable artifact.

## Approval items

- [ ] Title + two RQs.
- [ ] Gap wording.
- [ ] Contract/baseline fairness.
- [ ] Practical thresholds/statistics.
- [ ] UPF-like fidelity boundary.
- [ ] [[./Excellence Gate - ET4920|ET4920 compliance]].
