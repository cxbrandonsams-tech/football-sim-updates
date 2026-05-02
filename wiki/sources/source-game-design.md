---
title: "Source: game-design.md"
type: source
created: 2026-04-05
updated: 2026-04-05
sources: [docs/game-design.md]
tags: [ratings, pipeline, design, locked]
---

# Source: game-design.md

**File:** `docs/game-design.md`
**Date:** 2026-03-29
**Status:** LOCKED

## Summary

Canonical reference for player ratings (16 positions), overall formulas, and simulation pipeline architecture. Defines the pass pipeline (6 sequential phases) and run pipeline (5 sequential phases) with detailed phase interactions.

## Key Content

- 16 position types with unique rating sets (QB 8 ratings, RB 5, WR 5, TE 6, OL 4, DL 4, LB 7, CB 7, Safety 7)
- QB hidden sub-ratings: shortAccuracy, mediumAccuracy, deepAccuracy — set to 50 in scoutedRatings, never expose in UI
- Safety derived stat: Range = Speed*0.6 + Awareness*0.4 (hidden)
- Run contact: Power OR Elusiveness (not blended)
- Speed only triggers in open-field breakaway

## Wiki Pages Updated
- [[player-ratings]]
- [[simulation-engine]]

## See Also
- [[source-engine-state]]
- [[source-locked-values]]
