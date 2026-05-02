---
title: Era-Relative Scoring
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: [game-design.md, Hall of Fame system, Ring of Honor system]
tags: [legacy, scoring, fairness]
---
# Era-Relative Scoring

Legacy scoring (Hall of Fame, Ring of Honor) uses **seasonal rankings** instead of fixed stat thresholds. This prevents early-era players from dominating or being shut out as league averages shift over decades of simulation.

## The Problem

In a long-running franchise, league-wide stat averages drift. Passing yards per game in season 1 might average 220; by season 30 it could be 260. A fixed threshold like "4,000 passing yards = Hall of Fame candidate" would be nearly impossible early on and trivially easy later.

## The Solution: Rank-Based Points

Instead of comparing raw stats to fixed thresholds, the system ranks players within their own season:

| Rank | Points |
|------|--------|
| 1st  | 6      |
| 2nd  | 5      |
| 3rd  | 4      |
| 4th  | 3      |
| 5th  | 2      |
| 6th  | 1      |

A quarterback who leads the league in passing yards in season 3 earns the same 6 points as one who leads in season 30 — regardless of the raw yardage difference. This makes career accumulation fair across any era.

## Where It Applies

- **Hall of Fame** — Career legacy scores determine eligibility. Rank-based seasonal points accumulate over a career.
- **Ring of Honor** — Team-level legacy recognition uses the same rank-based system scoped to franchise history.

## Why Not Percentiles?

With 32 teams and limited roster sizes, the population per position per season is small. Percentile-based scoring would create false precision. Rank-based points with a top-6 cutoff are robust to small sample sizes and easy to reason about.

## See Also

- [[engine-lock]]
- [[read-only-layers]]
