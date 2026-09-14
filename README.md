# Flaky Test Root-Cause Diagnosis

Preliminary empirical study of **evidence requirements for automated flaky-test root-cause diagnosis**.

## Research Question

> **What evidence is necessary and sufficient for reliable flaky-test root-cause diagnosis?**

The study investigates how different evidence sources contribute to diagnosis rather than assuming that providing more context always improves performance.

## Dataset

The experiments use a pilot subset of **15 labeled flaky tests** from the **RustFT/FTW** dataset, covering nine root-cause categories:

* Randomness
* Network
* Async Wait
* Concurrency
* Logic
* Time
* I/O
* Unordered Collections
* Hard to Classify

## Models & Baselines

### Keyword Baseline

A simple rule-based baseline using root-cause-related keywords from the available evidence.

### BART-large-MNLI

A pretrained **BART-large-MNLI** zero-shot classification model is used to evaluate diagnosis under different evidence conditions.

The project does **not** fine-tune BART; the pilot evaluates how its predictions change as additional evidence is provided.

## Evidence Representation

Evidence is divided into five types:

| ID     | Evidence                                                           |
| ------ | ------------------------------------------------------------------ |
| **E0** | Issue description                                                  |
| **E1** | Failure evidence — logs, error messages, stack traces              |
| **E2** | Runtime evidence — execution behavior and runtime information      |
| **E3** | Source/execution-path evidence                                     |
| **E4** | External artifacts — commits, PRs, and related repository evidence |

## Evidence Ablation

Evidence is added cumulatively to measure its incremental diagnostic value:

| Condition   | Evidence               |    Accuracy |
| ----------- | ---------------------- | ----------: |
| **P0**      | E0                     |         20% |
| **P1**      | E0 + E1                |         20% |
| **P2**      | E0 + E1 + E2           |         40% |
| **P3**      | E0 + E1 + E2 + E3      |         40% |
| **P3 + E4** | E0 + E1 + E2 + E3 + E4 | Exploratory |

The P0–P3 results are based on the 15-case pilot using BART-large-MNLI. The E4 experiment is exploratory and uses only two cases, so it is not treated as a reliable performance estimate.

## Key Preliminary Observation

Adding **runtime evidence (E2)** increased pilot accuracy from **20% to 40%** in the BART-based ablation, while adding source/execution-path evidence (E3) did not produce an additional improvement.

This is only a preliminary observation from a small pilot and requires validation on a larger evaluation set.

## Explainability

The longer-term goal is to move beyond category prediction toward **evidence-grounded root-cause diagnosis**, consisting of:

```text
Root-cause category
        ↓
Causal mechanism
        ↓
Responsible location / artifact
        ↓
Supporting evidence
        ↓
Natural-language explanation
```

Explanations will be evaluated for diagnosis correctness and whether their claims are actually supported by the available evidence.




## Status

**Preliminary research / pilot study**

Current work focuses on validating evidence requirements, expanding the evaluation set, improving annotation reliability, and developing a more concrete and evidence-grounded diagnosis framework.
