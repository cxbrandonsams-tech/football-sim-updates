---
title: Player Ratings
type: entity
created: 2026-04-05
updated: 2026-04-05
sources: [game-design.md]
tags: [ratings, positions, players]
---
# Player Ratings

16 position types with unique, position-specific rating sets. Every rating must affect simulation — no decorative stats.

## Rating Counts by Position

| Position | Ratings | Notes |
|----------|---------|-------|
| QB | 8 | Includes hidden sub-accuracies (short/medium/deep) |
| RB | 5 | Power OR Elusiveness used at contact (never blended) |
| WR | 5 | Speed only triggers in open-field breakaway |
| TE | 6 | Dual blocking/receiving role |
| OL | 4 | Run blocking and pass blocking separated |
| DL | 4 | Pass rush and run defense |
| LB | 7 | Coverage + run defense hybrid |
| CB | 7 | Man and zone coverage distinctions |
| Safety | 7 + derived | Range = Speed * 0.6 + Awareness * 0.4 (hidden, never exposed in UI) |

## Overall Formulas

Overall ratings weight individual ratings differently per position. The formula ensures that a QB's overall reflects arm talent and decision-making, while a CB's overall emphasizes coverage and athleticism.

## True Ratings vs Scouted Ratings

- **trueRatings** — Used by the engine during simulation. The actual player ability.
- **scoutedRatings** — Visible to the GM. Revealed progressively through the [[scouting-draft]] system. May differ from true ratings until fully scouted.

This dual-layer system creates meaningful scouting decisions and draft risk.

## See Also

- [[simulation-engine]]
- [[scouting-draft]]
- [[playbook-fit-scoring]]
