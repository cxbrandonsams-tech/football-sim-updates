# Changelog

All notable updates to Football Sim.

---

## 2026-04-13

### Team + GM Navigation Merge
Merged the Team and GM top-level sections into a single unified "Team" section. The top nav now has 7 items instead of 8.

- **Roster dual-lens toggle** — switch between Performance view (Status, OVR, Age, Dev Trait) and Contracts view (Salary, Bonus, Years, Demands, Extend/Cut actions) without leaving the page
- **Cap summary strip** — payroll bar, cap space, expiring count, and demand count render inline above the contracts table
- **Contract filter chips** — All / Demands / Expiring quick filters with position-group collapsible rows
- **Trades and Free Agents** are now Team sub-tabs with a visual separator dividing on-field tabs (Overview, Depth Charts, Gameplans, Playbooks) from front-office tabs (Trades, Free Agents)
- **Free Agent starter comparison** — when browsing free agents, a subtle chip shows your current starter at that position if the FA is better (e.g., "Your WR1: Mike Evans (79 OVR)")
- Deleted `TeamOverviewView` and `ContractsView` (absorbed into existing views)

### Hall of Fame & Ring of Honor Recalibration
- HOF induction threshold raised from 150 to 175
- 3-season waiting period after retirement before HOF eligibility
- Max 7 inductees per year to prevent class inflation
- ROH induction threshold raised from 55 to 85, jersey retirement from 100 to 130
- 4-season minimum team tenure required for ROH
- Reduced seasonal rank points to slow ROH accumulation
- Legacy score computation now uses config constants instead of hardcoded values

---

## 2026-04-12

### Primetime Design System
Complete visual identity overhaul replacing the previous teal/orange FM-inspired palette:

