# football-predictions

Public, timestamped track record of pre-kickoff football bets placed with a
blind-WC2022-validated prediction model.

The model itself is private. This repo publishes only the **outputs** — the
prediction, the odds taken, the stake, and the result — so the track record is
tamper-evident: each bet is committed to git **before kickoff**, and the commit
timestamp proves it.

## The model (summary)

Final probability = **0.5 × transformer + 0.5 × confed-adjusted draw-aware Elo**,
neutral venue, strongest-XI path. Validated on blind WC2022; the blend beats both
pure transformer and pure Elo out of sample.

## Bankroll & staking

- **Starting bankroll:** €100.00
- **Staking rule:** fractional Kelly (quarter-Kelly) on legs clearing EV ≥ +3%,
  capped by the project's flat-5% sanity rule for sizing discipline.
- A bet is only a candidate if `model_prob × decimal_odds − 1 ≥ 0.03`.
- Longshots (odds ≥ ~6.0) and ultra-short favorites (odds ≤ ~1.20) are distrusted.
- Over/Under 2.5 is never bet (no backtested edge). 1X2 is the primary market.

## Files

- [`bankroll.md`](bankroll.md) — running bankroll ledger.
- [`bets/`](bets/) — one JSON file per bet, committed before kickoff.
- [`bets/README.md`](bets/README.md) — bet record schema.

## Disclaimer

For research and track-record purposes only. Not financial advice. Bet
responsibly.
