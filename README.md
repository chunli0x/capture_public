# Capture: Decentralized RLHF

Humans review a vision model's outputs. Consensus decides who gets paid. A slashable stake prices every review.

**Capture** is a mobile RLHF preference-review network. A reviewer sees two
vision-model outputs and picks the better one (A/B preference) or rates a
single output 1–5. Aggregated preferences form an RLHF preference dataset,
with trust priced into every review through a slashable $SKR bond.

Live on **Solana devnet** with test tokens: no production money, no production claims.

## How it works

**Onboard → Stake → Review → Settle.**

1. **Onboard.** Complete a liveness check, then pass 10 known-consensus pairs before you can stake or earn.
2. **Stake.** Stake $SKR to unlock paid reviewing. Your stake is the collateral at risk if you farm.
3. **Review.** Pick the better of two outputs, or rate one 1–5. "Can't tell" is always allowed and never penalized.
4. **Settle.** Three reviewers see each pair; the 2/3 majority pick wins. Agree and earn USDC; dissent earns nothing; farming is warned, then slashed.

Your agreement rate drives your level and payout multiplier, from Scout through Pathfinder.

See the full flow at [capture.fun/how-it-works.html](https://capture.fun/how-it-works.html).

## Screenshots

<p align="center">
  <img src="images/screenshots/01-judge-mountains.jpg" alt="Review: A/B preference" width="18%"/>
  <img src="images/screenshots/02-judge-interior.jpg" alt="Review: interior scene" width="18%"/>
  <img src="images/screenshots/03-calibrate-guide.jpg" alt="Calibrate: how to review" width="18%"/>
  <img src="images/screenshots/04-calibrate-standing.jpg" alt="Calibrate: standing by your answer" width="18%"/>
  <img src="images/screenshots/05-balances.jpg" alt="Balances: earnings and level ladder" width="18%"/>
</p>

## Architecture

<p align="center"><img src="images/architecture.png" alt="Capture architecture: Android client, scoring API, Solana settlement" width="720"/></p>

Android client → scoring API (calibration, three-reviewer consensus, accuracy ladder) → Solana settlement ($SKR bond escrow, warn/slash, treasury). A Merkle anchor commits each resolved batch on-chain.

<p align="center"><img src="images/user-flow.png" alt="Capture user flow" width="720"/></p>

## Benchmark

Our vision quality-judge grades every submission against the capture spec
before acceptance. On a 45-sample labeled set it scored **71.1%**: a measured
baseline.

## Test suite (measured 2026-10-29)

Backend 212 passed / 10 skipped · Rust 15 · Android 67.

## Honest lines

- Test $SKR and USDC on devnet: no production money, no production claims.
- Majority-preference bias is real: RLHF on majority preference flattens minority views.
- 18+, self-attested: not a cryptographic proof of age.
- Built for Android.

## Links

- [capture.fun](https://capture.fun): live product site
- [Terms](https://capture.fun/terms.html) · [Privacy](https://capture.fun/privacy.html)
