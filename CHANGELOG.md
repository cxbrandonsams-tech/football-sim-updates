# Changelog

All notable updates to Football Sim.

---

## 2026-04-05

### 10-Season Stress Test — Zero Bugs
Full end-to-end stress test simulating 10 complete seasons (regular season, playoffs, offseason, draft, season rollover). Results:
- 14/14 tests pass, 0 bugs, 0 warnings
- 10 champions crowned, 1,853 player histories, 90 Hall of Fame inductees
- 387 rivalry entries with 93 playoff meetings
- All narrative systems functional (record chases, milestones, arcs)
- Per-game ready-up + instant sim verified for CPU opponents

### Bug Fixes
- Regular season now auto-transitions to postseason after week 18 (no extra advance needed)
- Play-by-play log now visible during game replay (was only during live games)
- Camera zoom reduced ~35% for better field visibility
- Safety/MLB positioning fixed — no longer rush into backfield on zone drops
- CPU teams auto-ready when human team readies up (no manual ready-up needed for CPU opponents)
- Jersey number font size increased for readability
- Breakout arc detection tightened (was too aggressive, now requires 75% improvement + 500yd minimum volume)

### Multiplayer Game Day with Live Spectating
Per-game lifecycle: scheduled → ready → live → final

### Almanac — Complete Historical Reference Hub (9 Tabs)
New top-level "Almanac" nav item with comprehensive league history:

- **Awards** — year-by-year major awards (MVP, OPOY, DPOY, OROY, DROY, Coach of Year, Comeback Player) with All-Pro teams
- **All-Pro** — dedicated 1st/2nd team All-Pro viewer grouped by position, with year selector
- **Records** — career and single-season records for all major stat categories (career/single-season toggle)
- **Top 10 All-Time** — top 10 career leaders with stat group selector (Passing/Rushing/Receiving/Defense)
- **Season Leaders** — per-year stat leaders (top 5 per category) with year selector
- **Season Recaps** — composite year-by-year view: champion hero with team logos, runner-up, awards, stat leaders, full 32-team final standings
- **Past Champions** — championship history with dynasty tracker (title counts per team), year-by-year table
- **All-Time Standings** — franchise records with 6 sortable columns (Win%, W, Titles, PF, Diff, Playoffs)
- **Past Drafts** — round-by-round draft history by year, player names clickable, college listed

Backend: `draftHistory` field added to LeagueHistory (persisted at draft completion). Aggregation module `src/engine/almanac.ts` with pure functions for career/season leaders and franchise standings.

Frontend: Client-side aggregation in `web/src/utils/almanac.ts` for stat queries. 8 new view components.

### Narrative & Immersion Systems
Post-processing narrative layer that reads game results, stats, and history to generate richer storylines:

**Record Tracking:**
- Pace-based alerts after week 8 ("on pace to break the record")
- Near-record alerts after week 14 ("needs just X more to break the record")
- Record-broken events when all-time records fall
- Career record chase detection for veterans (3+ seasons)
- State-transition gating prevents spam (each alert fires once per player per stat per season)

**Extended Milestones:**
- Single-game milestones: 300/400/500 passing yards, 100/150/200 rushing/receiving yards, 4/5/6 TD passes, etc.
- Career tier milestones: 10K/20K/30K/40K/50K passing yards, 100/200/300 passing TDs, etc.
- Dedup against existing big-performance news to avoid double-reporting

**Rivalry System:**
- Division rivals always have a base rivalry
- Persistent rivalry heat accumulates from close games (+15), normal games (+5), upsets (+10 bonus), division games (+5 bonus), playoff meetings (+20)
- Pre-game rivalry previews for heated upcoming matchups
- Post-game "rivalry intensifies" for close rivalry games
- Heat decays 30% per offseason, entries pruned when below threshold

**Narrative Arcs:**
- Undefeated Watch: starts at 5-0, escalates at 8/10/12/14 wins, resolves on loss or perfect season
- Dynasty Run: detected from consecutive championships, tracks quest for 3-peat/4-peat
- Breakout Player: detected when production exceeds prior season by 50%+
- Revenge Game: previews for upcoming playoff rematches

**Frontend:** "Storylines" filter tab in news feed for all narrative news types.

All narrative systems are read-only — they never influence game simulation outcomes.

### Data Model Changes
- Added `draftHistory: DraftHistoryEntry[]` to LeagueHistory
- Added `rivalries: Record<string, RivalryHeat>` to League
- Added `narrativeArcs: NarrativeArc[]` to League
- Added `recordChaseState: Record<string, Record<string, boolean>>` to League
- Fixed `TeamSeasonHistory.championshipRound` on frontend to include all playoff rounds (wildcard, divisional, conference, championship, champion)
- Fixed `PlayerSeasonHistoryLine` on frontend to include missing fields (completions, attempts, carries, targets, sacksAllowed)

