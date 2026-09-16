---
id: AUDIT-VST-READINESS-001
type: engineering-audit
status: active
project: "[[10-project/Project VstState|Project VstState]]"
repository: VstHelper
commit: 7.236e+75
created: 2026-09-16
updated: 2026-09-16
tags:
  - source-audit
  - readiness
  - legacy
---

# VstState Source Readiness Audit

> [!danger] Verdict
> Source hiện tại là **legacy foundation**, chưa phải VstState research system mô tả trong proposal. Thư viện riêng build được, nhưng solution-level reproducibility, test/benchmark projects và backend contract chưa sẵn sàng.

## Snapshot

| Check | Evidence | Result |
|---|---|---|
| Repository commit | `7236e72` | captured |
| Working tree | nhiều modified + untracked files | 🔴 dirty; không được coi là reproducible baseline |
| Library target | `VstHelper/VstHelper.csproj` → `netstandard2.0`, unsafe enabled | 🟠 legacy target |
| Library Release build | 0 errors, 10 × CS8500 | 🟠 builds with unsafe managed-pointer warnings |
| Solution Release build | missing `VstHelper.Benchmarks.csproj` and `Test.csproj` | 🔴 fails |
| IStateBackend search | no implementation found | 🔴 absent |
| Test/benchmark source | solution references directories not present in workspace | 🔴 absent |
| Reusable primitives | MemoryPool, KeyIndexer, LockEngine, RawList and low-level utilities exist | 🟢 foundation only |

## Build evidence

**Library**

```text
dotnet build VstHelper/VstHelper.csproj -c Release
Build succeeded. 10 Warning(s), 0 Error(s).
```

Warnings CS8500 occur around pointers to managed/generic types, including `Keys/KeyPath.cs`, `Memory/Memory.cs` and `Memory/StringWriter.cs`. They require correctness/safety review before benchmark claims.

**Solution**

```text
dotnet build VstHelper/VstHelper.sln -c Release
MSB3202: VstHelper.Benchmarks/VstHelper.Benchmarks.csproj not found
MSB3202: Test/Test.csproj not found
Build FAILED.
```

## What can be reused

- allocation/page/slot concepts;
- key/index prototypes;
- lock primitive as an object of audit;
- architecture notes as hypotheses and design history.

## What cannot be claimed yet

- a working VstState backend;
- correctness under concurrency;
- zero-GC/lock-free/cache-efficient behavior;
- a reproducible benchmark suite;
- a runnable UPF-like pipeline.

## Remediation sequence

1. **Preserve baseline:** owner reviews/commits or deliberately snapshots current dirty changes; do not overwrite them.
2. **Repair solution topology:** create/restore test and benchmark projects or remove stale references through an ADR.
3. **Freeze runtime:** choose benchmark TFM/SDK with `global.json`; keep legacy library compatibility decision explicit.
4. **Implement contract adapters:** Dictionary, ConcurrentDictionary, VstState under [[./IStateBackend|IStateBackend]].
5. **Correctness first:** sequential differential + concurrent invariants.
6. **Unsafe audit:** resolve or justify every CS8500 warning; add stress/ASan-equivalent strategy where feasible.
7. **Pilot only after green build/test:** follow [[./Core Benchmark Protocol|Core Protocol]].
8. **Tag evidence commit:** record clean commit and checksum before confirmatory runs.

## Exit criteria

- [ ] Solution builds from a clean checkout.
- [ ] Zero unexplained compiler warnings in research projects.
- [ ] Tests/benchmark projects exist and are included.
- [ ] IStateBackend adapters pass the correctness gate.
- [ ] `global.json`/dependency versions are frozen.
- [ ] Benchmark smoke run emits complete manifest and checksum.
