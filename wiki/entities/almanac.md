---
title: Almanac
type: entity
created: 2026-04-05
updated: 2026-04-24
sources: [almanac-feature-idea.md]
tags: [almanac, history, complete, deprecated]
---

> **Note:** This page reflects the current Almanac structure after the April 24 replay archive addition. Several former Almanac tabs (Awards, Stats/Leaders) were moved to the League section, and others (Top 10, Past Champions, Past Drafts, History) were consolidated into Season Recaps. See `CLAUDE.md` for the authoritative tab list.

# Almanac

A historical reference hub providing comprehensive league history and preserved key replays. All current tabs are complete.

## Tabs

1. **Hall of Fame** — HOF inductee display with legacy scores and waiting-period logic.
2. **Ring of Honor** — Per-franchise Ring of Honor and jersey retirement.
3. **Records** — Career and single-season records by stat category.
4. **Season Recaps** — Year-by-year season recaps (champion, awards, leaders, standings, draft history).
5. **All-Time Standings** — All-time franchise standings with sortable columns.
6. **Head to Head** — Two-team picker with summary strip and historical results.
7. **Replays** — Preserved key game replays, including playoffs, human-vs-human games, upsets, and record/newsworthy games.
8. **GM Career** — User's GM career stats and history (conditional).

## Implementation

- **Backend:** Aggregation logic in `almanac.ts` computes all historical data from persisted league state.
- **Frontend:** Mirror utilities in `utils/almanac.ts` for client-side formatting and display.
- **Draft history** is persisted at draft completion, ensuring past drafts are always available even as rosters change.
- **Replay archive** is persisted in `game_logs`; ordinary play logs are purged on rollover while key replays remain available through Almanac Replays and `/replay/:leagueId/:gameId`.

## See Also

- [[narrative-systems]]
- [[hall-of-fame]]
