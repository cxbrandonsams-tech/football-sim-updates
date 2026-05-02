# Football Sim Game Design

> **Last updated:** 2026-05-02
> **See also:** [project-overview.md](project-overview.md) | [playbooks-and-formations.md](playbooks-and-formations.md) | [api-reference.md](api-reference.md)

This document summarizes the current public-facing game rules and major systems reflected in the shipped codebase.

## Design Principles

- Ratings only exist if they affect outcomes.
- Core football resolution is sequential, not purely random.
- Vertical slices beat partial systems: each feature ships end-to-end.
- Multiplayer admin flows are first-class product features, not afterthoughts.
- Long-term league history matters as much as a single game result.

## League Rules

- 32 teams across two conferences and four divisions per conference
- 18-week regular season followed by postseason
- 56-man roster cap and 45-player minimum
- $255M salary cap with dead-cap carry from signing bonuses
- Turn-based league progression with commissioner-controlled advancement

## Ratings and On-Field Resolution

The engine uses 16 position groups and position-specific ratings. Ratings feed a layered play pipeline rather than isolated dice rolls.

### Pass pipeline

1. Pre-snap context and concept setup
2. Protection versus pass rush
3. Route development versus coverage
4. QB read and throw execution
5. Catch resolution
6. Yards after catch

### Run pipeline

1. Blocking evaluation
2. Vision and hole selection
3. Initial engagement
4. Contact resolution
5. Breakaway and ball-security outcomes

The live tuning target remains realistic NFL-style output: stable completion rates, sack rates, yards per carry, and scoring without arcade inflation.

## Roster Building and Contracts

- Negotiations evaluate salary, bonus, years, and team fit on a 0-100 interest scale.
- A player generally needs **75+ interest** to sign.
- Extensions, free-agent offers, releases, and fifth-year options all feed the same cap model.
- Bonus money creates dead cap when the player is released.
- Practice squad actions and waiver flows support roster repair and depth management.

## Scouting and Draft

Football Sim uses a four-stage confidence system:

| Stage | Core decision |
|-------|---------------|
| School scouting | Powerhouse or dark-horse school focus |
| Position scouting | Allocate 100% across ten position buckets |
| Targeted scouting | Choose up to five schools |
| Interviews | Choose up to ten prospects for trait reveals |

Confidence narrows prospect uncertainty over time. Low confidence gives wide OVR ranges and softer language; high confidence produces tighter projections, clearer strengths/weaknesses, and better trait visibility.

The scouting surface also supports watch lists, scouting settings, scout directives, and auto-draft helpers.

## Coaching and Progression

The shipped coaching system includes five head-coach archetypes:

- **Developer** — Training Camp rerolls for young players
- **Strategist** — stronger playbook-fit bonuses
- **Motivator** — longer protection against harsh age-related regression
- **Recruiter** — stronger free-agency and scouting outcomes
- **Disciplinarian** — lower incident and penalty pressure

Each staff also includes OC/DC coordinators. Coordinators can be promoted, poached, replaced, and tracked through coaching trees.

Training Camp progression is d20-based. Age, traits, injuries, coach type, and position aging curves all influence whether a player improves, stalls, or declines.

## Schemes, Gameplans, and Playbooks

- Teams can activate up to three offensive and three defensive schemes.
- Identity schemes unlock passive bonuses when the team is built around them.
- Weekly gameplans tune offense and defense separately.
- RB usage splits and passing-down-back assignment are first-class controls.
- Custom offensive and defensive playbooks are supported, including custom plays and clone-first editing.

Detailed formation, slot, and custom-play rules live in [playbooks-and-formations.md](playbooks-and-formations.md).

## Narrative and Historical Systems

The simulation also ships long-horizon presentation systems:

- Rivalries, milestones, and record chases
- Data-driven prose news
- Weekly recap content and season recap pages
- Premium radio-show episodes when OpenAI + R2 are configured
- Replay preservation for important games

Legacy systems are built into normal league progression:

- **Hall of Fame:** 175-point induction threshold, three-season wait, up to seven inductees per year
- **Ring of Honor:** 85-point franchise threshold, 130 for jersey retirement, minimum four-season team tenure
- **GM Career:** longitudinal franchise record for user-run careers when enabled
