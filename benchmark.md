# Capture — Vision Judge Benchmark

**Measured** 2026-10-12 against the live judge, not a synthetic eval.

## What we measured

Capture's vision quality-judge grades every submission against the
capture spec before it is accepted: ground-level framing, real photo (not
a screenshot), no watermark, sharpness, and exposure. It returns a single
accept/reject verdict.

## Result

**71.1% accuracy — 32 of 45 labeled samples correct**, across 9 classes.

| Class | Correct |
|---|---|
| Ground-level accept | 5 / 5 |
| Blank | 5 / 5 |
| Blur | 5 / 5 |
| Screenshot | 5 / 5 |
| Underexposed | 4 / 5 |
| Watermark | 4 / 5 |
| Blown-out | 2 / 5 |
| Static wall | 2 / 5 |
| Eye-level | 0 / 5 |

## Error breakdown

- **13 false-accepts** — bad content that should have been rejected but was accepted.
- **0 false-rejects** — no good content was wrongly rejected.

## Honest read

The judge never rejects good content (no false-rejects), but it
over-accepts some bad content, and eye-level framing is its weakest spot
(0 / 5). This is a measured baseline, not a ceiling — accuracy improves
as labeled data grows and the per-dimension scoring is tuned.

All tokens and payouts on Capture are test tokens on Solana devnet.
