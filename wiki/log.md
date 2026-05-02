---
title: Wiki Log
type: log
---

# Wiki Operations Log

Chronological record of all wiki operations.

---

## [2026-04-08] coach-archival + team-subtab-stitch-reskin

Two-phase refactor that deleted the legacy coach carousel/attribute subsystem and reskinned the four Team subtabs to the Stitch / Material 3 design system. Historical note: a lightweight HC/OC/DC system was reintroduced later and is now the active coaching model.

**Phase 1 — Coach archival (backend + frontend):**
- Deleted `src/engine/coachCarousel.ts`, `src/models/Coach.ts`, `web/src/views/CoachingView.tsx`, `web/src/views/team/CoachSpotlight.tsx`.
- Backend types: stripped `CoachingStaff`, `Team.coaches`, `League.unemployedCoaches`, `LeagueHistory.coachHistory`, `CoachSeasonRecord`, `Coach_of_Year` from `AwardType`, `coach_change` from `NewsType`. Renamed `CoachArchetype → TendencyArchetype` / `COACH_ARCHETYPES → TENDENCY_ARCHETYPES`.
- Engine consumers: `schemeBonus.ts` got a `+0.007 REBALANCE` constant; `progression.ageBands` got `+0.01/-0.005` across all 5 bands; `defensiveSelection.ts` swapped per-team coach intelligence for league-average `COACH_INTEL_FACTOR=0.65` / `COACH_INTEL_NOISE=0.05`; `simulateGame.ts` 4th-down + game-script aggressiveness now derive from `team.playcalling.aggressiveness`.
- Promoted `TUNING.coaching.fourthDown → TUNING.fourthDown`. Deleted the rest of `TUNING.coaching`, `TUNING.frontOffice.coaching`, and dead `TUNING.scheme` fields.
- Server: deleted `/fire-coach`, `/hire-coach`, `/promote-within` routes.
- TeamShell: collapsed sub-nav from 5 → 4 tabs (Overview / Depth Charts / Gameplans / Playbooks). Stripped `'coaching'` from `NavTab`, `inGmSection`, `SubNav inTeamSection`, and 4 sites in `App.tsx`.
- DB: one-time wipe migration in `src/db.ts` (`2026-04-07-coach-archival-wipe` sentinel) truncates `users`, `leagues`, `league_memberships`, `game_logs`, `game_results` on first server start. Destructive — restored backups must have the sentinel row inserted manually.
- Renamed `CoachingGrade → TeamGrade` and `SeasonCoachingReport → SeasonPerformanceReport` in `web/src/gameRecap.ts`.

**Phase 2 — Team subtab Stitch reskin (visual-only):**
- Extracted `<TeamBackdrop>` helper in `TeamShell.tsx`. All four Team subtabs now share the stadium backdrop.
- Reskinned `DepthChartView.tsx`, `GameplansPanel.tsx`, `PhilosophySlidersPanel.tsx`, `PlaybooksPanel.tsx`, and the four `playbooks/*.tsx` subcomponents (`CallSheetColumn`, `PlaybookListColumn`, `PlayInspectorColumn`, `MiniFormationField`) to Material 3 tokens, MaterialIcon, and the Space Grotesk / Manrope / Inter / JetBrains Mono typography stack.

**Wiki updates:**
- Deleted `entities/coaching-intelligence.md` (entire subsystem gone).
- Updated `index.md`, `overview.md`, `synthesis/system-status-matrix.md`, `synthesis/development-timeline.md` to drop coach refs and add the 2026-04-08 entry.

**Doc updates (canonical layer):**
- `CLAUDE.md`, `docs/FRANCHISE_SOURCE_OF_TRUTH.md`, `docs/ARCHITECTURE.md`, `docs/game-design.md`, `docs/NEXT_STEPS.md`, `docs/TUNING_LOG.md`, `docs/ENGINE_STATE.md`, `docs/DOCS_GUARDRAILS.md`, `PLAYBOOKS_AND_FORMATIONS.md`, `IMPLEMENTATION_LOG.md` — all stripped of coach refs and updated with the rebalance notes.

