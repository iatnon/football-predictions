# Bet records

One JSON file per bet (or per multi-leg match — one file can carry more than
one leg, see the `bets[]` array below), named
`YYYY-MM-DD-home-vs-away.json`, committed **before kickoff**. The git commit
timestamp is the proof-of-time. This convention is unchanged from the WC2026
chapter into the club season.

## Schema

The current (multi-leg) shape is the primary schema; every field below has
appeared in a real bet file. Not every field is present on every record —
older WC2026 files used a flatter single-leg shape (a top-level `bet` /
`odds` / `stake_eur` instead of a `bets[]` array); both shapes are left as-is
in history (append-only, never rewritten).

### Top-level fields

| Field | Meaning |
|---|---|
| `match` | Fixture, e.g. `"Home Team vs Away Team"` |
| `competition` | Competition / league name |
| `kickoff_utc` | Scheduled kickoff (UTC) |
| `venue` | Stadium (neutral for WC; home ground for club fixtures) |
| `model` | Model recipe version used (e.g. `v20clean` 3-seed ensemble for club season) |
| `lineups_confirmed` | `true`/`false` — whether the confirmed XI was in hand at logging time |
| `confirmed_lineup_note` | Free-text confirmed starting lineups for both sides, when available |
| `probabilities` | Model probs `{home_win, draw, away_win}` (or named per team) |
| `model_xg` | Model expected-goals line per side + total |
| `odds` | Decimal odds taken, per market outcome |
| `note_on_odds` | Free-text note when the placed price drifted from the price the stake was sized against |
| `bets` | **Array of every leg placed on this match** — see per-leg fields below. Every leg clearing the +3pp edge threshold is included, not just the single highest-edge leg. |
| `placed` | `true`/`false` — whether the bet(s) were actually placed |
| `excluded_legs_note` | Free-text note on legs that did **not** clear the edge threshold and why |
| `total_stake_eur` | Sum of `stake_eur` across all legs in `bets[]` |
| `logged_pre_kickoff` | Timestamp the record was committed, pre-kickoff |
| `result` | Free-text settlement summary once the match is final (`pending` before then) |
| `final_score` | Final score / notable settlement detail (e.g. AET, shootout) |
| `profit_eur` | Net P/L in euros across all legs, filled after settlement |
| `bankroll_after_eur` | Bankroll after this match's P/L is applied |
| `coupon_ids` | Bookmaker bet-slip / coupon reference ID(s), when recorded |
| `verification` | Free-text pointer to slip screenshot or other proof, when recorded |
| `potential_return_eur` | Total potential return (stake + profit) across all legs if all won |

### Per-leg fields (inside `bets[]`)

| Field | Meaning |
|---|---|
| `leg` | The selection taken, e.g. `"Home win"`, `"Draw"`, `"Away win"` |
| `odds` | Decimal odds taken for this leg |
| `implied_prob` | 1 / odds |
| `model_prob` | Model probability for this leg |
| `edge_pp` | `model_prob − implied_prob`, in percentage points (threshold: ≥ 3.0) |
| `ev` | Expected value of this leg, `model_prob × odds − 1` |
| `stake_eur` | Stake in euros for this leg |
| `staking_method` | Sizing rule used, with the arithmetic shown (e.g. half-Kelly fraction, cap check) |
| `potential_profit_eur` | Profit if this leg wins |
| `potential_return_eur` | Stake + profit if this leg wins |
