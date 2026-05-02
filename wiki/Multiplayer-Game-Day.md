# Multiplayer Game Day

Multiplayer game day is built around a simple lifecycle:

`SCHEDULED → READY → LIVE → FINAL`

## Readiness

- CPU teams auto-ready.
- Human teams may need to ready up before a game can go live.
- Commissioners can see readiness blockers through the league readiness view.

## Scheduling

Games can be scheduled with a kickoff time.

- Owners can set or clear a planned live kickoff.
- Scheduled games can be advanced into a live session when the time is right.
- Persistent notifications tell owners what changed.

## Live Play

When a game goes live, it can be watched in real time or simulated instantly.

- Live mode streams events through the SSE layer.
- Instant sim still preserves the game result and replay data.

## Advance Flow

Multiplayer leagues can advance asynchronously.

- The league can queue a background week advance.
- Commissioners can inspect blockers before the advance runs.
- Final results and key replays are preserved in the history stack.

## Replays

Important games remain available after the live window closes. That includes playoff games, human-vs-human games, and other notable results.

## Why It Matters

Multiplayer is not just "the same league with other users in it." The readiness, scheduling, and replay systems are there to keep real people coordinated without forcing everyone into the same browser window at the same time.
