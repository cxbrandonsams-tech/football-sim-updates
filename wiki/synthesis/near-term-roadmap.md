---
title: Near-Term Roadmap
type: synthesis
created: 2026-04-05
updated: 2026-04-25
sources: [CLAUDE.md, project memory, shelved items list]
tags: [roadmap, priorities]
---

> **Updated 2026-04-25.** See `CLAUDE.md` for the canonical current project state.

# Near-Term Roadmap

Current priorities, medium-term goals, and long-term vision for the football simulation project.

## Current Priorities

### Stitch UI Redesign — COMPLETE
All views rebuilt on Stitch + Material 3 / Primetime design system as of 2026-04-13. The full rollout covered:

- **Dashboard** — `DashboardView` (canonical team page) [2026-04-07]
- **Team** — Overview, Depth Charts, Gameplans, Playbooks, Trades, Free Agents, Training Camp [2026-04-07 to 2026-04-10]
- **League** — Standings, Rankings, Stats, News, Awards, Commissioner [2026-04-10 to 2026-04-12]
- **Almanac** — Awards, Records, Recaps, Head-to-Head, Draft History, Replays, HOF/ROH/GM history [2026-04-11 to 2026-04-24]
- **Scouting** — College, Prospects, Scouting HQ, Watch List, Draft Board (4-stage confidence system) [2026-04-12 to 2026-04-13]
- **Global chrome** — TopNav, SubNav, Sidebar, RightPanel [2026-04-10]

The Primetime visual identity (monochrome + 6 accent tokens) is deployed globally via `tailwind.css`. `lucide-react` has zero imports remaining.

### Game Day View
The only remaining view not yet fully rebuilt on Stitch. Currently functional on the legacy design.

### Multiplayer Operations Spine — COMPLETE
Async advance, readiness pre-flight, live kickoff scheduling, persistent notifications, replay archive, Commissioner League Ops, smoke coverage, and CPU roster floor repair shipped on 2026-04-24.

### Long-Save Balance Gates — COMPLETE
Coordinator retention/promotion, multi-seed coaching balance checks, league-health assertions, 10-season stress hard-fail gates, and GitHub Actions deploy gating shipped on 2026-04-25.

### Coaching Balance Visibility
Next useful gameplay tooling: surface HC/OC/DC balance deltas in-game/admin UI so archetype and star-tier balance can be reviewed without reading CLI output.

## Medium-Term

### Enhanced 2D Visualization
Further polish on the matchviz system: additional route types, special teams plays, improved animation smoothness, instant replay capability.

### Multiplayer Enhancements
Expand multiplayer beyond the operations spine. Remaining areas: league-wide multiplayer draft, human-to-human trade negotiation polish, and deeper spectator/live-play flows.

### Mobile Responsive
The 3-column shell (`grid-cols-[17rem_1fr_17rem]`) hides sidebar at `md` and right rail at `xl`, but core views need responsive attention for smaller screens.

## Long-Term

### Advanced AI
Smarter CPU team management: draft strategy, free agency bidding, trade evaluation, gameplan adaptation based on opponent tendencies.

### Player Archetypes
Distinct player archetype profiles that influence development curves, peak windows, and decline patterns beyond raw ratings.

### Contract Depth
Restructuring, franchise tags, dead cap, salary floor, luxury tax — deeper financial simulation.

## Deferred (Not Planned)

These items are explicitly deferred and should not be implemented unless specifically requested:

- **Motion/audibles** — Pre-snap adjustments and hot routes
- **Full college simulation** — Complete college football pipeline feeding the draft
- **Holdouts** — Contract dispute mechanics
- **Legacy gameplans** — `GameplanSettings`/`PlaycallingWeights` replaced by tendencies/archetype system
- **AI autonomous trade proposals from trade block** — interest scoring only
- **FAAB waiver bidding** — priority is reverse-standings → rolling, no budget

## See Also

- [[system-status-matrix]]
- [[development-timeline]]
- [[vertical-slices]]