**Verification:** backend `tsc --noEmit` clean, frontend `npm run build` clean, forbidden-string grep sweep clean across all reskinned files. Bench script does not exist in this repo, so simulation drift will be measured against `ENGINE_STATE.md` baselines on the next manual sim cycle.

---

## [2026-04-07] stitch-redesign | DashboardView consolidation + UI direction

`DashboardView` rebuilt as the **canonical team page** for both the user's owned team and any other team. Made structural changes to the frontend nav and routing:

**Code changes:**
- `web/src/views/DashboardView.tsx` — refactored to take `teamId` (viewed) + `myTeamId` (ownership context). Hero stat row replaced the `Preview Next Game` button with two new cells: **Cap Free** (`$X.XM` with payroll subtitle) and **W/L Streak**. Off Rank and Def Rank now show PPG values beneath the rank. Up Next panel got two new buttons (**Watch Live**, **Simulate**) wired to `onWatchGame` / `onSimGame`. Recent Schedule sort flipped to oldest → newest left → right.
- `web/src/App.tsx` — new `dashboardTeamId` state + `handleSetTab()` wrapper that snaps the dashboard back to `myTeamId` when the user clicks the Dashboard nav button. New `handleSimGame()` calls `gameSim` API. `handleViewTeamDashboard(teamId)` sets `dashboardTeamId` then routes to the dashboard tab.
- `web/src/layout/TopNav.tsx` — removed `'team-dashboard'` from `NavTab`.
- **Deleted** `web/src/views/TeamDashboardView.tsx` — superseded by `DashboardView`.

**Wiki updates:**
- Created `entities/frontend-stitch-redesign.md` documenting the Stitch design system, the `DashboardView` template contract, and the per-page rebuild workflow.
- Updated `index.md` to catalog the new entity page (now 11 entities total).
- Updated `synthesis/system-status-matrix.md`: Frontend UI flipped from COMPLETE → ACTIVE (Stitch redesign in progress).
- Updated `synthesis/development-timeline.md` with the April 7 entry.
- Updated `synthesis/near-term-roadmap.md`: added Stitch redesign as the top current priority.
- Updated `overview.md` to mention the redesign.

**CLAUDE.md updates:**
- Corrected `TopNav` height (`h-14` → `h-20`).
- Replaced the navigation table with the actual `TopNav` button labels (Dashboard / Team / GM / Scouting / Game Day / League / Almanac / Draft) and removed the obsolete `team-dashboard` row.
- Added a Stitch UI Redesign section with the visual contract and per-page workflow.
- Updated the design system section to document both Stitch (canonical going forward) and the legacy Figma chrome.
- Added `MaterialIcon` and `InitialsAvatar` to the Key files list.

**Verification:** `cd web && npm run build` passes; `npm run lint` baseline 159 problems → still 159 (no new errors).


## [2026-04-06] playbooks-screen

Replaced the `PlaybooksPanel` placeholder with a real 3-column playbook editor under `web/src/views/team/playbooks/`:

- `PlaybookListColumn.tsx` — playbook cards, Playbook Fit meter, Down/Distance coverage bars, offense/defense toggle (amber Swords ↔ violet Shield).
- `CallSheetColumn.tsx` — formation-grouped call sheet with 5-dot call-rate strip, pass/run split bar, ADD PLAY / RESET CALLS actions (stubs).
- `PlayInspectorColumn.tsx` — selected-play metadata grid, mini formation field, strengths/weaknesses lists, call-rate slider + number input, Remove From Playbook.
- `MiniFormationField.tsx` — static SVG field with slot tokens + simple route/run overlay.
- `playbookFit.ts` — wraps `web/src/utils/playFit.ts` for the fit meter + down/distance coverage heuristics.
- `playStrengths.ts` — short user-facing strength/weakness phrases derived from engineType + conceptId (no tags field on plays).

API: Task 7 Path A — persistence uses existing `saveOffensePlaybook` / `saveDefensePlaybook` endpoints. The panel mutates the custom playbook in memory and re-saves the full object. Built-in playbooks are rendered read-only with a "Read-only (built-in)" badge. No backend changes.