### Bug Fixes
- Fixed stale `'semifinal'` comparison in PlayoffView.tsx (should be `'conference'`/`'divisional'`/`'wildcard'`)

---

## 2026-04-03

### 2D Top-Down Game Visualization
- Replaced the broadcast-style field view with a full-field animated 2D top-down visualization
- All 22 players rendered as labeled circles (QB, WR, CB, FS, etc.) with team colors
- Receivers run realistic route shapes (go, post, corner, slant, curl, out, flat, seam)
- Defensive players track coverage patterns based on scheme (Cover 1/2/3/4, man, zone blitz)
- Ball tracks from QB to receiver on passes, follows RB on runs
- Visual effects: receiver glow based on coverage window, QB pressure indicator, TD/INT/sack flashes, breakaway speed trails, penalty flags
- Commentary syncs sentence-by-sentence to animation phases
- Speed control: 1x / 2x / 4x playback

### Verification & Cleanup Pass
- Found and fixed 24 orphaned CSS class references across 4 files
- All legacy CSS fully eliminated — zero non-Tailwind styling remaining

---

## 2026-04-02

### Complete Frontend Redesign (Figma Match)
- Full visual rewrite of all 34 frontend files to match Figma design system
- Deleted 7,277 lines of legacy CSS — zero legacy CSS remains
- Added framer-motion page transitions, lucide-react icons, self-hosted Inter + JetBrains Mono fonts
- New 3-column shell: league feed sidebar, main content, info rail with power rankings

### Dashboard Overhaul
- Team Overview with color-coded offense/defense rankings (green top 10, amber mid, red bottom 12)
- Team Leaders: 5 stat categories (Passing, Rushing, Receiving, Sacks, INTs)
- Weekly Recap: AI-generated headlines, standout performers, notable games with color-coded tags
- Playoff Race: top 10 with seed-colored numbers, division records, week-over-week comparison
- Recent Schedule: horizontal scroll with VS/@ indicators, opponent records, W/L scores
- Trade Block placeholder (coming soon)

### Power Rankings System
- Weighted formula: 30% Win Score, 20% Point Differential, 15% Strength of Schedule, 15% Recent Form, 10% Efficiency, 5% Quality Wins, 5% Injury Adjustment
- Top 5 displayed in right panel with movement arrows (up/down/unchanged)
- Automatically shows user's team if outside top 5

### Live Search
- Search bar in top nav searches all players (by name) and teams (by name or abbreviation)
- Results show player OVR, position, team, age
- Click to navigate to player detail or team roster

---

## 2026-03-30

### Frontend Architecture Rebuild
- Migrated from monolithic CSS to Tailwind CSS v4
- Implemented Figma-based design system with dark navy theme
- 7-category navigation with contextual sub-navs
- Dashboard grid matching Figma layout specifications

---

## 2026-03-29

### Play-by-Play Broadcast Experience
- 10-feature broadcast enhancement: drive summary strip, momentum bar, key play flash, red zone overlay, penalty display, OT drama, around-the-league alerts, score ticker, rivalry stats, highlights reel
- Two-layer commentary system with 400+ phrase fragments across 3 styles
- Progressive sentence-by-sentence commentary reveal with keyword highlighting

### Engine Tuning Pass
- Simulation stat calibration against real NFL ranges
- Red zone TD rate tuned to ~68-69% (NFL average)

---

## Earlier Development (2026-03)

### Core Systems Built
- Position-specific player ratings (10 position types with unique rating sets)
- 5-phase pass engine (Protection, Separation, Decision, Throw, Catch)
- 5-phase run engine (Blocking, Vision, Engagement, Contact, Breakaway)
- Penalty system with accept/decline AI logic
- Clock model with 15-min quarters, two-minute drill, timeouts
- Overtime (NFL modified sudden death rules)
- Special teams scoring (kick/punt return TDs, blocked kicks, safeties)
- Playbook system with custom plays, formations, down/distance buckets
- Tendencies / gameplan system with 7 sliders and 8 coach archetypes
- Draft with scouting system (points budget, tiered reports)
- Free agency with contract offers and player demands
- Trading system with AI evaluation
- Hall of Fame with era-relative legacy scoring
- Ring of Honor with team-specific loyalty bonuses
- GM career tracking
- Multi-user auth with JWT, league creation/joining
- SQLite persistence, Vercel + Fly.io deployment
