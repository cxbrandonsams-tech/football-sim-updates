# Features

A complete breakdown of everything in Football Sim.

---

## Franchise Management

| Feature | Details |
|---------|---------|
| **Roster Management** | 53-man rosters across 16 position types. Cut, sign, and extend players. Dual-lens roster view shows performance data or contract details with one toggle. |
| **Salary Cap** | $420M cap with payroll tracking, cap space visualization, expiring contract alerts, and contract demand badges. Inline Extend/Cut actions right from the roster. |
| **Trading** | Propose trades with players and draft picks. AI evaluates trade value using OVR, age curves, contract control, and salary efficiency. Pending trade notifications with accept/reject. |
| **Free Agency** | Browse available players with position filters. Starter comparison chips show when a free agent beats your current player. Offer salary and years. |
| **Waiver Wire** | Recently released players hit waivers for 1 week. Priority is reverse-standings before week 10, then rolling. AI teams make claims too. |
| **Trade Block** | List players as available. AI teams express interest based on roster needs. Interest scoring drives visibility, but no autonomous AI offers. |
| **Depth Chart** | Drag-to-reorder across all position groups. Formation visualization shows starter assignments on an SVG field diagram. |

## Playbook System

| Feature | Details |
|---------|---------|
| **Custom Playbooks** | Create offensive and defensive playbooks by cloning from built-in templates. Add/remove plays, adjust weights per down/distance. |
| **13 Down/Distance Buckets** | Fine-grained play-calling control: 1st & 10, 2nd & Long, 3rd & Short, 4th & Goal, etc. |
| **Tendencies & Archetypes** | 7 philosophy sliders (run/pass balance, aggression, tempo, etc.) shape your team's identity. 8 archetype presets to start from. |
| **Formation Depth Charts** | Assign starters per formation slot. Visual field diagram shows player positions. |

## Game Simulation

| Feature | Details |
|---------|---------|
| **5-Phase Pass Engine** | Protection &rarr; Separation &rarr; Decision &rarr; Throw &rarr; Catch. Every rating matters: OL blocking vs. DL rush, WR route running vs. CB coverage, QB accuracy vs. coverage window. |
| **5-Phase Run Engine** | Blocking &rarr; Vision &rarr; Engagement &rarr; Contact (Power OR Elusiveness, not blended) &rarr; Breakaway (Speed triggers in open field only). |
| **Penalties** | Holding, pass interference, false start, offsides, and more. AI accept/decline logic. |
| **Clock Management** | 15-minute quarters, two-minute drill, timeout management, running vs. stopped clock. |
| **Overtime** | NFL modified sudden-death rules. |
| **Special Teams** | Kick/punt return TDs, blocked kicks, safeties, field goals with distance-based accuracy. |

## 2D Match Visualization

| Feature | Details |
|---------|---------|
| **All 22 Players** | Labeled circles with jersey numbers and team colors on a full-field top-down view. |
| **Route Running** | 9 receiver route shapes: go, slant, curl, out, in, post, corner, flat, seam. |
| **Coverage Patterns** | DL rush lanes, LB zone/blitz, CB man coverage, safety zone drops. |
| **Ball Tracking** | Pass arcs from QB to receiver, handoff paths on runs, kick arcs. |
| **Visual Effects** | Coverage window glow, QB pressure indicator, TD/INT/sack flashes, breakaway speed trails. |
| **Commentary Sync** | 400+ phrase fragments sync sentence-by-sentence to animation phases. 3 styles: neutral, hype, analytical. |
| **Speed Control** | 1x / 2x / 4x playback. |

## Scouting & Draft

