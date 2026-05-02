---
title: Frontend Stitch Redesign
type: entity
created: 2026-04-07
updated: 2026-04-08
sources: [CLAUDE.md, docs/superpowers/plans/2026-04-07-stitch-dashboard.md, docs/superpowers/plans/2026-04-07-coach-archive-and-team-reskin.md, web/src/views/DashboardView.tsx, web/src/tailwind.css]
tags: [frontend, design-system, stitch, ui, deprecated]
---

> **Deprecated — Historical Reference Only.** The M3 rollout is **complete** (all 11 sub-specs shipped as of 2026-04-13). All views have been migrated to Stitch/Primetime. Design tokens moved from Gold+Fire to Monochrome+Accent (Primetime): monochrome base (silver primary, pure neutral surfaces) with 6 accent tokens (neon, cyan, steel, gold, earth, football). Offense = Gold accent, Defense = Cyan accent. Typography updated to Outfit (headlines) + DM Sans (body). See `CLAUDE.md` for the current authoritative design system documentation. The content below is preserved as historical reference only and should not be used for implementation decisions.

# Frontend Stitch Redesign

A page-by-page rebuild of the Football Sim frontend using Google Stitch as the design source. Started April 7, 2026 with the Dashboard view. **`DashboardView` is the canonical template** for every other page going forward.

## Status

**COMPLETE** — All views have been migrated to Stitch/M3. The color system has since been updated to Monochrome + Accent palette.

## Why Stitch

The original Figma rewrite (April 2, 2026) shipped a consistent dark UI but lacked the editorial weight and material polish the project wanted. Google Stitch produces production-ready HTML mockups grounded in Material 3 tokens, giving:

- Editorial typography (Space Grotesk display, Manrope body, Material Symbols icons)
- A semantic color system (`primary` / `secondary` / `tertiary` / `error` rather than raw Tailwind palette colors)
- Glassmorphism cards over a stadium backdrop instead of flat dark slabs
- Headlines and stats that feel like a sports magazine rather than a generic admin dashboard

## Workflow per page

1. **Generate** the design in Google Stitch using the Stitch dashboard as the visual reference (so the family stays cohesive).
2. **Export** the Stitch HTML/JSX into `docs/figma-export/make-src/`.
3. **Plan + spec** under `docs/superpowers/plans/` and `docs/superpowers/specs/`.
4. **Rebuild** the view using only the Stitch tokens (see Visual Contract below).
5. **Hide rails** for the rebuilt page — add the tab name to the side-rail exclusion lists in `App.tsx` (~lines 192 + 251) so the page renders full-bleed.
6. **Verify** with `cd web && npm run build` (must stay clean against the lint baseline of 159 problems) and a manual visual checkpoint at the configured viewports.

## Visual contract

Every Stitch page must honor:

- **App background** = `bg-background` (`#0c0e17`), with `web/public/assets/backdrops/stadium-night.jpg` rendered fixed under the content via the `from-[#0c0e17]/90 via-[#0c0e17]/70 to-[#0c0e17]` gradient overlay used in `DashboardView`.
- **Cards** use `glass-panel rounded-[12px] p-6 border border-outline-variant/15`, never the legacy `#131b28` slab.
- **Headlines** = `font-headline` (Space Grotesk) + bold + tight tracking. **Stats** = `font-mono tabular-nums`. **Labels** = `font-label` uppercase tracking-wider.
- **Icons** = `<MaterialIcon name="..." />` from `components/MaterialIcon.tsx`. Lucide icons are forbidden on Stitch pages.
- **Colors** use semantic Material 3 tokens (`text-primary` / `text-secondary` / `text-tertiary` / `text-error`) instead of hard-coded Tailwind palette values like `text-emerald-400`.
- **Player tiles** without photos use `<InitialsAvatar name position size />`.

## Design tokens

Defined in the `@theme` block of `web/src/tailwind.css`:

