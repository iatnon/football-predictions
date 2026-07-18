# Bankroll ledger

Starting bankroll: **€100.00**

| # | Date (UTC) | Match | Bet | Odds | Stake | Result | P/L | Bankroll after |
|---|---|---|---|---|---|---|---|---|
| 1 | 2026-06-30 | Ivory Coast vs Norway (WC2026 R32) | Norway win | 2.15 | €11.20 | ✅ win | +€13.08 | €113.08 |
| 2 | 2026-06-30 | France vs Sweden (WC2026 R32) | France win | 1.32 | €3.43 | ✅ win | +€1.10 | €114.18 |
| 3 | 2026-07-01 | England vs DR Congo (WC2026 R32) | England win | 1.30 | €4.99 | ✅ win | +€1.50 | €115.68 |
| 4 | 2026-07-01 | Belgium vs Senegal (WC2026 R32) | Belgium win | 2.10 | €5.78 | ✅ win (3-2) | +€6.36 | €122.04 |
| 5 | 2026-07-09 | Morocco vs France (WC2026 QF) | France win | 1.60 | €10.00 | ✅ win (2-0) | +€6.00 | €128.04 |
| 6 | 2026-07-10 | Spain vs Belgium (WC2026 QF) | Belgium win | 5.75 | €3.00 | ❌ loss (2-1) | -€3.00 | €125.04 |
| 7 | 2026-07-11 | Norway vs England (WC2026 QF) | Norway win | 4.50 | €10.00 | ❌ loss (aet, 2-1) | -€10.00 | €115.04 |
| 8 | 2026-07-11 | Argentina vs Switzerland (WC2026 QF) | Argentina win (2 legs: 1.70 + 1.73) | 1.70 / 1.73 | €20.00 | ✅ win (aet, 3-1) | +€14.30 | €129.34 |
| 9 | 2026-07-14 | Spain vs France (WC2026 SF) | Spain win | 3.20 | €9.00 | ✅ win (2-1) | +€19.80 | €149.14 |
| 10 | 2026-07-15 | Argentina vs England (WC2026 Semifinal) | Argentina win | 3.10 | €11.00 | ✅ win | +€23.10 | €172.24 |
| 11 | 2026-07-19 | France vs England (WC2026 3rd place playoff) | Draw + England win (double) | 4.30 / 4.40 | €2.00 + €12.00 = €14.00 | ⏳ pending | — | — |

**Settled bankroll:** **€172.24** (10 of 11 bets resolved, 1 pending).

Record: 11 bets, 8 wins, 2 losses, 1 pending.

*(Correction: bet #10 was originally logged as "WC2026 Final" — it was actually the semifinal. Argentina won and advanced to face Spain (who beat France, bet #9) in the Final.)*

## Staking method (with dated rule changes)

Current rule (since 2026-07-07): **half-Kelly, capped at 8% of settled bankroll, rounded up to the nearest whole euro**:
`stake = ceil_to_euro( min( 0.5 × fullKelly × bankroll, 0.08 × bankroll ) )`

Rule-change history (no silent changes — every sizing deviation is dated here):
- **2026-06-30 → 2026-07-05: quarter-Kelly, 5% cap** (bets #1–#3). Bet #4 was a one-off flat-5% override (quarter-Kelly would have given €1.04 on a thin +4.0% EV edge).
- **2026-07-06: switched to half-Kelly, 5% cap.** Quarter-Kelly (and the prob-scaled variant tried internally) over-suppressed moderate-probability, moderate-edge picks.
- **2026-07-07: cap raised 5% → 8%.** Half-Kelly on high-probability, high-edge picks (e.g. p≈0.50, EV +17%) was being clipped by the 5% cap; 8% chosen over 10%/flat-7% alternatives.
- **2026-07-11: bet #8 (Argentina-Switzerland) doubled** — cap-bound €10 leg at 1.70, plus a second user-directed €10 leg at 1.73 after the price moved. Not a rule change, a one-off double.
- **2026-07-11: bet #7 (Norway-England) was a sub-threshold override** — flat €10 at only +1.6% EV (below the +3% candidate threshold), user-directed, not sized per formula.
- **2026-07-14: bet #9 (Spain-France) was user-directed at €9.00**, close to but not exactly the half-Kelly/8%-cap formula output.

Bet #5 sizing: full-Kelly 23.5%, half-Kelly 11.7% → 8% cap binds → 0.08 × €122.04 = €9.76 → **€10.00**.
Bet #6 sizing: full-Kelly 3.4%, half-Kelly 1.7% (well under cap) → 0.017 × €122.04 = €2.07 → **€3.00**.
Bet #8 sizing: full-Kelly 32.0%, half-Kelly 16.0% → 8% cap binds → 0.08 × €122.04 = €9.76 → **€10.00** (leg 1); leg 2 was a €10 user-directed double at the moved price (1.73).
Bet #10 sizing: full-Kelly 13.8%, half-Kelly 6.9% (under cap) → 0.069 × €149.14 = €10.28 → **€11.00**.
Bet #11 sizing (double, user-directed like bet #8): Draw leg full-Kelly 1.4%, half-Kelly 0.7% → 0.007 × €172.24 = €1.19 → **€2.00**. England win leg full-Kelly 13.1%, half-Kelly 6.5% (under cap) → 0.065 × €172.24 = €11.28 → **€12.00**. Both sized pre-placement at 3.85/3.95; actual placed odds drifted to 4.30/4.40 per bet-slip screenshot, stakes unchanged.
