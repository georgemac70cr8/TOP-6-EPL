# Top 6 Predictions

A Premier League 2026/27 "top 6" predictions pool tracker for 9 players. €20 buy-in each (€180 pot), scored automatically against the live table.

**Scoring:** for each of a player's 6 predicted teams — 10 points for an exact position match, 7 for one position off, 5 for two off, 1 for three-or-more off (still top 6), 0 if the team isn't in the real top 6 at all. Max 60 points.

## How it stays live

The page fetches Premier League results directly from the [openfootball](https://github.com/openfootball/football.json) public dataset (`2026-27/en.1.json`, no API key needed) every time it's opened, and again every 5 minutes while left open. It computes the current league table itself from match results (points → goal difference → goals scored; head-to-head is not applied, so it can differ slightly from the official table on rare ties), works out each predicted team's current position, and re-scores everyone. There's also a "Refresh now" button for an on-demand update.

If openfootball's GitHub source is briefly unreachable, it automatically falls back to a jsdelivr mirror of the same file.

## Files

- `index.html` — the entire app (self-contained, no build step, no dependencies)
- `predictions.json` — the 9 players' picks, the prize pool, and the prize split. Edit this file directly if a pick needs correcting or the split changes.

## Deploying

1. Push this folder to a new GitHub repo.
2. Go to [vercel.com/new](https://vercel.com/new), import the repo. No framework preset needed — Vercel serves static files by default. Leave build command and output directory blank.
3. Deploy. That's it — every visit refetches live data, so there's nothing to re-deploy as the season progresses (only `predictions.json` ever needs an edit/commit, e.g. to fix a pick).

## Local preview

Any static file server works, e.g.:

```
npx serve .
```

(Opening `index.html` directly via `file://` won't work — the browser blocks the fetch of `predictions.json` under that protocol.)

## Adjusting things later

- **Prize split:** edit `prizeSplit` in `predictions.json`.
- **A pick was wrong:** edit that player's array in `predictions.json`.
- **Team name not showing up right:** add an entry to `SHORT_NAME_MAP` near the top of the `<script>` in `index.html` — it matches by substring, so e.g. `"newcastle"` would map any "Newcastle United FC" variant.
