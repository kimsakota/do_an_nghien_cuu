---
id: ADR-003
type: adr
status: accepted
project: "[[10-project/Project VstState|Project VstState]]"
date: 2026-09-16
decision_makers:
  - Kim Sakota
created: 2026-09-16
updated: 2026-09-16
tags:
  - benchmark
  - fairness
  - semantics
---

# ADR-003 — Baseline Semantics and Fairness

> [!success] Decision
> Mọi backend phải thực hiện cùng observable contract. Dictionary chỉ là **single-thread reference**; ConcurrentDictionary và VstState là core concurrent comparison. Không benchmark một backend với semantics yếu hơn để lấy tốc độ.

## Frozen observable semantics

| Operation | Contract |
|---|---|
| TryGet | trả snapshot/copy đầy đủ của value tại một linearization point; false nếu absent |
| TryAdd | thêm khi absent; false nếu duplicate; không overwrite ngầm |
| TryUpdate | thay toàn bộ value khi present; false nếu absent |
| TryRemove | xóa và trả removed value/copy; false nếu absent |
| Count | exact chỉ tại quiescent checkpoint; không tính vào hot-path throughput |
| Enumeration | ngoài core benchmark; không dùng để tạo claim |

- Key là immutable và có cùng representation logic ở mọi backend.
- Value payload/logical fields giống hệt; physical size được ghi trong manifest.
- Concurrent operations phải linearizable **per key** theo contract trên.
- Không trả writable reference làm thay đổi semantics của backend.
- Preallocation/capacity/load factor phải được khai báo; memory metric tính cả reserved capacity có thể sử dụng.
- Trace, seed, initial state và success/failure outcome distribution phải tương đương.

## Validation before timing

1. Sequential differential test với Dictionary oracle.
2. Generated operation trace gồm success/failure cases và boundary keys.
3. Concurrent invariant tests: no lost acknowledged update, no duplicate live key, final checksum/count match quiescent oracle.
4. Fault/exception path được ghi; correctness failure hủy validity của timing run.

## Fairness record per run

- backend/version/configuration;
- key/value physical and logical bytes;
- initial capacity and occupancy;
- synchronization mode;
- GC/runtime/build;
- trace hash and seed;
- successful operation ratios;
- correctness checksum.

## Not decided here

Exact C# signature và struct layout phải được đối chiếu code hiện tại trong [[./IStateBackend|IStateBackend]]. Mọi thay đổi observable semantics cần ADR mới hoặc supersede ADR này.
