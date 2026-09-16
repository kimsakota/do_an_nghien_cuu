---
id: HUB-RESEARCH
type: dashboard
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Research Hub
tags:
  - dashboard
cssclasses:
  - research-dashboard
---

# 🔬 Research Hub

> [!abstract] Scientific control plane
> Mọi kết luận đi qua chuỗi **RQ → Hypothesis → Specification → Run → Analysis → Claim → Writing**. Kết quả âm hoặc vô định vẫn là kết quả hợp lệ nếu protocol đúng.

## Core argument

| Layer | Core object | Gate |
|---|---|---|
| Gap | [[30-research/Related Work and Research Gap|Related Work and Research Gap]] | nguồn sơ cấp + wording có boundary |
| RQ-01 | [[30-research/research-questions/RQ-01 - Dynamic State Trade-off|Dynamic state trade-off]] | EXP-001 + EXP-003 |
| RQ-02 | [[30-research/research-questions/RQ-04 - UPF End-to-End Cost|UPF-like end-to-end impact]] | EXP-002 |
| Semantics | [[40-engineering/interfaces/IStateBackend|IStateBackend]] | differential/concurrency correctness |
| Protocol | [[50-experiments/protocols/Core Benchmark Protocol|Core Benchmark Protocol]] | pilot + advisor review |
| Graduation | [[10-project/Excellence Gate - ET4920|Excellence Gate ET4920]] | evidence package |

## Research pipeline

![[./90-dashboards/Research Ledger.base#Research Pipeline|90-dashboards/Research Ledger.base > Research Pipeline]]

## Scope status

> [!success] Primary
> RQ-01 và RQ-02 là hai câu hỏi duy nhất được phép chi phối thesis structure.

> [!quote] Supporting analyses
> Dynamic workload, multi-core scaling, memory efficiency và locality là các góc trả lời RQ-01 — không tách thành nhiều contribution rời.

> [!example] Parked
> [[./RQ-05 - Hybrid Architecture|Hybrid architecture]], DPDK, persistence, production Open5GS/free5GC integration.

## Evidence discipline

> [!danger]
> ![[./Evidence Policy#^evidence-rule|30-research/methodology/Evidence Policy > ^evidence-rule]]

## Methodology

- [[./ADR-002 - Focused Research Scope|ADR-002 — Focused scope]]
- [[./ADR-003 - Baseline Semantics and Fairness|ADR-003 — Baseline fairness]]
- [[./EXP-001 - Baseline Throughput and Latency|EXP-001 — Core trade-off]]
- [[./EXP-003 - Compact Layout Mechanism Ablation|EXP-003 — Mechanism]]
- [[./EXP-002 - UPF End-to-End Backend Impact|EXP-002 — UPF-like impact]]

## Claim review checklist

- [ ] Statement có population/scope, baseline và metric.
- [ ] Evidence link tới immutable run + analysis.
- [ ] Có raw path, checksum, commit và environment.
- [ ] Run là đơn vị thống kê; không pseudo-replication từ từng operation.
- [ ] Có uncertainty, effect size và practical relevance.
- [ ] Evidence against/anomaly không bị xóa.
- [ ] Wording không vượt evidence.
- [ ] Mechanism claim có ablation/counter, không chỉ wall-clock.
- [ ] Limitations được đưa vào thesis.
