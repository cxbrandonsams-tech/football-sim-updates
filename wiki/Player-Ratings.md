# Player Ratings

Football Sim uses position-specific ratings. There are no generic "athleticism" or "skill" buckets shared by every player.

## The Two Layers

- `trueRatings` are the engine values used in simulation.
- `scoutedRatings` are what you see as a GM, with scouting noise applied until the player is fully known.
- `overall` is derived from true ratings.
- `scoutedOverall` is derived from scouted ratings.

The gap between `trueRatings` and `scoutedRatings` is the scouting game.

## Personality Ratings

Every non-kicker/punter also carries personality ratings:

- `workEthic` helps progression and training outcomes.
- `loyalty` lowers contract friction.
- `greed` raises contract demands.

These ratings matter even though they are not shown as traditional on-field stats.

## Position Families

| Position | Core Ratings |
|---|---|
| QB | Arm strength, pocket presence, mobility, short/medium/deep accuracy, processing, decision-making |
| RB | Speed, elusiveness, power, vision, ball security |
| WR | Speed, route running, hands, YAC, size |
| TE | Speed, route running, hands, YAC, size, blocking |
| OL | Pass blocking, run blocking, awareness, discipline |
| DL | Pass rush, run defense, discipline |
| LB | Pass rush, run defense, coverage, speed, pursuit, awareness, discipline |
| CB | Man coverage, zone coverage, ball skills, speed, size, awareness, discipline, tackling |
| Safety | Man coverage, zone coverage, ball skills, speed, size, awareness, discipline, tackling |
| K / P | Kick power, kick accuracy, composure |

## Hidden Rules

- Safety range is hidden and derived from speed and awareness.
- Scouting noise shrinks as scouting level rises.
- Rookies, free agents, and veterans can all be compared on the same scale because the engine uses the same position-specific formulas for everyone.

## Why It Matters

The game rewards building around your actual roster shape:

- Better line play changes the pass and run engines.
- Better receivers do not help if the quarterback cannot process or throw accurately.
- A high-overall player can still be a poor fit for your scheme if the relevant ratings do not line up.
