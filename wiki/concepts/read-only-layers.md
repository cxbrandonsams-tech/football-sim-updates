---
title: Read-Only Layers
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: [architecture, narrative system, almanac system]
tags: [architecture, separation, narrative]
---
# Read-Only Layers

Narrative systems and the Almanac are **read-only layers**. They consume simulation outputs but never influence game outcomes.

## The Pattern

The simulation engine is a pure function: given team rosters, gameplans, and random seeds, it produces game results deterministically. Systems built on top of the engine fall into two categories:

1. **Engine systems** — Directly participate in simulation (play calling, player ratings, injury rolls). These are subject to [[engine-lock]].
2. **Read-only layers** — Post-process simulation outputs for display, storytelling, or historical analysis. These can be extended freely because they cannot break game balance.

## How It Works

```
Simulation Engine (pure)
    ↓ outputs
Game Results, Stats, History
    ↓ consumed by
[Narrative] [Almanac] [Awards] [Hall of Fame] [Ring of Honor]
    ↓ produces
News stories, records, rankings, legacy scores
```

Read-only layers observe the world but do not act on it. A rivalry narrative might declare "Team A dominates Team B" based on head-to-head records, but this narrative has zero effect on the next Team A vs. Team B simulation.

## Why This Matters

Without strict separation, feature creep corrupts game balance:

- "Rivalry games should be closer" leads to outcome manipulation
- "Dynasty teams should attract better free agents" turns narrative into gameplay
- "Record-chasing players should get stat boosts" creates feedback loops

By enforcing read-only access, these layers can be as creative and expressive as needed without any risk to the simulation's integrity.

## Implementation

Read-only layers receive data through:
- Post-game stat objects
- Season history arrays
- Career aggregation queries

They never receive references to mutable game state, team objects, or player rating objects. The data flows one direction only.

## See Also

- [[engine-lock]]
- [[document-ownership]]
- [[system-status-matrix]]
