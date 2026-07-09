# Bankroll ledger

Starting bankroll: **€100.00**

| # | Date (UTC) | Match | Bet | Odds | Stake | Result | P/L | Bankroll after |
|---|---|---|---|---|---|---|---|---|
| 1 | 2026-06-30 | Ivory Coast vs Norway (WC2026 R32) | Norway win | 2.15 | €11.20 | ✅ win | +€13.08 | €113.08 |
| 2 | 2026-06-30 | France vs Sweden (WC2026 R32) | France win | 1.32 | €3.43 | ✅ win | +€1.10 | €114.18 |
| 3 | 2026-07-01 | England vs DR Congo (WC2026 R32) | England win | 1.30 | €4.99 | ✅ win | +€1.50 | €115.68 |
| 4 | 2026-07-01 | Belgium vs Senegal (WC2026 R32) | Belgium win | 2.10 | €5.78 | ✅ win (3-2) | +€6.36 | €122.04 |
| 5 | 2026-07-09 | Morocco vs France (WC2026 QF) | France win | 1.60 | €10.00 | *pending* | — | €112.04 staked / €122.04 settled |

**Current exposure:** €10.00 open on bet #5.
**Settled bankroll:** **€122.04** (4 of 5 bets resolved).

Record: 5 bets, 4 wins, 0 losses, 1 pending.

## Staking method (with dated rule changes)

Current rule (since 2026-07-07): **half-Kelly, capped at 8% of settled bankroll, rounded up to the nearest whole euro**:
`stake = ceil_to_euro( min( 0.5 × fullKelly × bankroll, 0.08 × bankroll ) )`

Rule-change history (no silent changes — every sizing deviation is dated here):
- **2026-06-30 → 2026-07-05: quarter-Kelly, 5% cap** (bets #1–#3). Bet #4 was a one-off flat-5% override (quarter-Kelly would have given €1.04 on a thin +4.0% EV edge).
- **2026-07-06: switched to half-Kelly, 5% cap.** Quarter-Kelly (and the prob-scaled variant tried internally) over-suppressed moderate-probability, moderate-edge picks.
- **2026-07-07: cap raised 5% → 8%.** Half-Kelly on high-probability, high-edge picks (e.g. p≈0.50, EV +17%) was being clipped by the 5% cap; 8% chosen over 10%/flat-7% alternatives.

Bet #5 sizing: full-Kelly 23.5%, half-Kelly 11.7% → 8% cap binds → 0.08 × €122.04 = €9.76 → **€10.00**.
