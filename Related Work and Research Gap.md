---
id: RW-GAP-001
type: literature-synthesis
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
areas:
  - state-management
  - network-functions
  - key-value-store
tags:
  - related-work
  - research-gap
---

# Related Work and Research Gap

> [!abstract]
> Note này giới hạn contribution bằng nguồn sơ cấp. Mục tiêu không phải chứng minh VstState “đầu tiên”, mà xác định câu hỏi còn thiếu trong **selected literature** và thiết kế evaluation trả lời đúng câu hỏi đó.

## Evidence map

| Work | Primary focus | State/data model | What it contributes | Boundary relative to this project |
|---|---|---|---|---|
| [OpenNF — SIGCOMM 2014](https://opennf.cs.wisc.edu/publications) | Coordinated control of NF state and forwarding during redistribution | NF state across instances | APIs/control plane for move/copy/share with event ordering | Không trực tiếp so sánh compact managed-memory store với same-semantics concurrent hash baseline |
| [FlexState — IEEE Access 2021](https://doi.org/10.1109/ACCESS.2021.3061814) | Decouple NF packet logic from selected data store | State abstraction + drivers | Flexible state backend abstraction with NF evaluation | Trọng tâm là flexibility/decoupling; không trả lời trade-off compact layout dưới dynamic per-flow workload của đề tài |
| [FASTER — SIGMOD 2018](https://www.microsoft.com/en-us/research/publication/faster-concurrent-key-value-store-place-updates/) | Concurrent point operations, in-place update, larger-than-memory state | General key–value records + hybrid log | Cache-optimized concurrent index and update-intensive KV design | Là advanced related baseline, nhưng problem envelope gồm persistence/larger-than-memory chứ không phải controlled UPF-like per-flow case |
| [FlowBlaze — NSDI 2019](https://www.usenix.org/conference/nsdi19/presentation/pontarelli) | Stateful packet processing in programmable hardware | Per-flow EFSM state | Expressive stateful processing at SmartNIC/FPGA scale | Khác hardware/runtime và research question; hữu ích để đặt VstState vào landscape |
| [.NET ConcurrentDictionary documentation](https://learn.microsoft.com/en-us/dotnet/api/system.collections.concurrent.concurrentdictionary-2) | Thread-safe in-process key/value operations | Managed-memory concurrent hash map | Mainstream same-runtime baseline | Baseline, không phải bằng chứng rằng VstState tốt/xấu hơn |

## Synthesis

- NF literature nhấn mạnh abstraction, redistribution, consistency, programmability hoặc hardware packet processing.
- High-performance KV literature nhấn mạnh concurrency, update path, persistence và working set lớn.
- Các hướng này xác nhận state access là một systems problem có thật, nhưng cũng cảnh báo rằng “state store nhanh” phụ thuộc semantics, workload, runtime và level of integration.
- Vì vậy đề tài phải tách ba lớp evidence: **trade-off**, **mechanism**, **end-to-end impact**.

> [!question] Defensible gap
> Trong tập tài liệu sơ cấp đã khảo sát, chưa có câu trả lời trực tiếp cho câu hỏi: **một compact in-memory state store trên managed runtime tạo trade-off nào về bytes/live-state, throughput và p99 so với concurrent hash baseline có cùng semantics dưới lookup/update/insert/delete per-flow workloads; và trade-off đó còn có ý nghĩa bao nhiêu trong pipeline UPF-like khi thay duy nhất backend?**

^gap-statement

## Novelty position

> [!success]
> Novelty được đặt ở **evaluation package có kiểm soát + mechanism ablation + UPF-like transfer**, không đặt ở tuyên bố mơ hồ “dùng cấu trúc compact là mới”.

## Search expansion protocol

Trước khi đóng Chương Related Work:

- [ ] Backward/forward snowball từ OpenNF, FlexState, FASTER và FlowBlaze.
- [ ] Tìm thêm state management cho NFV/UPF, concurrent maps trên managed runtime và cache-conscious layout.
- [ ] Ghi search strings, database, ngày tìm và inclusion/exclusion.
- [ ] Cập nhật gap nếu tìm thấy công trình trả lời gần như trực tiếp.
- [ ] Xin GVHD review wording novelty.

## Citation hygiene

- Nguồn ở bảng là starting set, không phải systematic review hoàn tất.
- Mọi câu “không có”, “đầu tiên”, “vượt trội” đều bị cấm nếu không có protocol review tương ứng.
- Dùng primary paper/spec cho technical claim; blog chỉ làm navigation.
