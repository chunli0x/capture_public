# Capture — Decentralized RLHF

Humans judge a vision model's outputs. Consensus decides who gets paid. A slashable stake prices every judgment.

**Capture** is a mobile RLHF preference-judging network. A judge sees two
vision-model outputs and picks the better one (A/B preference) or rates a
single output 1–5. Aggregated preferences form an RLHF preference dataset,
with trust priced into every judgment through a slashable $SKR bond.

Live on **Solana devnet** with test tokens — no production money, no production claims.

## How it works

**Calibrate → Stake → Judge → Settle.**

1. **Calibrate.** Pass 10 known-consensus pairs before you can stake or earn.
2. **Stake.** Deposit $SKR to unlock paid judging. Your stake is the collateral at risk if you farm disagreement.
3. **Judge.** Pick the better of two outputs, or rate one 1–5. "Can't tell" is always allowed and never penalized.
4. **Settle.** Three judges see each pair; the majority pick wins. Agree and earn; dissent earns nothing; systematic farming is warned, then slashed.

Your agreement rate drives your level and payout multiplier, from Scout through Pathfinder.

See the full flow at [capture.fun/how-it-works.html](https://capture.fun/how-it-works.html).

## Screenshots

<p align="center">
  <img src="images/screenshots/01-judge-mountains.jpg" alt="Judge: A/B preference" width="18%"/>
  <img src="images/screenshots/02-judge-interior.jpg" alt="Judge: interior scene" width="18%"/>
  <img src="images/screenshots/03-calibrate-guide.jpg" alt="Calibrate: how to judge" width="18%"/>
  <img src="images/screenshots/04-calibrate-standing.jpg" alt="Calibrate: standing by your answer" width="18%"/>
  <img src="images/screenshots/05-balances.jpg" alt="Balances: earnings and level ladder" width="18%"/>
</p>

## Architecture

![Capture architecture](images/architecture.png)

Android client → scoring API (calibration, K=3 consensus, accuracy ladder) → Solana settlement ($SKR bond escrow, warn/slash, treasury). A Merkle anchor commits each resolved batch on-chain.

![Capture user flow](images/user-flow.png)

## Benchmark

Our vision quality-judge grades every submission against the capture spec
before acceptance. On a 45-sample labeled set it scored **71.1%** — a measured
baseline that improves as labeled data grows. Full per-class breakdown in
[benchmark.md](benchmark.md).

## Test suite (measured 2026-10-29)

Backend 212 passed / 10 skipped · Rust 15 · Android 67.

## Honest lines

- Test $SKR and USDC on devnet — no production money, no production claims.
- Majority-preference bias is real: RLHF on majority preference flattens minority views.
- Over 18, self-attested — not a cryptographic proof of age.
- Built for Android.

## Links

- [capture.fun](https://capture.fun) — live product site
- [Terms](https://capture.fun/terms.html) · [Privacy](https://capture.fun/privacy.html)