Design tokens: dashboard card chrome (`bg-[#131b28]/80`, `bg-[#161f30]/90` headers, `border-slate-700/40 rounded-xl`), `#0b101a` body + orange/teal ambient glows, `#FF6B00` only as 1px ring + 6% wash on active playbook + selected play row, amber-400 / violet-400 accents for offense / defense.


## [2026-04-05] init | Wiki System Created
Initialized the LLM Wiki system for Football Sim.
- Created directory structure: `wiki/entities/`, `wiki/concepts/`, `wiki/sources/`, `wiki/synthesis/`
- Created `CLAUDE.md` schema with full rules, conventions, and workflows
- Created `wiki/index.md` master catalog
- Created `wiki/log.md` operations log

## [2026-04-05] ingest | Full Documentation Corpus (40+ sources)
Bulk ingest of all existing documentation: 10 main docs, 18 specs, 12 plans.

**Pages created (21 total):**

Entities (10):
- `entities/simulation-engine.md` — core engine architecture and frozen constants
- `entities/player-ratings.md` — 16 position rating systems
- `entities/playbook-system.md` — plays, formations, weighted selection
- `entities/playbook-fit-scoring.md` — play-to-roster matching system
- `entities/narrative-systems.md` — record chases, rivalries, arcs (LOCKED v1)
- `entities/almanac.md` — 9-tab historical reference
- `entities/hall-of-fame.md` — era-relative legacy scoring
- `entities/coaching-intelligence.md` — scouting, adjustments, scheme bonuses
- `entities/scouting-draft.md` — draft prospects, scouting, college layer
- `entities/multiplayer-gameday.md` — per-game lifecycle, spectator links

Concepts (5):
- `concepts/engine-lock.md` — simulation freeze philosophy
- `concepts/era-relative-scoring.md` — rank-based legacy fairness
- `concepts/vertical-slices.md` — complete features over partial systems
- `concepts/read-only-layers.md` — narrative/almanac separation from engine
- `concepts/document-ownership.md` — single canonical source per system

Sources (3):
- `sources/source-architecture.md` — ARCHITECTURE.md summary
- `sources/source-engine-state.md` — ENGINE_STATE.md summary
- `sources/source-game-design.md` — game-design.md summary

Synthesis (3):
- `synthesis/system-status-matrix.md` — lock status of all 14 systems
- `synthesis/development-timeline.md` — project history March-April 2026
- `synthesis/near-term-roadmap.md` — current priorities and future plans

**Also updated:**
- `wiki/overview.md` — full project synthesis with cross-references
- `wiki/index.md` — all 21 pages cataloged

## [2026-04-05] cleanup | Removed non-project material
Removed AI 2027 ingest pages (source-ai-2027.md, intelligence-explosion.md, neuralese.md, ai-alignment-challenge.md) — not relevant to Football Sim, NFL, or project scope. Wiki scoped to project-relevant content only.

## [2026-04-06] team-section-rebuild | Depth Charts + Roster + Gameplans + Spotlight
Frontend-only rebuild of the Team section. Backend untouched.

