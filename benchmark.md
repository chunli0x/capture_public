# Capture: Vision Quality-Judge Evaluation

**Evaluation date:** 2026-10-12. **Dataset:** 45 labeled samples across 9 classes, 5 per class (balanced). The judge emits a single accept/reject verdict per submission; this report measures that verdict against the fixed benchmark labels.

## Evaluation design

The benchmark is a held-out, labeled set spanning the capture-spec dimensions: ground-level framing, real photo (not screenshot), no watermark, sharpness, and exposure. One class is an intended accept case (`accept_ground_level`); the other eight are specific reject cases (blank, blown-out, blur, eye-level, screenshot, static wall, underexposed, watermark). Per-sample dimension scores produced by the vision model are thresholded into a verdict; the labels are the ground truth the verdict is scored against. Labels are authored fixtures, not independently double-reviewed human gold: see Limitations.

## Overall result

**Accuracy 71.1% (32/45 correct).** Wilson 95% confidence interval: **56.6%–82.3%**. With N=45 this is a point-in-time measurement, not an established population rate.

## Confusion (reject treated as positive class)

| | Predicted reject | Predicted accept |
|---|---|---|
| Label reject | **27** (correct rejects) | **13** (false-accepts) |
| Label accept | **0** (false-rejects) | **5** (correct accepts) |

- **False-accept rate: 13/40 = 32.5%**: nearly one in three reject cases was accepted.
- **False-reject rate: 0/5 = 0%**: no accept case was wrongly rejected.
- **Reject precision: 100% (27/27)**: every rejection the judge issued was correct.
- **Reject recall: 67.5% (27/40; Wilson 95% CI 52.0%–79.9%)**: the judge misses about a third of bad content.
- **Accept precision: 27.8% (5/18)**: of the 18 samples the judge accepted, only 5 were actually acceptable.

## Per-class results

| Class (label) | n | Correct | Recall (correct/labeled) | False-accepts |
|---|---|---|---|---|
| accept_ground_level (accept) | 5 | 5 | 100% |: |
| reject_blank | 5 | 5 | 100% | 0 |
| reject_blur | 5 | 5 | 100% | 0 |
| reject_screenshot | 5 | 5 | 100% | 0 |
| reject_underexposed | 5 | 4 | 80% | 1 |
| reject_watermark | 5 | 4 | 80% | 1 |
| reject_blown_out | 5 | 2 | 40% | 3 |
| reject_static_wall | 5 | 2 | 40% | 3 |
| reject_eye_level | 5 | 0 | 0% | 5 |

Per-class precision is not separable: the judge returns a single accept/reject verdict, not a per-class label, so precision is defined only at the binary decision level (reject 100%, 27/27; accept 27.8%, 5/18). The per-class recall above is the correct-rejection rate for each reject class and the correct-accept rate for the accept class.

## Failure slices

- **Eye-level framing: 0/5 (0%).** The judge accepted all five eye-level captures. This is a systematic failure, not noise: eye-level framing is never caught and blocks any claim of framing robustness.
- **Blown-out exposure: 2/5 (40%), 3 false-accepts.** The missed samples pass the exposure dimension, so the exposure check is not driving the verdict for these cases.
- **Static wall: 2/5 (40%), 3 false-accepts.** Static-wall samples pass sharpness and real-photo scoring and slip through on framing.

## Limitations

- **N=45 is small.** The 56.6%–82.3% accuracy interval and the 5-per-class recall estimates carry wide uncertainty; no class can be characterized finer than 0/5–5/5 resolution.
- **Labels are single-authored fixtures**, not dual-reviewed human gold with recorded adjudication. Per evaluation methodology this narrows the claim to "agreement with the fixed benchmark labels," not population-level grading quality.
- **No calibration/threshold split.** Dimension-score thresholds were not fit on a separate calibration set, so per-dimension threshold tuning is not evidenced in this benchmark.
- **No abstention path.** The judge always returns a verdict; there is no "unresolved" label to absorb low-confidence samples.

## Next steps

1. Add eye-level negatives and re-examine the framing/ground-level threshold that lets them through; 0/5 must be resolved before framing robustness is claimed.
2. Expand the locked test to ≥20 samples per class to tighten per-class recall confidence intervals.
3. Introduce a calibration split to fit dimension thresholds before any locked-test re-measurement.
4. Record dual-reviewer labels and adjudication for the test set to upgrade label provenance.

All tokens referenced are test tokens on Solana devnet.
