# Design

Football Sim uses the **Primetime** design system — a premium dark-mode visual identity built for dense information display without feeling cluttered.

---

## Primetime Color System

**Monochrome base** with pure neutral surfaces (no blue-tinted grays). Six accent colors provide semantic meaning:

| Token | Hex | Usage |
|-------|-----|-------|
| **Neon** | `#2bff5e` | Interactive highlights, active states, badges |
| **Cyan** | `#00d4ff` | Defense accent, top-rated player highlights, secondary CTAs |
| **Steel** | `#5b8fcc` | Neutral emphasis, mid-tier indicators |
| **Gold** | `#d4a017` | Offense accent, premier awards, primary CTAs |
| **Earth** | `#8B6914` | Expiring contracts, aging indicators |
| **Football** | `#8B4513` | Thematic accents |

**Convention:** Offense = gold, Defense = cyan. This applies across the Team section — playbooks, gameplans, roster filters, and spotlight stats all follow this split.

## Typography

| Role | Font | Usage |
|------|------|-------|
| **Headlines** | Outfit | Section titles, nav buttons, hero stats |
| **Body/Labels** | DM Sans | Body text, table cells, form labels |
| **Stats** | JetBrains Mono | Numeric data, OVR ratings, salary figures, countdown timers |

## Glass Panels

Cards use `bg-black/60 backdrop-blur-md` with a layered depth system:
- **Top-border highlight** — subtle lighter edge at the top of each card
- **Gradient background** — dark-to-darker gradient on hover
- **Dual-layer shadows** — ambient shadow + tighter shadow for lift effect
- **Hover reveal** — cards lift slightly on hover with a gradient reveal

Two surface modes: `glass` (used in Dashboard, Awards, Almanac) and `panel` (used in Depth Charts, Gameplans, Playbooks).

## Page Entrance Choreography

Every page uses staggered CSS animations (`pt-enter` classes with delay variants `pt-enter-d0` through `pt-enter-d5`). Elements fade in and translate upward with 0.3s ease-out timing, creating a polished reveal sequence when navigating between sections.

## Component Kit (Stitch)

8 primitives power the UI:

| Component | Purpose |
|-----------|---------|
| **StitchCard** | Container with glass/panel surface modes and depth system |
| **StitchSection** | Titled content section with eyebrow label |
| **StitchTabBar** | Horizontal tab navigation with accent underline |
| **StitchTable** | Sortable data table with density options |
| **StitchChipRail** | Horizontal filter chip strip with pill and text variants |
| **StitchStatCell** | Numeric stat display with label |
| **StitchBadge** | Status indicator (ok/warn/error tones) |
| **StitchHeroStat** | Large hero-sized stat with label and optional fire accent |

## Player Portraits

Every player, prospect, and Hall of Famer has a unique procedurally generated SVG portrait:
- 11 composited layers (face shape, skin tone, hair style, eyes, nose, mouth, facial hair, accessories, etc.)
- Seeded RNG (FNV-1a hash + Mulberry32 PRNG) ensures the same player always generates the same face
- 10 numeric appearance indices persist across the player's career, through retirement, into the Hall of Fame
- `PlayerAvatar` wrapper falls back to `InitialsAvatar` (position-tinted gradient + initials) when portrait data is missing

## Navigation

7 top-level sections:

| Section | Sub-tabs |
|---------|----------|
| **Dashboard** | Team overview with league feed sidebar |
| **Team** | Overview, Depth Charts, Gameplans, Playbooks | Trades, Free Agents |
| **Scouting** | College, Prospects, Scouting HQ, Draft Board |
| **Game Day** | Full-screen match visualization |
| **League** | Standings, Rankings, Stats, News, Playoffs, Awards, Commissioner |
| **Almanac** | 13 historical reference tabs |
| **Draft** | Draft room (conditional — only during draft phase) |

The Team section uses a visual separator (`|`) in its sub-nav to distinguish on-field tabs (Overview through Playbooks) from front-office tabs (Trades, Free Agents).
