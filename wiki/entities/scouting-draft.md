---
title: Scouting & Draft
type: entity
created: 2026-04-05
updated: 2026-04-05
sources: [FRANCHISE_SOURCE_OF_TRUTH.md]
tags: [draft, scouting, college, deprecated]
---

> **Deprecated:** This page describes the old 3-level point-based scouting system (750-point pool, 3 scouting levels). It was replaced by the 4-stage confidence-based scouting pipeline in April 2026. See `CLAUDE.md` (Scouting System section) for the current system.

# Scouting & Draft

The scouting and draft system generates prospect classes, allows progressive evaluation, and runs a 7-round draft with AI-driven team picking.

## Draft Class Generation

~300 prospects per draft class, distributed across all position groups with realistic talent distribution.

## Scouting System

- **Flat 750-point scouting pool** per team, per draft cycle.
- **3 scouting levels** with increasing cost and detail:

| Level | Cost | Detail |
|-------|------|--------|
| Level 1 | 5 points | Basic overview, wide rating ranges |
| Level 2 | 15 points | Narrower ranges, key ratings revealed |
| Level 3 | 30 points | Near-complete picture, hidden true ratings revealed progressively |

Scouted ratings (visible to the GM) converge toward true ratings as scouting level increases. See [[player-ratings]] for the trueRatings vs scoutedRatings distinction.

## College Layer

5 conferences provide cosmetic flavor (school names, conference prestige). The college layer is cosmetic — it does not affect player ratings or development.

## Draft Execution

- **7 rounds** with all 32 teams picking.
- **AI picking** is needs-based — teams evaluate roster holes and draft accordingly.
- **Draft history** is persisted at draft completion for the [[almanac]] Past Drafts tab.

## See Also

- [[player-ratings]]
- [[almanac]]
