---
id: ARCH-001
type: architecture
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
areas:
  - systems
  - networking
created: 2026-09-16
updated: 2026-09-16
aliases:
  - VstState Architecture
tags:
  - needs-review
---

# System Architecture

> [!abstract]
> Kiến trúc tách workload/protocol khỏi state backend để correctness, benchmark và UPF-like pipeline có thể dùng chung abstraction. ^architecture-summary

## Context diagram

~~~mermaid
flowchart LR
  CTL[Control operations] --> SB[IStateBackend]
  PKT[GTP-U packet] --> PARSER[Parser]
  PARSER --> SB
  SB --> D[Dictionary]
  SB --> C[ConcurrentDictionary]
  SB --> V[VstState]
  SB --> H[Hybrid optional]
  SB --> RULE[PDR/FAR-like state]
  RULE --> ACT[Forward / Drop / Count]
~~~

## Component responsibilities

| Component | Responsibility | Must not own |
|---|---|---|
| VstState | Store/index/lifetime | UPF protocol policy |
| VstBench | Generate/measure operations | Hide raw results |
| VstTraffic | Reproducible workload trace | Backend-specific shortcuts |
| VstUPF-Lab | Packet → key → state → action | Full 5G core |
| VstResults | Preserve/process evidence | Rewrite raw run data |
| VstPaper | Communicate claims | Introduce unsupported numbers |

## Quality attributes

1. Correctness and memory safety.
2. Reproducibility.
3. Throughput and tail latency.
4. Memory efficiency.
5. Concurrency scalability.
6. Explainability via profiling.
7. Linux portability.

## Open decisions

- [ ] Ownership and reclamation model.
- [ ] Key/value layout contract.
- [ ] Concurrency strategy.
- [ ] Persistence boundary.
- [ ] Hybrid architecture entry gate.

## Links

- Interface: [[./IStateBackend|IStateBackend]]
- Protocol: [[./Core Benchmark Protocol|Core Benchmark Protocol]]
- RQs: [[./Research Hub|Research Hub]]