---
id: SYS-AI-CONTEXT
type: ai-context
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - ai-context
---

# AI Context

> [!abstract] Đọc theo thứ tự
> 1. Note này.
> 2. [[./Current Handoff|Current Handoff]].
> 3. Note project/RQ/experiment được giao.
> 4. Chỉ mở source hoặc legacy khi thật sự cần.

## Project

**Vietnamese title:** Nghiên cứu và đánh giá kiến trúc quản lý trạng thái hiệu năng cao cho các chức năng mạng có trạng thái, ứng dụng thử nghiệm trong 5G User Plane Function.

**English title:** Design and Evaluation of High-Performance State Management for Stateful Network Functions: A 5G UPF Case Study.

[[./Project VstState#^project-summary|Project summary]]

## Scope

- VstState state engine.
- VstBench benchmark harness.
- VstTraffic workload generator.
- VstUPF-Lab case-study prototype.
- VstResults raw/processed data and plots.
- VstPaper thesis/paper artifacts.

## Non-scope

- Không xây toàn bộ mạng 5G.
- Không triển khai gNodeB, AMF hoặc SMF hoàn chỉnh.
- Không tuyên bố cạnh tranh trực tiếp với commercial UPF.
- Không mặc định 32-byte layout, zero-GC hay hybrid index là tốt hơn.

## Golden rule

> [!danger] Fact ≠ Hypothesis ≠ Expected result ≠ Observation ≠ Claim
> Không được biến con số trong tài liệu cũ, output AI, expected result hoặc một run đơn lẻ thành fact khoa học. Mỗi claim định lượng phải trỏ tới analysis/run, raw-data path, environment và commit có thể tái hiện. ^claim-policy

## Research chain

**RQ → Hypothesis → Experiment Specification → Experiment Run → Analysis → Claim → Thesis Section**

## Source priority

1. Raw data + script + commit của chính dự án.
2. Standard/specification chính thức.
3. Peer-reviewed paper.
4. Tài liệu dự án upstream.
5. Blog/secondary source.
6. Legacy note hoặc AI-generated text — chỉ dùng để định hướng, không dùng làm evidence.

## Repository access

Dùng [[./Repository Registry|Repository Registry]]. Trong note kỹ thuật luôn ghi:

- repository;
- relative_path;
- commit;
- symbol hoặc line range nếu có;
- trạng thái kiểm chứng.

## Output expectations

- Viết rõ assumption và uncertainty.
- Mọi thay đổi kiến trúc đáng kể tạo hoặc cập nhật ADR.
- Mọi benchmark mới bắt đầu từ Experiment Specification.
- Không sửa số liệu trong run note sau khi run đã chốt; tạo analysis hoặc run mới.
- Handoff phải nêu completed, blockers, next actions và “do not assume”.