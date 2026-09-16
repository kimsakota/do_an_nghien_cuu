---
id: CMP-VSTSTATE-MEMORY
type: component
status: draft
project: "[[10-project/Project VstState|Project VstState]]"
areas:
  - memory-management
created: 2026-09-16
updated: 2026-09-16
aliases:
  - Memory Manager
tags:
  - needs-review
---

# VstState Memory Manager

> [!abstract]
> Component chịu trách nhiệm region/slab/slot ownership và lifetime; correctness của allocate/free/reuse quan trọng hơn mọi claim zero-allocation. ^component-summary

## Responsibilities

- Reserve/commit memory regions.
- Allocate fixed/size-class slots.
- Track free/used state.
- Enforce alignment.
- Reclaim safely under concurrency.
- Expose metrics: reserved, committed, used, fragmentation.

## Invariants

> [!danger]
> - Không double allocation một slot.
> - Không use-after-free.
> - Không reuse trước khi reader an toàn.
> - Metrics phải reconcile với ownership state.
> - Shutdown/dispose không leak.

## State model

~~~mermaid
stateDiagram-v2
  [*] --> Free
  Free --> Reserved: allocate
  Reserved --> Live: initialize
  Live --> Retired: remove
  Retired --> Free: safe reclamation
~~~

## Dependencies

- [[./Slab Allocator|Slab Allocator]]
- [[./Virtual Memory|Virtual Memory]]
- [[./Memory Reclamation|Memory Reclamation]]
- [[./Test Strategy|Test Strategy]]

## Verification

- [ ] Single-thread property tests.
- [ ] Stress test under concurrency.
- [ ] Long-run leak test.
- [ ] Invalid free detection.
- [ ] Counter reconciliation.