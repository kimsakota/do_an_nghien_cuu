---
id: EXP-{{date:YYYYMMDD}}-{{time:HHmm}}
type: experiment-spec
status: planned
project: "[[10-project/Project VstState|Project VstState]]"
research_question: ""
hypothesis: ""
baselines: []
metrics: []
owner: ""
due: ""
created: "{{date:YYYY-MM-DD}}"
updated: "{{date:YYYY-MM-DD}}"
aliases: []
tags: []
---

# {{title}}

> [!warning] Pre-registration
> Chốt protocol, primary metric, exclusions và decision rule **trước khi xem kết quả**. Mọi thay đổi sau đó phải ghi deviation. ^experiment-contract

## Objective

Experiment này trả lời điều gì mà evidence hiện tại chưa trả lời?

## Design matrix

| Dimension | Values |
|---|---|
| Backends |  |
| Dataset sizes |  |
| Workloads |  |
| Thread counts |  |
| Seeds |  |
| Repetitions |  |
| Warmup |  |
| Measurement window |  |

## Metrics

| Metric | Unit | Collection method | Primary? |
|---|---|---|---:|
| Throughput | ops/s |  | ✓ |
| Latency | p50/p95/p99 |  |  |
| Memory/state | bytes |  |  |
| Allocation | bytes/op |  |  |

## Controlled environment

- CPU / governor:
- RAM:
- OS / kernel:
- Runtime / GC:
- Affinity:
- Background services:
- Build mode:
- Commit/tag:

## Procedure

1. ...
2. ...
3. ...

## Exact commands

~~~powershell
# setup

# warmup

# run

~~~

## Data contract

**Raw path:**  
**Naming:**  
**Schema:**  
**Checksum:**  
**Retention:**  

## Analysis plan

- Summary statistics:
- Uncertainty:
- Outlier policy:
- Plot set:
- Statistical test/effect size:
- Multiple-comparison handling:

## Decision rules

> [!question] Support / refute / inconclusive
> - Support when ...
> - Refute when ...
> - Inconclusive when ...

## Threats to validity

| Threat | Class | Mitigation |
|---|---|---|
| JIT/warmup | internal |  |
| Synthetic workload | construct |  |
| Single machine | external |  |
| Sample uncertainty | conclusion |  |

## Readiness checklist

- [ ] Correctness tests pass.
- [ ] Baselines use comparable semantics.
- [ ] Metrics collector validated.
- [ ] Dry run completed.
- [ ] Storage path exists.
- [ ] Spec reviewed.
- [ ] Status changed to **ready**.