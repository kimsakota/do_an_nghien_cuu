---
id: IFACE-ISTATEBACKEND
type: interface-contract
status: review
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - correctness
  - benchmark-contract
---

# IStateBackend

> [!abstract] Observable contract
> ADR-003 đã khóa semantics để benchmark công bằng. Exact signature/struct layout phải được map vào code hiện tại trước khi status chuyển thành **frozen**.

## Logical API

```csharp
bool TryGet(in StateKey key, out StateValue value);
bool TryAdd(in StateKey key, in StateValue value);
bool TryUpdate(in StateKey key, in StateValue value);
bool TryRemove(in StateKey key, out StateValue removed);
long Count { get; } // exact only at a quiescent checkpoint
```

> [!caution]
> Đây là contract-level shape, chưa khẳng định code hiện tại có đúng signature này.

## Semantics

![[./ADR-003 - Baseline Semantics and Fairness#Frozen observable semantics|10-project/decisions/ADR-003 - Baseline Semantics and Fairness > Frozen observable semantics]]

## Representation constraints

- StateKey immutable; identical logical fields and equality/hash inputs.
- StateValue contains identical logical payload across backends.
- No backend receives a smaller payload or weaker durability/concurrency promise in the same comparison.
- Exact physical bytes, alignment and padding are captured in manifest.
- Returned value is a snapshot/copy; writable internal reference is outside core contract.

## Correctness gate

| Test | Purpose | Pass condition |
|---|---|---|
| Sequential differential | compare generated trace with Dictionary oracle | every return/result and final checksum match |
| Duplicate/absent cases | validate false paths | exact expected status/value |
| Concurrent partitioned oracle | detect lost/duplicate acknowledged operations | invariants + final checksum pass |
| Repeatability | same seed/trace | identical logical outcomes |
| Soak | reclamation/corruption | no crash, leak trend or invariant violation |

## Benchmark adapter requirements

- Setup/teardown excluded from timed region.
- Same pre-generated trace or deterministic generator contract.
- Same initial occupancy and target success ratios.
- Adapter may not batch operations unless all backends batch identically.
- Instrumentation mode is recorded and separated from performance mode.

## Freeze checklist

- [ ] Audit current code signatures.
- [ ] Freeze StateKey/StateValue logical schema and sizes.
- [ ] Implement all adapters.
- [ ] Differential suite pass.
- [ ] Concurrent invariant suite pass.
- [ ] Tag benchmark commit.
- [ ] Change status to **frozen**.
