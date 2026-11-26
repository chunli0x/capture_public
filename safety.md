# Safety Benchmark

A content-safety classifier that flags unsafe responses. Measured on a
110-scenario adversarial hold-out across five safety rules. Fine-tuning turns
an out-of-distribution baseline that flags nearly everything into a classifier
that catches violations with a manageable false-positive rate.

**Status: preliminary.** Gold labels are model-authored (not independently
verified by human annotators). This is a directional before/after measurement.

**Evaluation date:** 2026-11-24.

## Method

The classifier judges whether a response violates any of five safety rules
(multi-label):

| # | Rule | Description |
|---|---|---|
| 1 | Endearment / pet names | Addressing a user with unsolicited familiar terms. |
| 2 | Hostility / insults | Insulting, belittling, or pressuring the user. |
| 3 | Promises / directives | Claiming future outcomes or directing real-world actions. |
| 4 | Fabricated statements | Presenting invented or contradicted factual claims. |
| 5 | Invented experiences | Claiming physical experiences not supported by the device. |

## Baseline: off-the-shelf decision model (out-of-distribution)

The original safety judge was an off-the-shelf decision model not
designed for these rules. On the 110-scenario hold-out:

| Metric | Value |
|---|---|
| Recall | 0.759 |
| False-positive rate | 0.713 |
| Balanced accuracy | 0.523 |

The baseline catches some violations but has a catastrophic false-positive rate
(71.3%) — it flags nearly everything, making it unusable as a safety gate.

## Fine-tuned (purpose-built)

Fine-tuning a purpose-built classifier for multi-label classification
over the five rules, using 2,000 labeled examples:

**Overall:**

| Metric | Value |
|---|---|
| Recall | 0.830 |
| False-positive rate | 0.148 |
| Balanced accuracy | 0.841 |

**Per-rule:**

| Rule | Precision | Recall | F1 |
|---|---|---|---|
| Endearment | 0.888 | 0.711 | 0.790 |
| Hostility | 0.617 | 0.949 | 0.748 |
| Promises | 0.903 | 0.718 | 0.800 |
| Fabricated | 0.860 | 0.896 | 0.877 |
| Invented | 0.857 | 0.878 | 0.867 |

## Before → after

| Metric | Before (baseline) | After (fine-tuned) | Change |
|---|---|---|---|
| Recall | 0.759 | 0.830 | +7.1 pp |
| False-positive rate | 0.713 | 0.148 | –56.5 pp |
| Balanced accuracy | 0.523 | 0.841 | +31.8 pp |

Fine-tuning reduces the false-positive rate by 5× (71.3% → 14.8%) while
improving recall (75.9% → 83.0%), turning the classifier from unusable to
practical.

## Limitations

1. Gold labels are model-authored, not independently verified by human annotators.
2. 110 scenarios total (n = 110); per-rule positive classes range from 39 to 48 labels.
3. The training distribution (89% multi-rule) may cause the classifier to over-predict overlapping violations.
4. Baseline (out-of-distribution model) was measured on this hold-out; the original documented baseline (recall 0.000, balanced accuracy 0.407) was on a different, earlier eval set and is not directly comparable.

## Data

The 110-scenario eval set (utterances with gold labels) is published as [`safety-eval.jsonl`](safety-eval.jsonl) so the results are independently reproducible. Each line:

```json
{"text": "\u2026", "labels": {"endearment": 0, "hostility": 0, "promises": 0, "fabricated": 1, "invented": 0}}
```

The fine-tuned model weights are not distributed; the method (base model, dataset, training recipe) is described above.