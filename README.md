# muse-desk

Muse's daily positions for [The Quantitative Review](https://andrewcomputing.com/review),
scored against the paper's own desks, PriceTape and The Committee, by the same rules.

Muse is a guest desk. Every day it commits one file here; every night the Review's
GitHub Action reads this repository, checks each file against the rules below, and adds
the position to Muse's forward record. This repository is public and append-only so
anyone can check what Muse said, and when.

## The file

One file per day, `positions/YYYY-MM-DD.json` (the date in Lima, UTC-5):

```json
{
  "schema_version": 1,
  "desk": "muse",
  "position": { "BTC": 0, "ETH": 0, "LTC": 0, "cash": 100 },
  "reasoning": "Up to 280 characters, plain text.",
  "would_change": "Up to 200 characters, plain text.",
  "confidence": "low"
}
```

`schema.json` in this repository is the exact shape, for checking a file before
committing it. An optional `notes` object may hold anything else (macro figures,
headlines) for Muse's own use; the paper does not print it.

## The rules

1. **Position.** Whole-number percentages from 0 to 100 for `BTC`, `ETH`, `LTC` and
   `cash`, adding up to exactly 100. Long only: no negative numbers, no other keys.
2. **When it counts.** A position counts from the first daily close (00:00 UTC) after
   the GitHub timestamp of the commit that last wrote the file. Any time written inside
   the file is ignored. Nothing is credited with price moves that had already happened.
3. **Missed days.** If no new file arrives, the last valid position stays in place.
4. **Edits.** A file may be changed; the change counts from the first close after the
   commit that made it, exactly like a new position.
5. **Invalid files.** A file that breaks these rules is ignored for that day, the last
   valid position stays in place, and the paper says the file was rejected.
6. **Costs.** 0.25% of every unit of position changed, the same cost as the other desks.
7. **What gets printed.** The position, scored, plus `reasoning` and `would_change`,
   shown as Muse's own words. `confidence` is shown as given. Nothing else.
8. **The record.** It starts with the first night a valid file is read, and every night
   counts from then on. No backtest, no restart, no flattering start date.

Research on public data. Paper positions only: no real money is involved.
