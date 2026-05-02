---
title: "Source: ENGINE_STATE.md"
type: source
created: 2026-04-05
updated: 2026-04-05
sources: [docs/ENGINE_STATE.md]
tags: [engine, metrics, locked]
---

# Source: ENGINE_STATE.md

**File:** `docs/ENGINE_STATE.md`
**Date:** 2026-04-05
**Status:** LOCKED

## Summary

Final validation snapshot comparing simulation output against NFL baselines from 1000+ game sample. Documents accepted structural gaps and all post-lock mechanical additions.

## Key Metrics

| Stat | Sim Value | NFL Target |
|------|-----------|------------|
| PPG | 21.4 | 22-24.5 |
| 3rd-down conversion | 39.5% | 39-42% |
| QB completion | 67.3% | 64-67.5% |
| Sacks/team | 2.4 | 2.3-2.8 |

## Post-Lock Additions
Penalty system (6 types), PAT/2PT conversion, talent gap compression (0.80x), trailing team boost, special teams scoring, safeties (1-yard threshold), clock model (15-min quarters), two-minute drill, NFL overtime rules.

## Wiki Pages Updated
- [[simulation-engine]]

## See Also
- [[source-locked-values]]
- [[source-game-design]]
