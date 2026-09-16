---
id: SYS-VAULT-GUIDE
type: guide
status: active
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - system
---

# Vault Guide

> [!abstract] Mục đích
> Vault này là **knowledge/control plane** cho ET4920: đủ rõ cho người, có cấu trúc cho AI, và giữ được chuỗi truy vết từ câu hỏi nghiên cứu tới bằng chứng.

## Nguyên tắc kiến trúc

1. **Folder** cho biết note thuộc quy trình nào.
2. **Link** diễn tả quan hệ có nghĩa.
3. **Property** cung cấp trạng thái có thể lọc bằng Bases/Search.
4. **Tag** chỉ dùng cho tín hiệu ngang hiếm gặp như **needs-review** hoặc **blocked**.
5. Một note chỉ có một trách nhiệm chính.
6. Mọi số liệu hiệu năng phải lần ngược được tới Experiment Run và raw data.

## Bản đồ vault

| Prefix | Vai trò | Loại note chính |
|---|---|---|
| 00-system | Điều hành vault | dashboard, guide, template, AI context |
| 01-inbox | Capture chưa xử lý | inbox |
| 10-project | Quản lý A–Z | project, milestone, deliverable, risk |
| 20-learning | Học và ôn | course, concept, lab, question |
| 30-research | Logic khoa học | research-question, hypothesis, claim |
| 40-engineering | Thiết kế hệ thống | architecture, component, code-map, adr |
| 50-experiments | Bằng chứng thực nghiệm | protocol, experiment-spec, experiment-run, analysis |
| 60-writing | Artifact cuối | thesis-section, paper-section, defense |
| 70-logs | Nhật ký | daily, weekly, meeting |
| 80-library | Nguồn | source, paper, standard, book, oss-project |
| 90-dashboards | View động | base |
| 99-archive | Lịch sử | legacy, archived |
| assets | Ảnh và tệp nhỏ | image, diagram |

## Luồng chuẩn

~~~mermaid
flowchart LR
  A[Course / Source] --> B[Concept]
  B --> C[Research Question]
  C --> D[Hypothesis]
  D --> E[Experiment Spec]
  E --> F[Experiment Run]
  F --> G[Analysis]
  G --> H[Claim]
  H --> I[Thesis / Paper]
~~~

> [!warning] Không được nhảy cóc
> Không tạo claim chỉ từ intuition, expected result hay tài liệu legacy. Claim phải liên kết evidence có nguồn gốc rõ.

## Quy tắc đặt tên

- Note kỹ thuật ưu tiên English/ASCII; dùng **aliases** cho tiếng Việt.
- ID dùng prefix ổn định: RQ, H, CLM, EXP, RUN, ADR, M, D, RISK.
- Không dùng tên mơ hồ như “note1”, “final-new”, “s”.
- Daily note: **YYYY-MM-DD**.
- Experiment run: **RUN-YYYYMMDD-HHmm - short-name**.

## Quy tắc nội dung

> [!check] Một note tốt
> - 2–5 dòng summary ở đầu;
> - properties đúng schema;
> - ít nhất một link ra ngoài note;
> - tách rõ Fact / Hypothesis / Observation / Claim;
> - có Next action nếu note chưa hoàn tất.

## Tạo note mới

1. Tạo file đúng folder.
2. Chạy **Templates: Insert template**.
3. Điền các property bắt buộc.
4. Thêm liên kết ngược về hub/MOC cha.
5. Nếu note sinh công việc, tạo task có ngữ cảnh hoặc Deliverable note.

Xem [[./Templates Guide|Templates Guide]] và [[./Property Dictionary|Property Dictionary]].