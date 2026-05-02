---
title: Playbook System
type: entity
created: 2026-04-05
updated: 2026-04-08
sources: [FRANCHISE_SOURCE_OF_TRUTH.md]
tags: [playbooks, plays, selection]
---
# Playbook System

37 plays across 5 formations. The playbook system governs play selection, weighting, and situational calling.

## Play Structure

Each play maps to an **engineType** that determines which simulation pipeline processes it:

- `inside_run` — Between the tackles
- `outside_run` — Sweeps, tosses, edge runs
- `short_pass` — Screens, slants, flats
- `medium_pass` — Curls, outs, crossing routes
- `deep_pass` — Go routes, posts, corners

## Playbooks

Playbooks are weighted collections of plays. The **OffensivePlan** maps 13 down/distance buckets to specific playbooks, allowing situational play calling (e.g., different tendencies on 3rd-and-long vs 1st-and-10).

## Weight Modifiers

Play selection weights are modified by multiple factors:

| Modifier | Range | Description |
|----------|-------|-------------|
| Tendency | +/- 25% | Team tendency sliders (run/pass bias, aggressiveness, blitz rate, etc.) — `TeamTendencies` |
| Repetition | 0.4 - 1.0 | Penalizes recently called plays |
| Context | 0.7 - 1.2 | Game situation (score, clock, field position) |
| Meta counter-trend | +/- 10% | Adjusts against league-wide tendencies |
| Fit factor | 0.7 - 1.3x | From [[playbook-fit-scoring]], roster-play alignment |

## PlayConcepts

PlayConcepts are defined in the data model but unused in v1. Reserved for future expansion.

## See Also

- [[playbook-fit-scoring]]
- [[simulation-engine]]
