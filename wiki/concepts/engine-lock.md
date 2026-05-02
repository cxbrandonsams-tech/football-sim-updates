---
title: Engine Lock
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: [DOCS_GUARDRAILS.md, LOCKED_VALUES.md, config.ts]
tags: [philosophy, locked, governance]
---
# Engine Lock

The simulation engine is **locked** after calibration. This is the single most important architectural decision in the project.

## What It Means

After validating against 1,000+ simulated games, every tuning constant in `config.ts` (`TUNING`) was frozen. These values control every probability, threshold, and modifier in the simulation pipeline. Once locked, they do not change.

Post-lock work adds **new mechanics** (penalties, PAT, clock management, overtime) rather than modifying existing ones. Each new mechanic is additive — it plugs into the pipeline without touching the frozen constants.

## Why It Exists

Simulation tuning is a trap. Without a hard lock, every surprising game result becomes a temptation to "fix" a constant. But constants interact in nonlinear ways — adjusting one creates cascading side effects that take hundreds of games to surface. The lock prevents regression by making the tuned state immutable.

[[DOCS_GUARDRAILS.md]] enforces this policy. Any PR that modifies a locked value must provide a statistical justification across a full-season sample.

## Anti-Patterns

- **Reactive tuning** — Changing a constant because one game "felt wrong." Individual game variance is expected and healthy.
- **Arcade mechanics** — Adding dramatic modifiers (clutch bonuses, momentum swings) that override the probability model.
- **Scattered definitions** — Spreading tuning constants across multiple files instead of keeping them centralized in `config.ts`.

## The Lock Process

1. Build the mechanic and its constants
2. Run 1,000+ game validation
3. Verify statistical outputs match target ranges
4. Freeze the constants — they become part of [[LOCKED_VALUES]]
5. Document in [[ENGINE_STATE]]

## See Also

- [[document-ownership]]
- [[read-only-layers]]
- [[vertical-slices]]
