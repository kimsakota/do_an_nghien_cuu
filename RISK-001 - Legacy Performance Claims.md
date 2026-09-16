---
id: RISK-001
type: risk
status: active
project: "[[10-project/Project VstState|Project VstState]]"
probability: high
impact: high
owner: Kim Sakota
review_on: 2026-09-23
mitigation: Evidence policy + claim ledger + reproducible experiments
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Legacy claims
tags:
  - legacy-unverified
---

# RISK-001 — Legacy Performance Claims

> [!warning] Risk statement
> Do tài liệu cũ chứa expected hoặc unverified performance numbers, có khả năng người/AI tái sử dụng chúng như kết quả thật, dẫn tới claim sai và làm yếu luận văn. ^risk-statement

## Assessment

| Dimension | Rating | Rationale |
|---|---|---|
| Probability | high | Nhiều tài liệu cũ viết số liệu theo giọng kết luận |
| Impact | high | Ảnh hưởng scientific integrity |
| Detectability | medium | Khó nhận ra nếu mất provenance |
| Urgency | high | Phải kiểm soát trước writing/benchmark |

## Early warning signals

- Số liệu không link tới run/raw data.
- Từ “đã chứng minh”, “nhanh hơn” nhưng thiếu environment/commit.
- AI trích con số từ legacy snapshot.
- Claim không có evidence_level.

## Prevention

- [x] Golden rule trong [[./AI Context#^claim-policy|AI Context]].
- [x] Claim template có provenance checklist.
- [x] Legacy note gắn **legacy-unverified**.
- [ ] Audit mọi con số khi migrate tài liệu cũ.

## Mitigation

**Trigger:** phát hiện số liệu không có provenance trong draft.  
**Action:** hạ claim về proposed, gắn needs-review, truy lại nguồn hoặc thiết kế experiment.  
**Fallback:** bỏ số khỏi thesis nếu không tái hiện được.

## Review log

| Date | Probability | Impact | Signal | Decision |
|---|---|---|---|---|
| 2026-09-16 | high | high | Vault initialized | opened |