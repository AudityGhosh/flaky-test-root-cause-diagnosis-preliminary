# Flaky Test Root-Cause Diagnosis

Preliminary empirical study of **evidence requirements for automated flaky-test root-cause diagnosis**.

## Research Question

> What evidence is necessary and sufficient for reliable flaky-test root-cause diagnosis?

The study investigates whether different evidence sources—issue descriptions, failure logs, runtime information, and source/execution paths—provide different diagnostic value.

## Pilot Study

- **Dataset:** RustFT / FTW
- **Pilot cases:** 15 labeled flaky tests
- **Root-cause categories:** Randomness, Network, Async Wait, Concurrency, Logic, Time, I/O, Unordered Data, and Hard to Classify
- **Approach:** Controlled evidence ablation using progressively richer evidence packages.

| Condition | Evidence | Accuracy |
|---|---|---:|
| P0 | Issue description | 20% |
| P1 | + Failure evidence | 20% |
| P2 | + Runtime evidence | 40% |
| P3 | + Source/execution-path evidence | 40% |

These are **preliminary results from a small pilot** and are not intended as general performance claims.

