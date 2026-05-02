# Football Sim Project Overview

> **Last updated:** 2026-05-02
> **See also:** [index.md](index.md) | [game-design.md](game-design.md) | [system-architecture.md](system-architecture.md)

Football Sim is a browser-based football franchise simulation focused on full-season roster management, believable play resolution, and multiplayer league operations. The current product is a TypeScript monorepo with a React frontend on Vercel and an Express + SQLite backend on Fly.io.

## Product Shape

The game loop is:

```text
Regular Season (18 weeks)
  -> Postseason
  -> Offseason Week 1 (awards, retirements, Hall of Fame / Ring of Honor, contract decisions, coach changes)
  -> Offseason Week 2 (coach market, free agency wave 1)
  -> Draft
  -> Offseason Week 3 (next class generation, free agency wave 2)
  -> Offseason Week 4 (Training Camp progression)
  -> New Season
```

Each league has 32 teams, 16 on-field positions, 56-man rosters, a 45-player minimum, a $255M salary cap, persistent league history, and commissioner-controlled multiplayer operations.

## Current Feature Surface

- **Command Center and team dashboard:** schedule, action items, cap outlook, standings context, trade activity, watch list, and weekly recap surfaces.
- **Team management:** roster overview, depth charts, weekly gameplans, playbooks, trades, free agents, contract negotiation, practice squad actions, and Training Camp.
- **Scouting and draft:** Scouting HQ, prospect cards, confidence-based fog of war, draft board, watch list, scout directives, auto-draft helpers, and seven draft rounds.
- **Game Day:** scheduled kickoffs, ready-up flow, live and quick simulation, match visualization, box scores, spectator links, and archived replays.
- **League views:** standings, rankings, stats, news, weekly recaps, playoffs/offseason flow, awards, and team owners.
- **Almanac:** Hall of Fame, Ring of Honor, records, season recaps, head-to-head history, replay archive, and GM career history when enabled.
- **Commissioner tools:** invites, approval-gated joins, seat transfers, commissioner transfer, readiness ops, announcements, manual edits, recovery actions, and commissioner logs.

## Core Gameplay Systems

- **Simulation engine:** rating-driven pass and run pipelines with locked tuning targets and era-stable scoring expectations.
- **Scouting:** four-stage confidence pipeline that narrows OVR ranges and reveals more specific intel over time.
- **Coaching:** five archetypes, coordinator promotion/poaching, offseason hiring market, and d20 Training Camp progression support.
- **Contracts:** salary, years, and signing-bonus negotiation with dead cap, fifth-year options, and interest thresholds.
- **Narrative:** rivalry heat, milestones, record chases, prose-generated news, and optional premium radio episodes.
- **Legacy:** Hall of Fame induction at 175 legacy points after a three-season waiting period; Ring of Honor induction at 85 team-legacy points with jersey retirement at 130.

## Technical Model

- **Frontend:** React 19, Vite 8, Tailwind CSS v4, Framer Motion.
- **Backend:** Express 5, better-sqlite3, JWT auth, SSE for live game and highlight streams.
- **Persistence:** one JSON blob per league plus supporting tables for users, memberships, logs, results, notifications, and radio episodes.
- **Deployment:** Vercel for the SPA, Fly.io for the stateful API.

## Status

The current codebase ships the full core loop: simulation, scouting, coaching, contracts, multiplayer operations, notifications, replay preservation, commissioner administration, and the Primetime/Stitch frontend pass. The remaining work is now mostly iterative product polish, balancing, and additional content rather than missing platform foundations.