**DepthChartView (`web/src/views/DepthChartView.tsx`)**
- Adopted Dashboard color language: card chrome `bg-[#131b28]/80 border-slate-700/40`, header `bg-[#161f30]/90`, ambient navy body with subtle orange + teal blurred glows.
- Per-unit color tints: Offense → sky, Defense → violet, Special Teams → amber. Tints flow into the field token borders, formation field glow, position-card heading, starter row background, and unit toggle pill.
- Formation list now mirrors `src/models/Formation.ts` and `src/models/DefensivePackage.ts` exactly: Shotgun, Shotgun Empty, Singleback, I-Formation, Jumbo I (offense); 4-3 Base, 3-4 Base, Nickel, Dime, Quarter, Goal Line (defense). Personnel-grouping parens stripped from display.
- Formation selector relocated to the leftmost header position and wrapped in a tinted "hero" pill (unit-colored border, soft tint, glowing dot, custom chevron, large font) so it's the visual anchor of the screen.
- Position cards: bumped to `min-w-[200px] max-w-[260px]`, gap+padding increased.
- Rows now `flex flex-wrap justify-center` instead of a rigid `grid-template-columns: repeat(maxCols, 1fr)`, so QB/RB rows center under the OL row instead of being grid-pinned.
- **No-duplicate-starters guarantee:** each `PositionCard` owns a unique starter index inside its slot list (`allPlayers[dot.depth]`). WR1 → players[0], WR2 → players[1], WR3 → players[2]. Bench rows are shared below the starter zone. Drag-drop swaps absolute slot indices, so promoting a bench player into a starter slot demotes the player it replaces. The same player can no longer appear as the starter on two different cards in one formation.
- Slot mapping widened so I-Form/Jumbo I `FB` resolves through `RB`, 3-4 ILBs through `MLB`/`LB`, and S falls through `FS`/`SS`.

**RosterView (Overview tab) (`web/src/views/RosterView.tsx`)**
- **Sortable columns:** every column header is now click-to-sort. First click ascending, second flips to descending. Columns: Status, Player, Pos, OVR, Age, Salary, Bonus, Years.
- **Default sort = position ascending**, using a canonical position rank (QB → RB → WR → TE → OL → DL → LB → DB → K/P) — not alphabetical. Secondary sort within the same position is OVR-desc.
- Dropped the `#` index column. Replaced it with a **Status** column rendering a colored pill with a Lucide icon: Star/emerald for "Starter", HeartPulse/red for "Injured", CircleDot/slate for "Backup". Starter computation runs over the unfiltered roster so it stays stable regardless of position filter.
- Friendlier numerics: `money()` formatter (`$4.2M`, `$850K` with the unit as a smaller dimmer suffix), chunky OVR pill, bolder age/salary/years, contract-expiring (`years === 1`) shows a yellow chip. Starter avatars now get an emerald border ring.

**GameplansPanel (`web/src/views/team/GameplansPanel.tsx`)**
- Down-and-distance bucket labels switched from `text-slate-400 font-semibold` → `text-slate-100 font-bold` for readability.
- **Offense vs Defense color split:** offense uses amber (`text-amber-300 / bg-amber-400/15 / border-amber-400/50`) with a `Swords` icon, defense uses violet (`text-violet-300 / bg-violet-400/15 / border-violet-400/50`) with a `Shield` icon. Previously both were red-orange family and read as the same color. Save buttons inherit the section accent.

**PhilosophySlidersPanel (`web/src/views/team/PhilosophySlidersPanel.tsx`)**
- Same offense=amber+Swords / defense=violet+Shield treatment for cross-screen consistency.
- Slider value display is now an editable `<input type="number" min={0} max={100}>` clamped to 0–100. Users can either drag the slider or click the number to type a precise value.

**PlayerSpotlight (`web/src/views/team/PlayerSpotlight.tsx`)**
- Now receives `league` from `TeamShell`.
- New **Stats** card: position-aware columns
  - QB → CMP/ATT, YDS, TD, INT
  - RB/FB → CAR, YDS, TD, REC
  - WR/TE → REC, YDS, TD, TGT
  - Defense → TKL, SCK, INT
  - Top row = current-season totals aggregated from `league.currentSeason.games[*].boxScore.players[playerId]`, highlighted in the orange accent. Below it: last 2 historical seasons from `league.history.playerHistory[playerId]`.
- New **Game Log** card: per-game grid with `Wk | Opp | Res | <stat columns>`. Opp formatted as `vs DEN` / `@ LAR`. Res shows `W 24–17` / `L 13–28` colored emerald/red.
- Both new panels use the dashboard card chrome.

**TeamShell (`web/src/views/team/TeamShell.tsx`)**
- Main / right-rail split: 70/30 → 78/22 → **85/15**. The depth-chart screen and roster grid now have substantially more horizontal room.
- Wires `league` through to `PlayerSpotlight`.

**Documentation impact:** no engine, model, or schema changes. All work is presentation-layer.
