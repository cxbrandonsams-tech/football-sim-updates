---
title: Development Timeline
type: synthesis
created: 2026-04-05
updated: 2026-04-25
sources: [git history, project memory, CLAUDE.md]
tags: [timeline, history, deprecated]
---

> **Deprecated:** This timeline was originally frozen on April 8, 2026. Short April 24-25 addenda have been appended for major implementation pushes; see git history and newer specs for the full record.

# Development Timeline

Chronological history of the football simulation project from inception through current state.

## Early March 2026 — Core Systems

Foundation work: league structure, team/player models, position-specific ratings, draft system, free agency, contracts, depth charts, and the initial simulation pipeline (`simulateWeek` / `simulateGame`). Express API with SQLite persistence. JWT authentication.

## March 27, 2026 — Engine Lock

Simulation engine validated against 1,000+ games. All tuning constants in `config.ts` frozen. [[engine-lock]] policy established. LOCKED_VALUES and ENGINE_STATE documents created. From this point forward, simulation changes are additive only.

## March 29, 2026 — Play-by-Play and Tuning

Play-by-play event system (`PlayEvent[]`) added to game simulation. Pass engine and run engine produce granular event logs. Final tuning pass on scoring rates, turnover frequencies, and penalty distributions. Engine metrics documented in ENGINE_STATE.

## March 30, 2026 — Frontend Architecture

React 19 + Vite 8 + Tailwind CSS v4 stack established. 3-column shell layout (sidebar, main content, right panel). Navigation system with 8 top-level items and contextual sub-tabs. Design system tokens defined. API client with typed REST wrappers.

## April 2, 2026 — Figma Rewrite

Complete frontend rewrite from Figma design system. Card patterns, color palette (`#0b101a` app background, `#FF6B00` accent), typography (Inter Variable + JetBrains Mono). All legacy CSS removed. 24 view files rebuilt to match Figma source of truth.

## April 3, 2026 — 2D Visualization and Team Dashboard

Match visualization system (`matchviz/`) built as a [[vertical-slices|vertical slice]]: coordinate system, formations, route rendering, defensive paths, ball physics, animation loop, and playback controls. Team dashboard with team-color theming. Hall of Fame and Ring of Honor with [[era-relative-scoring]].

## April 5, 2026 — Feature Expansion

Multiple systems shipped:
- **Almanac** — All 9 tabs (Records, Franchise, Seasons, Players, Games, Awards, Head-to-Head, Superlatives, Draft History) as a complete [[vertical-slices|vertical slice]]
- **Narrative systems** — Records tracking, rivalry detection, dynasty/drought arcs, narrative news generation
- **Multiplayer game day** — Active development began
- **Playbook fit scoring** — Active development began
- **10-season stress test** — Full validation run confirming engine stability across extended franchise play
- **Defensive spacing fixes** — Anti-stacking deconfliction, tackle ring convergence, zone drop lateral preservation in 2D visualization

## April 6, 2026 — Team Section Rebuild + Playbooks Editor

Frontend-only rebuild of the Team section. `TeamShell` orchestrates Overview / Depth Charts / Coaches / Gameplans / Playbooks with an 85/15 main + spotlight split. `DepthChartView` mirrors the canonical formation list and enforces no-duplicate-starters per slot. `RosterView` got sortable columns + Status pills. `GameplansPanel` and `PhilosophySlidersPanel` adopted the offense=amber+Swords / defense=violet+Shield split. `PlaybooksPanel` shipped as a real 3-column editor (Playbook List / Call Sheet / Play Inspector) backed by the existing `saveOffensePlaybook` / `saveDefensePlaybook` endpoints. The Coaches subtab was deleted on Apr 8 in the coach archival cutover.

## April 7, 2026 — Stitch UI Redesign Begins

`DashboardView` rebuilt as the **canonical team page** for any team using Google Stitch + Material 3. The deleted `TeamDashboardView.tsx` and the `team-dashboard` tab are gone — `DashboardView` covers both the user's owned team and any other team selected via search / standings / news / etc. `App.tsx` got a `dashboardTeamId` state + a `handleSetTab()` wrapper that snaps the dashboard back to `myTeamId` when the user clicks the Dashboard nav button. Hero stat row replaced the Preview Next Game button with **Cap Free** + **W/L Streak**, and the Up Next panel got **Watch Live** + **Simulate** buttons wired to `gameSim`. From this point forward, every other view will be re-stitched one at a time using `DashboardView` as the template. See [[frontend-stitch-redesign]].

## April 8, 2026 — Coach Archival + Team Subtab Stitch Reskin

Two-phase refactor.

