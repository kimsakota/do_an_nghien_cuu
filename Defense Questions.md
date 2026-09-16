---
id: WRITE-DEFENSE-QA
type: defense
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - defense
---

# Defense Questions

> [!tip] Answer pattern
> **Direct answer → evidence → limitation → implication.** Never begin with implementation detail before answering the question.

## Contribution and novelty

> [!question]
> - Đóng góp khoa học là algorithm mới, system mới hay evaluation mới?
> - Vì sao gap không chỉ là “chưa ai benchmark code của em”?
> - Prior work gần nhất là gì và project khác ở đâu?
> - Nếu VstState thua ConcurrentDictionary, đồ án còn đóng góp gì?
> - Vì sao chỉ hai RQ là đủ cho ET4920?

## Fairness and correctness

> [!question]
> - Hai backend có đúng cùng semantics không?
> - Dictionary có phải baseline concurrent công bằng không?
> - Làm sao biết throughput cao không đến từ bỏ qua update/lost data?
> - Capacity/load factor/memory reserved được tính thế nào?
> - Linearizable per-key được kiểm tra tới đâu?

## Measurement and statistics

> [!question]
> - Vì sao 10 repetitions? Pilot chứng minh measurement window ra sao?
> - Vì sao dùng median/bootstrap thay vì chỉ mean/p-value?
> - p99 sampling có đủ mẫu và có coordinated omission không?
> - Exclusion nào được đặt trước? Run lỗi có bị xóa không?
> - Practical threshold 10–15% lấy căn cứ và được ai duyệt?
> - Thermal/JIT/GC/order effects được kiểm soát ra sao?

## Mechanism

> [!question]
> - Memory thấp hơn có chứng minh locality tốt hơn không?
> - EXP-003 thực sự chỉ thay một factor chứ?
> - Counter hardware có bị multiplex/virtualization làm sai không?
> - Nếu LLC misses giảm nhưng p99 xấu hơn thì kết luận gì?
> - Index, layout và sharding được tách khỏi nhau thế nào?

## UPF-like relevance

> [!question]
> - Pipeline giống và khác UPF thật ở điểm nào?
> - TEID/PDR/FAR được mô hình hóa ra sao?
> - Vì sao Null backend cần thiết?
> - Microbenchmark effect chuyển thành end-to-end effect thế nào?
> - Vì sao không tuyên bố line-rate/3GPP compliance?

## Research integrity

> [!question]
> - Claim nào thuộc prior work, claim nào do project tạo?
> - Figure này truy về raw data, commit và checksum nào?
> - Kết quả âm/inconclusive quan trọng nhất là gì?
> - Threat lớn nhất với external validity?
> - Nếu reviewer tái chạy không giống, quy trình debug là gì?

## Mock-defense scoreboard

| Date | Reviewer | Contribution | Rigor | Systems | UPF | Integrity | Top fix |
|---|---|---:|---:|---:|---:|---:|---|
|  |  |  |  |  |  |  |  |
