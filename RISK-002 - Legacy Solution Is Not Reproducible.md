---
id: RISK-002
type: risk
status: active
project: "[[10-project/Project VstState|Project VstState]]"
probability: high
impact: critical
owner: Kim Sakota
created: 2026-09-16
updated: 2026-09-16
tags:
  - reproducibility
  - source
---

# RISK-002 — Legacy Solution Is Not Reproducible

> [!danger]
> The solution references missing Test/Benchmark projects and the repository is dirty. Any performance number produced now would lack a clean, rebuildable evidence baseline.

## Trigger

- solution build fails with MSB3202;
- code under test cannot be identified by clean commit;
- correctness or benchmark projects are absent;
- unsafe warnings remain unexplained.

## Impact

- benchmark cannot be independently rerun;
- regression/correctness status is unknown;
- claims may accidentally describe a different code state;
- schedule is consumed by repair late in the project.

## Mitigation

- follow [[./VstState Source Readiness Audit|Source Readiness Audit]];
- freeze a clean baseline before new architecture work;
- enforce build/test/checksum gate in CI;
- prohibit confirmatory runs until resolved.

## Contingency

If legacy repair cost is excessive, create a minimal clean research solution that wraps only audited primitives; document what was reused and keep the legacy tree read-only.
