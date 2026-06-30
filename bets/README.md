# Bet records

One JSON file per bet, named `YYYY-MM-DD-home-vs-away.json`, committed **before
kickoff**. The git commit timestamp is the proof-of-time.

## Schema

| Field | Meaning |
|---|---|
| `match` | Fixture and competition |
| `kickoff_utc` | Scheduled kickoff (UTC) |
| `venue` | Stadium (neutral for WC) |
| `model` | Model recipe version used |
| `probabilities` | Model blend probs `[home, draw, away]` |
| `model_xg` | Model expected-goals line |
| `bet` | The selection taken |
| `odds` | Decimal odds taken |
| `implied_prob` | 1 / odds |
| `model_prob` | Model probability for the selection |
| `edge_pp` | model_prob − implied_prob, in percentage points |
| `ev` | Expected value of the bet, `model_prob × odds − 1` |
| `stake_eur` | Stake in euros |
| `staking_method` | Sizing rule used |
| `potential_profit_eur` | Profit if the bet wins |
| `result` | `pending` / `win` / `loss` (filled after the match) |
