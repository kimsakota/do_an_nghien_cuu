---
id: RUN-{{date:YYYYMMDD}}-{{time:HHmm}}
type: experiment-run
status: running
project: "[[10-project/Project VstState|Project VstState]]"
specification: ""
research_question: ""
hypothesis: ""
commit: ""
dataset: ""
seed: ""
environment: ""
raw_data: ""
checksum: ""
started_at: "{{date:YYYY-MM-DD}} {{time:HH:mm}}"
ended_at: ""
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!danger] Near-immutable run record
> Sau khi status là **completed**, không sửa số liệu hay command. Nếu sai, đánh dấu **invalid**, nêu lý do và tạo run mới. ^run-integrity

## Manifest

| Field | Value |
|---|---|
| Specification | [[|]] |
| Commit/tag |  |
| Machine |  |
| CPU / RAM |  |
| OS / kernel |  |
| Runtime / GC |  |
| Backend |  |
| Dataset / seed |  |
| Threads |  |
| Start / end |  |

## Exact command

~~~powershell

~~~

## Environment snapshot

~~~text

~~~

## Raw data

- Path:
- Checksum:
- File count / size:
- Collector version:

## Result snapshot

| Metric | Value | Unit | Notes |
|---|---:|---|---|
| Throughput |  | ops/s |  |
| p50 |  | µs |  |
| p95 |  | µs |  |
| p99 |  | µs |  |
| Memory/state |  | bytes |  |

^run-result

## Observations

> [!note] Observation, không phải claim
> Mô tả điều đo được trong run này, không tổng quát hóa vượt scope.

## Anomalies / deviations

> [!warning]
> - Protocol deviation:
> - Noise:
> - Failed samples:
> - Reason to invalidate:

## Completion checklist

- [ ] Exit code và logs đã lưu.
- [ ] Raw data có checksum.
- [ ] Commit clean/reproducible.
- [ ] Deviation đã ghi.
- [ ] Status set **completed** hoặc **invalid**.
- [ ] Link vào analysis.