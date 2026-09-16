---
id: PROTO-ENV
type: protocol
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - environment
  - provenance
---

# Benchmark Environment and Provenance

> [!warning] Development snapshot — not benchmark-approved
> Các giá trị dưới đây được tự động đọc ngày 2026-09-16 để làm dev baseline. Confirmatory host phải được capture lại ngay trước run.

## Current development host

| Field | Observed |
|---|---|
| CPU | 11th Gen Intel Core i5-11400H @ 2.70 GHz |
| Logical processors | 12 |
| Architecture | x64 |
| OS | Windows NT build 10.0.26200.0 |
| .NET SDK | 10.0.301 |
| .NET host/runtime | 10.0.9 |
| RID | win-x64 |
| global.json | not present |

## Missing before approval

- [ ] Physical cores, cache hierarchy and RAM configuration.
- [ ] Power plan/governor, turbo policy and thermal state.
- [ ] Exact target framework and GC mode.
- [ ] BIOS/microcode and virtualization status where relevant.
- [ ] Background process policy and CPU affinity.
- [ ] Linux host/profile for hardware counters if Windows collector is insufficient.
- [ ] Repository commit, dirty flag and build flags.

## Per-run manifest

```yaml
run_id:
experiment:
commit:
dirty:
build:
backend:
backend_config:
key_bytes:
value_bytes:
initial_capacity:
live_states:
occupancy:
workload:
trace_sha256:
seed:
workers:
warmup_s:
measurement_s:
runtime:
gc_mode:
cpu:
os:
affinity:
collector:
started_at:
raw_path:
raw_sha256:
correctness_checksum:
validity:
```

## Provenance rule

Manifest and raw file are immutable after run. Correction creates a new analysis/run record; it never silently edits source evidence.
