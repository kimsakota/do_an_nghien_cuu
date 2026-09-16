---
id: GATE-ET4920
type: quality-gate
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - et4920
  - quality-gate
cssclasses:
  - research-dashboard
---

# 🏆 Excellence Gate — ET4920

> [!abstract]
> ET4920 hiện được HUST công bố là đồ án nghiên cứu cử nhân 8 tín chỉ. Nguồn hướng dẫn HUST nhấn mạnh tổng quan tài liệu, định hướng/mục tiêu, kết quả dự kiến, kế hoạch, cơ sở lý thuyết, mô hình/mô phỏng và nghiên cứu ban đầu làm nền cho bậc cao hơn. **Rubric chấm điểm chính xác của học kỳ/đơn vị vẫn phải được GVHD xác nhận.**

## Official alignment

- [HUST/SEEE — ET1 curriculum, ET4920 8 credits](https://seee.hust.edu.vn/vi/dao-tao/dao-tao-dai-hoc/et1-ky-thuat-dien-tu-vien-thong-287931.html?download=1&id=0)
- [HUST — guidance for bachelor research project](https://ts.hust.edu.vn/tin-tuc/mot-so-luu-y-danh-cho-k62-khi-dang-ky-hoc-phan-do-an-tot-nghiep)

## Red / amber / green scorecard

| Gate | Excellent evidence | Current | Exit criterion |
|---|---|---:|---|
| G1 — Research problem | measurable problem, bounded gap, two answerable RQs | 🟢 | ADR-002 + gap note reviewed |
| G2 — Literature | primary sources + traceable synthesis + search log | 🟠 | snowball/search log complete; GVHD validates gap |
| G3 — Technical product | working VstState, harness, UPF-like demo | 🔴 | build/tests/demo pass on tagged commit |
| G4 — Correctness | differential, concurrency, invariant tests | 🔴 | all backends pass frozen contract |
| G5 — Experimental rigor | pre-registration, pilot, randomization, repetitions, uncertainty | 🟠 | protocol approved; confirmatory runs complete |
| G6 — Mechanism | at least one clean ablation + counters | 🔴 | EXP-003 analyzed or limitation honestly documented |
| G7 — Application relevance | backend-only change in controlled UPF-like pipeline | 🔴 | EXP-002 + null-backend decomposition |
| G8 — Reproducibility | one-command runner, manifest, raw checksums, environment | 🟠 | independent rerun succeeds |
| G9 — Scholarly writing | claim-evidence traceability, negative results, limitations | 🟠 | thesis review checklist 100% |
| G10 — Defense readiness | live/scripted demo, backup video, Q&A evidence index | 🔴 | two mock defenses passed |
| G11 — Engineering context | applicability, operations, cost/energy/security/ethics boundaries | 🟠 | dedicated discussion section |
| G12 — Formal compliance | correct cohort rubric, format, deadlines, advisor approval | 🔴 | official documents attached/linked and signed off |

## What “excellent” means here

> [!success]
> **Excellent ≠ mọi hypothesis đều đúng.** Excellent nghĩa là contribution rõ, system chạy đúng, evaluation công bằng, evidence có uncertainty, mechanism được kiểm tra, giới hạn được nói thật và reviewer có thể tái lập.

## Stop-the-line rules

- Không chạy confirmatory benchmark khi G4 chưa xanh.
- Không gọi “locality improvement” nếu EXP-003/counters chưa hỗ trợ.
- Không gọi “UPF improvement” từ microbenchmark.
- Không đưa số vào abstract nếu chưa link được raw data → analysis → claim.
- Không thêm hybrid/DPDK/Open5GS khi G3–G8 core chưa đạt.

## Advisor validation checklist

- [ ] Xác nhận rubric ET4920 đúng khóa và đơn vị.
- [ ] Xác nhận title và hai primary RQs.
- [ ] Xác nhận baseline/fairness contract.
- [ ] Xác nhận practical thresholds và statistics plan.
- [ ] Xác nhận mức fidelity tối thiểu của UPF-like case.
- [ ] Xác nhận format báo cáo, slide, demo và mốc nghiệm thu.

## Evidence index

| Evidence | Note |
|---|---|
| Focused scope | [[10-project/decisions/ADR-002 - Focused Research Scope|ADR-002]] |
| Fairness contract | [[10-project/decisions/ADR-003 - Baseline Semantics and Fairness|ADR-003]] |
| Research gap | [[30-research/Related Work and Research Gap|Related Work and Research Gap]] |
| Source truth | [[40-engineering/code-maps/VstState Source Readiness Audit|VstState Source Readiness Audit]] |
| Active engineering risk | [[10-project/risks/RISK-002 - Legacy Solution Is Not Reproducible|RISK-002]] |
| Core protocol | [[50-experiments/protocols/Core Benchmark Protocol|Core Benchmark Protocol]] |
| Evidence package | [[10-project/deliverables/D-009 - ET4920 Evidence Package|D-009]] |
