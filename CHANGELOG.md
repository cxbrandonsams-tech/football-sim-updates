# Changelog

All notable updates to Football Sim.

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
