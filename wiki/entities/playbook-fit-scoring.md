---
title: Playbook Fit Scoring
type: entity
created: 2026-04-05
updated: 2026-04-05
sources: [playbook-fit-scoring-design.md]
tags: [playbooks, fit, ratings]
---
# Playbook Fit Scoring

Scores how well plays fit a roster's strengths on a 0.0 to 1.0 scale. Creates a meaningful link between [[player-ratings]] and [[playbook-system]] selection.

## Rating Demands per Engine Type

Each engineType defines which player ratings matter and their relative weight. Example for `deep_pass`:

| Rating | Weight |
|--------|--------|
| QB deep accuracy | 0.35 |
| QB arm strength | 0.30 |
| WR speed | 0.35 |

Other engine types weight different combinations (e.g., `inside_run` emphasizes OL run blocking and RB power).

## Impact on Gameplay

Fit scoring affects two separate systems:

1. **Selection weight multiplier** (0.7 - 1.3x) — Plays that fit the roster are called more often.
2. **Simulation success bonus** (+/- 9%) — Well-fitted plays execute better on the field.

Combined, this creates a **+/- 15% swing** between a perfectly fitted play and a poorly fitted one.

## Letter Grades

Fit scores are translated to letter grades for GM visibility:

A+, A, A-, B+, B, B-, C+, C, C-, D+, D, D-, F

These grades help the GM understand which playbook configurations maximize their roster's potential.

## See Also

- [[playbook-system]]
- [[player-ratings]]
