---
title: Multiplayer Game Day
type: entity
created: 2026-04-05
updated: 2026-04-24
sources: [multiplayer-gameday-design.md, src/sse.ts, src/server.ts]
tags: [multiplayer, gameday, live]
---
# Multiplayer Game Day

Per-game lifecycle management for multiplayer leagues, handling readiness, simulation timing, live game streaming, commissioner operations, notifications, and replay preservation.

## Game Lifecycle

```
SCHEDULED → READY → LIVE → FINAL
```

- **SCHEDULED** — Game is on the calendar, not yet ready for simulation.
- **READY** — Both teams (or required teams) have confirmed readiness.
- **LIVE** — Game is being simulated or streamed.
- **FINAL** — Game complete, results persisted.

## League Settings

| Setting | Description |
|---------|-------------|
| `weekDeadlineHours` | Hours before auto-advance of the week |
| `requireReadyUp` | Whether human teams must confirm readiness |
| `allowInstantSim` | Whether games can be simulated immediately |

## Team Readiness

- **CPU teams** auto-ready — no human intervention needed.
- **Human teams** must ready up when `requireReadyUp` is enabled.
- **Commissioner** can force-advance the week regardless of readiness state, nudge owners, force-ready a blocking team, force-sim a game, and clear scheduled kickoff times.

## League Readiness

`GET /league/:id/readiness` powers the commissioner pre-flight view. It reports blockers and warnings for:
- Salary cap compliance
- Roster floor compliance
- Human ready-up state
- Scheduled kickoff timing
- Draft state
- Coach/offseason/training camp state
- Pending contracts

Human-owned teams remain responsible for roster blockers. CPU-only roster repair fills unowned teams with replacement-level one-year contracts so AI roster collapse does not stall long-running leagues.

## Scheduling and Notifications

Owners or commissioners can set/clear planned kickoff times through `POST /league/:id/game/:gameId/schedule`. Affected owners receive persistent notifications. The TopNav notification bell also surfaces league advancement, readiness nudges, commissioner overrides, and archived replay moments.

## Week Deadline Timer

A countdown timer tracks time remaining before auto-advance. Supports **pause** and **resume** for commissioner flexibility.

## Live Streaming

SSE (Server-Sent Events) infrastructure has shipped in `src/sse.ts` — a connection manager for live game streaming + highlights. Both modes are now available:
- **Instant sim + replay** — game simulated immediately, results played back from `boxScore` + `events`.
- **Live SSE stream** — incremental events pushed to connected clients via the `sse.ts` connection manager.

## Spectator Page

Available at `/watch/:leagueId/:gameId` — allows viewing game results and replay for any completed game.

## Replay Archive

Season rollover purges ordinary current-season play logs but preserves key replays:
- Playoff games
- Human-vs-human games
- Major upsets
- Record/newsworthy games

The archive is exposed in Almanac Replays and the standalone `/replay/:leagueId/:gameId` route.

## See Also

- [[simulation-engine]]
