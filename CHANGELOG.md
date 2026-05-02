# Changelog

All notable updates to Football Sim.

---

## 2026-05-02

### Documentation Sync

- Refreshed the public wiki to match the live project surface, including simulation, scouting, season lifecycle, player ratings, playbooks, gameplans, contracts, coaching, waivers, narrative systems, Almanac, Hall of Fame, and multiplayer game day.
- Updated the top-level README, feature summary, and home page so player-facing guides are easy to find.
- Replaced stale Almanac and simulation summaries with current mechanics language, including the 6-phase pass engine and the week-by-week offseason loop.

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
