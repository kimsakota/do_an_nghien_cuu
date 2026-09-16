---
id: WRITE-PAPER
type: paper-section
status: outline
project: "[[10-project/Project VstState|Project VstState]]"
created: 2026-09-16
updated: 2026-09-16
tags:
  - paper
---

# Paper Outline

> [!abstract]
> Candidate paper is a **characterization + mechanism + transfer** story. Final headline is selected only after confirmatory evidence.

1. Abstract — problem, method, one bounded result, artifact.
2. Introduction — exact gap and contributions.
3. Background/Related Work — position against NF state systems and KV engines.
4. Semantics and VstState Design.
5. Experimental Methodology.
6. RQ-01 Trade-off Results.
7. Compact-layout Mechanism Ablation.
8. UPF-like Transfer Study.
9. Discussion, negative results and limitations.
10. Reproducibility statement.
11. Conclusion.

## Allowed title patterns after evidence

- “Characterizing …” for descriptive/conditional findings.
- “When Compact State Layouts Help …” only if operating regions are repeatable.
- Avoid “High-Performance”, “Scalable” or “Cache-Efficient” in final title unless evidence supports the adjective.

## Submission gate

- [ ] One sentence contribution survives adversarial review.
- [ ] Related work gap is updated and non-absolute.
- [ ] Same-semantics baseline reviewed.
- [ ] Mechanism has ablation/counters.
- [ ] End-to-end result has a proper counterfactual.
- [ ] Artifact independently rerun.
- [ ] No figure/manual number without script + raw hash.