| Feature | Details |
|---------|---------|
| **4-Stage Scouting Pipeline** | School Scouting &rarr; Position Scouting &rarr; Targeted Scouting &rarr; Interviews. Each stage has deadlines and accumulates confidence 0-100%. |
| **18-Week College Season** | 50 schools across 5 conferences. Pre-rolled season with standings, stat leaders, weekly headlines, and Top 25 rankings. |
| **Confidence System** | Higher confidence = tighter OVR range, more strengths/weaknesses revealed, better potential tier accuracy. Diminishing returns prevent over-scouting. |
| **Interviews** | Pick 10 prospects to interview during playoffs. Only way to reveal development trait and character flags. |
| **Draft Board** | Rank prospects, browse by position, view team needs. Confidence % and OVR range replace old scout levels. |
| **Draft Room** | Multi-round draft with pick-by-pick resolution. Sim remaining picks, advance to your pick, or auto-draft. |

## Season & History

| Feature | Details |
|---------|---------|
| **Full Season Lifecycle** | Regular season (18 weeks) &rarr; Playoffs &rarr; Offseason &rarr; Draft &rarr; repeat. |
| **Progression/Regression** | Players improve or decline based on age, development trait, and performance. |
| **Hall of Fame** | Era-relative legacy scoring. 175-point threshold, 3-season waiting period, max 7 inductees per year. |
| **Ring of Honor** | Per-franchise honors. 85-point threshold with 4-season minimum tenure. Jersey retirement at 130 points. |
| **GM Career** | Track your wins, championships, draft hits, and career arc across seasons. |
| **13-Tab Almanac** | Awards, All-Pro, Hall of Fame, Ring of Honor, Records, Top 10 All-Time, Season Leaders, Season Recaps, History, Past Champions, All-Time Standings, Past Drafts, GM Career. |

## Narrative & Immersion

| Feature | Details |
|---------|---------|
| **Record Chasing** | Pace alerts at week 8, near-record alerts at week 14, record-broken events when all-time marks fall. Career record chase detection for veterans. |
| **Rivalry System** | Division rivals always have a base rivalry. Heat accumulates from close games, upsets, division games, and playoff meetings. Decays 30% per offseason. Pre/post-game rivalry news. |
| **Story Arcs** | Undefeated Watch (5-0 start, escalates through the season), Dynasty Run (consecutive championships), Breakout Player (50%+ production jump), Revenge Game (playoff rematch previews). |
| **Milestones** | Single-game (300/400/500 passing yards, 100/200 rushing, etc.) and career tier milestones (10K/20K/30K passing yards, 100/200/300 TDs, etc.). |
| **Prose Engine** | Data-driven sports writing with categorized vocabulary banks, context tagging, and variety tracking. Professional-quality game recaps, trade reports, and milestone announcements. |
| **The Brandon Sams Show** | AI-generated sports radio with 5 distinct voice characters (host, analyst, 3 callers). Auto-triggers at key season moments. Full audio with transcript. |

## ELO & Power Rankings

| Feature | Details |
|---------|---------|
| **ELO Ratings** | Margin-of-victory adjusted, home advantage, persists across seasons. Visible on the Rankings page. |
| **Power Rankings** | Weighted formula: 30% Win Score, 20% Point Diff, 15% SOS, 15% Recent Form, 10% Efficiency, 5% Quality Wins, 5% Injury Adjustment. Tiered display: Elite / Contender / Fringe / Rebuilding. |

## Multiplayer

| Feature | Details |
|---------|---------|
| **Multi-User Leagues** | Create or join leagues. Each user claims a team. JWT auth. |
| **Per-Game Ready-Up** | Both teams must ready up before a game goes live. CPU opponents auto-ready. |
| **Live Spectating** | Watch games in progress via SSE streaming. |
| **Commissioner Tools** | League management for the league creator. |

## Visual Identity

| Feature | Details |
|---------|---------|
| **Primetime Design System** | Monochrome base with 6 accent tokens (neon, cyan, steel, gold, earth, football). Glass panels with backdrop blur. Card depth system with layered shadows. |
| **SVG Player Portraits** | Procedurally generated 11-layer faces. Seeded RNG ensures the same player always looks the same. |
| **32 Team Logos** | Custom 256x256 PNGs for every franchise. |
| **Typography** | Outfit headlines, DM Sans body, JetBrains Mono stats. |
| **Animations** | Staggered page entrance choreography, stat counter animations, hover reveals, streak pulses. |