**Phase 1** deleted the legacy coach carousel/attribute subsystem from backend + frontend. `Coach.ts`, `coachCarousel.ts`, `CoachingView.tsx`, `CoachSpotlight.tsx` were deleted at that time. `Team.coaches`, `League.unemployedCoaches`, `coachHistory`, `Coach_of_Year`, `coach_change` news, `COACH_ARCHETYPES` (renamed `TENDENCY_ARCHETYPES`), `OffensiveScheme`/`DefensiveScheme` types, the old fire/hire/promote routes, and old engine consumers (scheme alignment bonus, coach traits in progression, contract negotiator FA discount, talent_evaluator scouting bonus, HC personality 4th-down decisions, coach intelligence in defensiveSelection) were stripped. Two pre-strip contributions worth preserving were absorbed into the player layer as flat constants: `+0.007 REBALANCE` in `schemeBonus.ts` and `+0.01/-0.005` across `progression.ageBands`. The Coaches Team subtab was deleted, collapsing the sub-nav from 5 → 4 tabs (Overview / Depth Charts / Gameplans / Playbooks). A one-time DB wipe migration in `src/db.ts` truncates user data on first server start after the deploy lands. Historical note: a new lightweight HC/OC/DC system was later reintroduced and is now active.

**Phase 2** reskinned the four Team subtabs (Depth Charts, Gameplans, Playbooks + the Stitch-already Overview) to the Material 3 / Stitch design system. Extracted a shared `<TeamBackdrop>` helper. Token swap (slate/orange/emerald → surface-container-* / primary / secondary / tertiary), font swap (Inter / JetBrains Mono → Space Grotesk / Manrope / Inter / JetBrains Mono), icon swap (Lucide → MaterialIcon). Visual-only — zero behavior changes.

The Stitch reskin rollout continues into League / Almanac / GM / Scouting / Game Day next.

## April 24, 2026 — Multiplayer League Operations Spine

Implemented the first end-to-end multiplayer operations layer:

- **Async advancement** — commissioner advance can run as a background job with progress polling.
- **Readiness pre-flight** — league-level blockers and warnings for cap, roster, ready-up, draft, coach, contracts, and training camp state.
- **Live game scheduling** — owners or commissioner can schedule/clear kickoff times for unplayed games.
- **Scheduled-games visibility** — dashboard/sidebar widgets show upcoming live kickoffs and human matchups.
- **Persistent key replays** — rollover now preserves playoff games, human-vs-human games, major upsets, and record/newsworthy games instead of purging all logs.
- **Replay Archive** — Almanac Replays tab plus standalone `/replay/:leagueId/:gameId` playback route.
- **Notifications** — persistent per-user league notifications for kickoff changes, advance events, readiness nudges, commissioner overrides, and archived replay moments.
- **Commissioner League Ops** — new commissioner tab for readiness blockers, owner nudges, force-ready, auto-sim, and kickoff clearing with activity/log trails.
- **Multiplayer smoke coverage** — added a real HTTP smoke test covering two-owner scheduling, notifications, readiness blockers, nudges, force-ready, force-sim, and async advance.
- **Test stabilization** — fixed ready-up ownership hydration for game snapshots and moved the long-season stress harness to an isolated in-process app. Default stress coverage is now 3 seasons in `npm test`; the dedicated `validate10` script remains the 10-season engine validation path.
- **CPU roster floor repair** — added replacement-level CPU-only roster repair after cap cuts and before season rollover scheduling, eliminating multi-season roster-collapse warnings while keeping human-owned teams responsible for their own roster blockers.

## April 25, 2026 — Long-Save Stability and Balance Gates

Closed the loop on the coaching and long-save validation pass:

- **Coordinator retention/promotion** — firing a HC now leaves OC/DC in place; an existing coordinator can be promoted to HC and receives a generated replacement in the vacated coordinator role.
- **Free-agent depth pool** — new leagues start with below-average FA filler so long saves do not exhaust depth players.
- **Receiving TD distribution** — red-zone target selection now dampens same-game receiving TD concentration.
- **Stress gate hardening** — the 3-season default / 10-season `FULL_STRESS=1` harness now fails on any bug, warning, stat anomaly, or UX issue.
- **Seeded balance CI** — `npm run balance:ci` runs 2 seasons across 3 fixed seeds and asserts coach balance plus league health (FA pool, roster range, team count, final phase/year, missing HC/OC/DC).
- **Deploy gate** — GitHub Actions now runs build + seeded balance CI before Fly deploy.

## See Also

- [[system-status-matrix]]
- [[near-term-roadmap]]
- [[engine-lock]]
