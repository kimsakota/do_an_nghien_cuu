---
id: METH-EVIDENCE
type: methodology
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Evidence Policy
tags:
  - research-integrity
---

# Evidence Policy

> [!danger] Evidence rule
> Không số liệu nào được dùng như fact/claim nếu không lần ngược được tới **nguồn hoặc raw data + command + commit + environment**. Legacy note và AI output chỉ tạo hypothesis/question, không tạo evidence. ^evidence-rule

## Epistemic labels

| Label | Có nghĩa | Không được hiểu là |
|---|---|---|
| Fact | Nguồn authoritative hoặc quan sát tái hiện được | Universal truth |
| Hypothesis | Dự đoán falsifiable | Kết quả mong muốn |
| Expected result | Planning estimate | Observation |
| Observation | Điều thấy trong scope/run cụ thể | Claim tổng quát |
| Claim | Kết luận có evidence và boundary | Marketing statement |

## Evidence ladder

1. legacy-unverified
2. anecdotal
3. single-run
4. replicated
5. triangulated
6. externally-supported

^evidence-ladder

## Claim gate

Một claim chỉ chuyển **supported** khi:

- statement có scope/baseline/metric;
- experiment spec đã freeze decision rule;
- runs có provenance và hợp lệ;
- repetitions/uncertainty đủ;
- anomaly/evidence against được xử lý;
- wording không vượt external validity;
- limitations được ghi.

## Invalid evidence

- Screenshot không có raw artifact.
- Con số copy từ legacy mà không có source.
- Benchmark thiếu commit/environment.
- Average duy nhất cho workload có tail behavior.
- Run bị protocol deviation nhưng không ghi.
- So sánh backend khác semantics.

## AI instruction

> [!warning]
> Nếu thiếu provenance, AI phải nói **không đủ evidence**, đề xuất cách kiểm tra và không tự điền số hợp lý.