| Category | Tokens |
|----------|--------|
| Background | `--color-background` `#0c0e17`, `--color-surface`, `--color-surface-container-{lowest,low,high,highest}`, `--color-surface-bright` |
| Text | `--color-on-surface` `#f0f0fd`, `--color-on-surface-variant` `#aaaab7` |
| Primary | `#ff8d8c` (CTA + record badges), `--color-on-primary-fixed` for buttons |
| Secondary | `#00f4fe` (accents, division highlights, win streaks) |
| Tertiary | `#ffc965` (cap free, warnings) |
| Error | `#ff716c` (loss streaks, injuries marked Out) |
| Outline | `--color-outline` `#737580`, `--color-outline-variant` `#464752` |
| Fonts | `--font-headline` Space Grotesk, `--font-body` Manrope, `--font-label` Inter, `--font-mono` JetBrains Mono |

## Canonical template — DashboardView

`web/src/views/DashboardView.tsx` is the reference implementation. It is **simultaneously** the user's Dashboard tab and the Team Page for any other team — there is no separate route. Ownership context is passed via a separate `myTeamId` prop alongside the viewed `teamId`.

### Key contract

| Prop | Purpose |
|------|---------|
| `teamId` | The team being viewed. Bound from `dashboardTeamId ?? myTeamId` in `App.tsx`. |
| `myTeamId` | The user's owned team — used for context-aware decisions. |
| `standings` | Computed standings for ranks. |
| `busy` | Disables Watch Live + Simulate buttons during in-flight requests. |
| `onWatchGame(gameId)` | Routes to the Game Day view. |
| `onSimGame(gameId)` | Calls `gameSim` API and replaces league state. |
| `onViewPlayer(id)` | Opens the player detail modal. |
| `onViewTeamDashboard(teamId)` | Loads another team in this same view. |
| `onLeagueUpdate(league)` | Replaces the cached league after mutations. |

### Section layout

1. **Hero card** — team logo + name watermark, division rank label, record pill, and a 4-cell stat row: **Off Rank + PPG**, **Def Rank + PPG Allowed**, **Cap Free** (`$X.XM`), **W/L Streak**.
2. **Left column** — Division Standings table + Playoff Race (top 7 conference seeds).
3. **Middle column** — Team Leaders (Pass / Rush / Rec yardage cards with `InitialsAvatar`) + Weekly Recap news strip.
4. **Right column** — Up Next card (current team vs opponent + **Watch Live** + **Simulate** buttons) + Injury Report (top 3 by severity).
5. **Recent Schedule** — horizontal scroll, oldest game on the left, most recent on the right.

### Routing rules

- Clicking **Dashboard** in `TopNav` resets `dashboardTeamId = null`, snapping back to the user's owned team. Wrapped via `handleSetTab()` in `App.tsx`.
- Clicking another team anywhere in the app calls `handleViewTeamDashboard(teamId)` which sets `dashboardTeamId` then navigates to the dashboard tab.
- The deleted `team-dashboard` tab and `TeamDashboardView.tsx` are gone — `DashboardView` covers both cases.

## Pages still on legacy chrome

The remaining sections (League, Almanac, GM, Scouting, Game Day) still use the legacy Figma cards (`bg-[#131b28]/80` slab + Lucide icons + ad-hoc Tailwind palette colors). The Stitch redesign rolls them out individually. Order is driven by user direction.

Tracked in [[near-term-roadmap]].

## Shipped Stitch pages

| Page | Date | Notes |
|------|------|-------|
| `DashboardView` | 2026-04-07 | Canonical template. Used for the user's Dashboard tab and any other team. |
| Team > Overview (`RosterStitchView` + `PlayerSpotlightStitch`) | 2026-04-07 | 8/4 12-column grid with stadium backdrop. |
| Team > Depth Charts (`DepthChartView`) | 2026-04-08 | 85/15 layout under shared `<TeamBackdrop>`. Per-unit color tints in Stitch tokens. |
| Team > Gameplans (`GameplansPanel` + `PhilosophySlidersPanel`) | 2026-04-08 | Offense=primary coral + sports_football icon, defense=tertiary amber + shield icon. |
| Team > Playbooks (`PlaybooksPanel` + `playbooks/*`) | 2026-04-08 | Active playbook accent uses `ring-primary` + `bg-primary/[0.06]`. |

## See Also

- [[system-status-matrix]] — Frontend UI status and lock state
- [[development-timeline]] — when the Figma rewrite shipped vs the Stitch rebuild
- [[vertical-slices]] — why we ship one full page at a time, not partial systems
- [[near-term-roadmap]] — which page is queued next
