---
title: Narrative Systems
type: entity
created: 2026-04-05
updated: 2026-04-05
sources: [NARRATIVE_SYSTEMS_LOCK.md, narrative-systems-design.md]
tags: [narrative, locked, news]
---
# Narrative Systems

A read-only layer over simulation that generates storylines, milestones, records, and rivalries. LOCKED v1 — no modifications without re-validation.

## 5 Modules

### 1. Orchestrator (`narrative.ts`)
Central dispatcher that coordinates all narrative modules after each game simulation. Determines which stories fire and manages deduplication.

### 2. Milestones
- **Single-game milestones** — Notable performances (e.g., 400+ passing yards, 4+ TD games).
- **Career milestones** — Tiered thresholds for career accumulations (e.g., 10,000 yards, 100 TDs).

### 3. Records
Three-stage tracking: **pace** (on track to break) → **near** (within striking distance) → **broken** (new record set). Creates escalating tension through a season.

### 4. Rivalry
- **Structural rivalries** — Division opponents, conference matchups.
- **Persistent heat** — 0-100 scale tracking intensity between teams. Builds from competitive games, playoff meetings, and close outcomes.

### 5. Arcs
Long-running storylines: **undefeated** season chase, **dynasty** runs, **breakout** player seasons, **revenge** game narratives.

## Persistent State

Three objects persist across seasons:
- `rivalries` — Team-pair heat values
- `narrativeArcs` — Active long-running storylines
- `recordChaseState` — Tracking for active record pursuits

**Decay:** 30% reduction per offseason to prevent stale narratives.

**Dedup rules** prevent spam by suppressing duplicate or near-duplicate stories within configurable windows.

## See Also

- [[almanac]]
