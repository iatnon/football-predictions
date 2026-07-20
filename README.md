# football-predictions

Public, timestamped track record of pre-kickoff football bets placed with a
leak-audited prediction model.

The model itself is private. This repo publishes only the **outputs** — the
prediction, the odds taken, the stake, and the result — so the track record is
tamper-evident: each bet is committed to git **before kickoff**, and the commit
timestamp proves it.

## The model (summary) — club season 2026-27

Predictions come from the **v20clean 3-seed ensemble**, a lineup-aware club
transformer (52 leagues, 48,927 players, train cutoff 2024-08-01, leak-audited:
+4.53% CE-lift vs an Elo baseline). Bets are taken against **Unibet (unibet.nl)**
prices — currently the best odds available to us — at t-15min with confirmed
lineups in hand. Every leg (home / draw / away) whose edge is **≥ 3 percentage
points** (`model_prob − 1/decimal_odds`) is logged, not just the single
highest-edge leg per match.

### WC2026 (completed chapter)

The repo opened on the **2026 FIFA World Cup**, using a
blind-WC2022-validated recipe — final probability = 0.5 × transformer +
0.5 × confed-adjusted draw-aware Elo, neutral venue, strongest-XI path — bet
against Bet365. That chapter is closed: **12 bets, 9-3, €100.00 → €196.04
(+96.0%)**. Full record in [`bankroll.md`](bankroll.md). The €196.04 settled
bankroll carries forward as the starting bankroll for the club season.

## Bankroll & staking

- **Starting bankroll (current chapter):** €196.04 (carried over from the
  settled WC2026 bankroll).
- **Staking rule (since 2026-07-07, unchanged into the club season):**
  half-Kelly, capped at 8% of settled bankroll, rounded up to the nearest
  whole euro:
  `stake = ceil_to_euro( min( 0.5 × fullKelly × bankroll, 0.08 × bankroll ) )`
  where `fullKelly = (p × odds − 1) / (odds − 1)`. Full dated rule-change
  history is in [`bankroll.md`](bankroll.md).
- A bet is only a candidate if `model_prob × decimal_odds − 1 ≥ 0.03` (edge
  ≥ 3 percentage points vs the raw Unibet price, never de-vigged).
- Longshots (odds ≥ ~6.0) and ultra-short favorites (odds ≤ ~1.20) are distrusted.
- Over/Under 2.5 is never bet (no backtested edge). 1X2 is the primary market.

## Files

- [`bankroll.md`](bankroll.md) — running bankroll ledger.
- [`bets/`](bets/) — one JSON file per bet, committed before kickoff.
- [`bets/README.md`](bets/README.md) — bet record schema.

## Disclaimer

For research and track-record purposes only. Not financial advice. Bet
responsibly.
