---
title: Simulation Engine
type: entity
created: 2026-04-05
updated: 2026-04-05
sources: [ENGINE_STATE.md, game-design.md, LOCKED_VALUES.md]
tags: [engine, locked, simulation]
---
# Simulation Engine

The simulation engine is the locked core of the football simulation. It processes every play through deterministic pipelines that produce realistic NFL-caliber outcomes.

## Pass Pipeline (6 Phases)

1. **Protection** — OL pass blocking vs DL pass rush. Determines pocket time and pressure.
2. **Separation** — WR/TE route running vs CB/S coverage. Generates windows of opportunity.
3. **Decision** — QB reads the field using Awareness, Vision, and Decision Speed ratings.
4. **Throw** — Accuracy and arm strength determine ball placement and velocity.
5. **Catch** — Receiver hands, contested catch ability, and defender disruption.
6. **YAC** — Yards after catch driven by speed, elusiveness, and open-field context.

## Run Pipeline (5 Phases)

1. **Blocking** — OL run blocking grades vs DL gap defense. Creates or collapses lanes.
2. **Vision** — RB vision rating identifies the best available gap.
3. **Engagement** — First contact: Power OR Elusiveness check (never blended).
4. **Contact** — Tackle attempt resolution at the point of attack.
5. **Breakaway** — Speed-only check triggers in open field for big gains.

## TUNING Constants

Frozen constants in the `TUNING` object (`engine/config.ts`). These values are locked and calibrated against NFL baselines:

- **21.4 PPG** average points per game
- **39.5%** third-down conversion rate
- **67.3%** completion percentage

All constants are immutable after calibration. Changes require re-validation against the full baseline suite.

## See Also

- [[player-ratings]]
- [[playbook-system]]