- **Monochrome base** with silver primary and pure neutral surfaces
- **6 accent tokens**: neon (#2bff5e), cyan (#00d4ff), steel (#5b8fcc), gold (#d4a017), earth (#8B6914), football (#8B4513)
- **Offense = gold, Defense = cyan** accent convention across all Team views
- **Typography**: Outfit for headlines, DM Sans for body/labels, JetBrains Mono for stats
- **Glass panels**: `bg-black/60 backdrop-blur-md` with card depth system (top-border highlights, gradient hover reveals, layered shadows)
- **Page entrance choreography**: staggered CSS animations (`pt-enter`) for all views
- Auth screens retain original Primetime gold/fire/cyan orbs

### Prose Engine — Professional Sports Writing
Replaced template-based news generation with a data-driven prose engine:

- Categorized vocabulary banks (verbs, adjectives, metaphors) across 11 category files
- Article templates for all 23 news types with opener/closer/transition banks
- Context tagging system for situation-aware word selection
- Variety tracker prevents repetitive phrasing across articles
- Professional sports writing quality with natural-sounding game recaps, trade reports, and milestone announcements

### The Brandon Sams Show (Premium Radio Feature)
AI-generated sports radio show with full audio production:

- **Script assembler** builds `RadioScript` from league state with 15 segment types scored by relevance
- **5 speaker roles** with distinct OpenAI TTS voices: host, analyst, and 3 caller personas (Mad Mike, Big Shirley, Stats Steve)
- **6 in-season triggers** (week 1, mid-season, late-season, wildcard, championship) + 3 offseason triggers (FA recap, draft preview, draft recap)
- **Audio pipeline**: OpenAI TTS generation → ffmpeg stitching → Cloudflare R2 storage
- **RadioSidebar UI**: custom audio player with auto-scrolling transcript, past episode list, generating/pending/failed states
- Replaces the standard League Feed sidebar when premium is enabled

### Almanac Expansion (13 Tabs)
- Added **Ring of Honor** and **GM Career** tabs (moved from League/GM sections)
- Added **History** and **Hall of Fame** (moved from League section)
- All Almanac pages converted to full-bleed glass + backdrop layout with transparent section wrappers
- Total: Awards, All-Pro, Hall of Fame, Ring of Honor, Records, Top 10 All-Time, Season Leaders, Season Recaps, History, Past Champions, All-Time Standings, Past Drafts, GM Career

### League Section Restructure
- **New Rankings page** — 3-panel layout: featured team card + tiered table (Elite/Contender/Fringe/Rebuilding) with ELO ratings
- **ELO rating system** — margin-of-victory adjusted, home advantage, persists across seasons
- **Team Stats** — Offensive, Defensive, and Efficiency sub-tabs with sortable ranking tables
- **8 new defensive/efficiency stats**: totalPlays, thirdDownConv, thirdDownAtt, redZoneTDs, redZoneTrips, sacks, interceptions, fumblesRecovered
- **News redesign** — "The Gridiron Chronicle" newspaper layout with All/My Team tabs and 3-column article grid
- Narrative tab removed; active storylines and rivalry watch merged into News as pinned sections
- History and Hall of Fame moved to Almanac
- "Leaders" sub-tab renamed to "Stats"

### Standings Redesign
- OOTP-style 4-column layout: IC/SC conference leaders flanking division tables
- Full-bleed layout with stadium backdrop
- Color-coded front-office personality badges
- Team mentalities simplified to 3 labels: Win-Now / Balanced / Rebuilding

---

## 2026-04-11

### SVG Player Portraits
- Procedurally generated player faces using an 11-layer SVG composite system
- Seeded RNG (FNV-1a + Mulberry32) ensures deterministic appearance from player name
- 10 numeric appearance indices controlling face shape, skin tone, hair, eyes, nose, mouth, facial hair, accessories
- Portraits appear across Dashboard, Team, Scouting, Almanac, Hall of Fame, and player profiles
- `PlayerAvatar` wrapper component with `InitialsAvatar` fallback for missing portraits

### Confidence-Based Scouting System (4 Stages)
Complete overhaul replacing the old point-based L1/L2/L3 scouting:

1. **School Scouting** (Offseason → Week 1): binary Powerhouse/Dark Horse choice, drips weeks 1–10
2. **Position Scouting** (Weeks 1–10 → Week 11): 10-position % allocation, drips weeks 11–18
3. **Targeted Scouting** (Weeks 11–18 → Wild Card): pick 5 schools, drips WC → Championship
4. **Interviews** (Playoffs → Offseason): pick 10 prospects, immediate delivery, only way to reveal devTrait + characterFlags

- Confidence 0–100% drives OVR range width (54 → 2), strengths/weaknesses count, potential tier accuracy
- Diminishing returns formula: `effectiveGain = rawGain * (1 - current * 0.3)`
- Pre-rolled 18-week college season with 50 schools, 5 conferences, stat leaderboards
- Full Stitch UI: ScoutingShell with College, Prospects, Scouting HQ, and Draft Board views

---

## 2026-04-08

### Coach System Archived
Entire coaching subsystem removed from backend and frontend:
- All coach types, models, engine consumers, 3 server endpoints, Coach of Year award, coach_change news type, COACH_ARCHETYPES, and the Coaches subtab deleted
- Simulation rebalanced with `+0.007` in schemeBonus and adjusted progression age bands
- One-time DB wipe migration for clean slate

### Stitch Design System — Team Section
- Team subtabs (Overview, Depth Charts, Gameplans, Playbooks) reskinned to Stitch
- Shared `<TeamBackdrop>` stadium image across all Team subtabs
- Stitch component kit: StitchCard, StitchSection, StitchTabBar, StitchTable, StitchChipRail, StitchStatCell, StitchBadge, StitchHeroStat

### Depth Chart Redesign
Two-tab layout:
- **Overview**: 10-column responsive grid with all position groups, drag-to-reorder, Sort All by OVR
- **Formations**: unit toggle + formation selector, SVG field visualization, per-slot PositionCards with drag reorder

### Playbook Editor
- 3-column layout: Playbook List / Call Sheet / Play Inspector
- Offense/Defense side toggle with accent theming (gold/cyan)
- Clone-first playbook creation (required source), delete custom playbooks
- Debounce save with status indicators

### Waiver Wire & Trade Block
- **Waivers**: in-season cuts → 1-week waivers, reverse-standings priority before week 10 then rolling, AI claims + resolution
- **Trade Block**: lightweight player shopping with interest scoring, no autonomous AI offers

### Team Logo Optimization
- All 32 team logos re-exported as 256x256 square PNGs with transparent backgrounds

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
- Regular season now auto-transitions to postseason after week 18
- Play-by-play log now visible during game replay
- Camera zoom reduced ~35% for better field visibility
- Safety/MLB positioning fixed for zone drops
- CPU teams auto-ready when human team readies up
- Jersey number font size increased for readability
- Breakout arc detection tightened (75% improvement + 500yd minimum)

### Multiplayer Game Day with Live Spectating
Per-game lifecycle: scheduled → ready → live → final

### Almanac — Complete Historical Reference Hub (9 Tabs)
Awards, All-Pro, Records, Top 10 All-Time, Season Leaders, Season Recaps, Past Champions, All-Time Standings, Past Drafts.

### Narrative & Immersion Systems
Record-chase detection, extended milestones, rivalry system, narrative arcs (undefeated watch, dynasty, breakout, revenge). Surfaces through the news feed.

---

## 2026-04-03

### 2D Top-Down Game Visualization
- All 22 players rendered as labeled circles with team colors
- Receivers run realistic route shapes (go, post, corner, slant, curl, out, flat, seam)
- Defensive players track coverage patterns based on scheme
- Ball tracks from QB to receiver on passes, follows RB on runs
- Visual effects: coverage window glow, QB pressure, TD/INT/sack flashes, breakaway trails
- Commentary syncs sentence-by-sentence to animation phases
- Speed control: 1x / 2x / 4x playback

---

## 2026-04-02

### Complete Frontend Redesign
- Full visual rewrite of all 34 frontend files to match Figma design system
- 3-column shell: league feed sidebar, main content, info rail with power rankings
- New dashboard with team overview, playoff race, team leaders, weekly recap, recent schedule
- Power Rankings with weighted formula (wins, point diff, SOS, recent form, efficiency, quality wins, injury adjustment)
- Live search across all players and teams

---

## 2026-03-30 and Earlier

### Core Systems
- Position-specific player ratings (16 positions with unique rating sets)
- 5-phase pass engine (Protection, Separation, Decision, Throw, Catch)
- 5-phase run engine (Blocking, Vision, Engagement, Contact, Breakaway)
- Penalty system, clock model, overtime, special teams scoring
- Playbook system with custom plays, formations, tendencies/archetypes
- Draft, scouting, free agency, contracts, trading
- Hall of Fame, Ring of Honor, GM career tracking
- Multi-user auth with JWT, league creation/joining
- SQLite persistence, Vercel + Fly.io deployment
