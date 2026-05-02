# Football Sim API Reference

> **Last updated:** 2026-05-02
> **See also:** [system-architecture.md](system-architecture.md) | [configuration-guide.md](configuration-guide.md) | [deployment-guide.md](deployment-guide.md)

Football Sim exposes a REST API plus SSE streams from the Express backend.

## Conventions

- Production base URL: `https://football-sim.fly.dev`
- Development base URL: `http://localhost:3000`
- Auth: `Authorization: Bearer <token>`
- Most mutating league endpoints return a **sanitized full league payload**
- Error shape: `{ "error": "Human-readable message" }`

## Authentication and League Access

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/auth/signup` | Create user and return JWT |
| `POST` | `/auth/login` | Authenticate and return JWT |
| `GET` | `/auth/me` | Validate token and return current user |
| `GET` | `/leagues` | Public league browser |
| `GET` | `/my-leagues` | Authenticated user’s leagues |
| `POST` | `/league/create` | Create a new league |
| `POST` | `/league/join` | Join an existing league |
| `GET` | `/league/:id` | Fetch sanitized league state |
| `POST` | `/league/:id/claim-team` | Claim an unowned team |
| `GET` | `/league/:id/members` | Member list |
| `POST` | `/league/:id/settings` | Commissioner settings update |

## Weekly Advancement and Readiness

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/advance-week` | Synchronous advancement |
| `POST` | `/league/:id/advance-week-async` | Queue background advancement job |
| `GET` | `/league/:id/advance-job/:jobId` | Poll async job status |
| `GET` | `/league/:id/readiness` | Readiness blockers and warnings |
| `POST` | `/league/:id/pause-timer` | Pause auto-advance timer |
| `POST` | `/league/:id/resume-timer` | Resume auto-advance timer |

Readiness covers cap state, roster floor, ready-up, scheduled kickoffs, draft blockers, coach state, contract blockers, and Training Camp blockers.

## Game Day and Streaming

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/game/:gameId/ready` | Mark a team ready |
| `POST` | `/league/:id/game/:gameId/schedule` | Set or clear kickoff time |
| `POST` | `/league/:id/game/:gameId/start` | Start live simulation |
| `POST` | `/league/:id/game/:gameId/sim` | Instant simulation |
| `POST` | `/league/:id/stream-token` | Mint short-lived stream token |
| `GET` | `/league/:id/game/:gameId/live` | Live play-by-play SSE |
| `GET` | `/league/:id/week/:week/highlights` | Weekly highlights SSE |
| `GET` | `/league/:id/game/:gameId/events` | Finished-game event log |
| `GET` | `/league/:id/results/:season` | Season results |
| `GET` | `/league/:id/replays` | Replay archive index |
| `GET` | `/league/:id/replays/:season` | Season replay archive |

Replay preservation includes playoff games, human-vs-human games, major upsets, and record or narrative-worthy games.

## Roster, Contracts, and Free Agency

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/extend-player` | Team extension |
| `POST` | `/league/:id/negotiate-interest` | Preview extension interest |
| `POST` | `/league/:id/fifth-year-option` | Rookie option decision |
| `POST` | `/league/:id/release-player` | Release and create dead cap |
| `POST` | `/league/:id/sign-free-agent` | Direct signing flow |
| `POST` | `/league/:id/offer-contract` | Interest-based FA offer |
| `POST` | `/league/:id/practice-squad/add` | Move player to practice squad |
| `POST` | `/league/:id/practice-squad/promote` | Promote player from practice squad |
| `POST` | `/league/:id/practice-squad/sign` | Sign a free agent to practice squad |

## Waivers, Trades, and Trade Block

| Method | Path | Notes |
|--------|------|-------|
| `GET` | `/league/:id/waivers` | Current waiver pool |
| `POST` | `/league/:id/waivers/claim` | Submit claim |
| `DELETE` | `/league/:id/waivers/claim/:playerId` | Cancel claim |
| `POST` | `/league/:id/propose-trade` | Trade proposal |
| `POST` | `/league/:id/respond-trade` | Accept or reject |
| `GET` | `/league/:id/trade-block` | Trade block view |
| `POST` | `/league/:id/trade-block` | Add player to trade block |
| `DELETE` | `/league/:id/trade-block/:playerId` | Remove player from trade block |
| `POST` | `/league/:id/trade-block/needs` | Ask for AI fit/needs guidance |
| `POST` | `/league/:id/shop-player` | Shop a player league-wide |

## Team Strategy, Schemes, and Playbooks

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/set-depth-chart` | Positional depth chart |
| `POST` | `/league/:id/set-gameplan` | Legacy gameplan payload |
| `POST` | `/league/:id/set-tendencies` | Tendency sliders |
| `POST` | `/league/:id/set-schemes` | Active schemes and practice allocation |
| `POST` | `/league/:id/set-situation-buckets` | Scheme-to-situation mapping |
| `POST` | `/league/:id/set-identity-scheme` | Identity scheme selection |
| `POST` | `/league/:id/set-weekly-gameplan` | Weekly offensive and defensive posture |
| `POST` | `/league/:id/set-rb-usage` | Carry split and passing-down back |
| `POST` | `/league/:id/set-formation-slot` | Offensive formation assignments |
| `POST` | `/league/:id/set-package-slot` | Defensive package assignments |
| `POST` | `/league/:id/set-offensive-plan` | Offensive play selection plan |
| `POST` | `/league/:id/set-defensive-plan` | Defensive play selection plan |
| `POST` | `/league/:id/save-offense-playbook` | Save offensive playbook |
| `POST` | `/league/:id/delete-offense-playbook` | Delete offensive playbook |
| `POST` | `/league/:id/save-defense-playbook` | Save defensive playbook |
| `POST` | `/league/:id/delete-defense-playbook` | Delete defensive playbook |
| `POST` | `/league/:id/save-custom-play` | Save custom offensive play |
| `POST` | `/league/:id/delete-custom-play` | Delete custom offensive play |
| `POST` | `/league/:id/save-custom-defense-play` | Save custom defensive play |
| `POST` | `/league/:id/delete-custom-defense-play` | Delete custom defensive play |

## Scouting and Draft

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/draft-pick` | User draft pick |
| `POST` | `/league/:id/advance-draft-pick` | One CPU pick |
| `POST` | `/league/:id/advance-to-user-pick` | Auto-advance to next user pick |
| `POST` | `/league/:id/sim-draft` | Sim remaining draft |
| `POST` | `/league/:id/draft-board` | Save big board |
| `POST` | `/league/:id/watch-list` | Update scouting watch list |
| `POST` | `/league/:id/scouting-settings` | Watch-list and capacity settings |
| `GET` | `/league/:id/scouting-intel` | Current scouting intel |
| `POST` | `/league/:id/scout-directive` | Assign scout directive |
| `POST` | `/league/:id/scout-auto-draft` | Automated draft setup |
| `POST` | `/league/:id/scout-action` | Scout assistant actions |
| `POST` | `/league/:id/scout-pick` | Assistant-driven pick choice |
| `POST` | `/league/:id/create-prospect` | GM-career prospect creation flow |

## Coaching, Coordinators, and Training Camp

| Method | Path | Notes |
|--------|------|-------|
| `GET` | `/league/:id/coach-market` | Available coaches |
| `POST` | `/league/:id/fire-coach` | Fire current HC |
| `POST` | `/league/:id/promote-coordinator` | Promote OC or DC |
| `POST` | `/league/:id/hire-coach` | Hire from market |
| `GET` | `/league/:id/pending-poach` | Pending poach state |
| `POST` | `/league/:id/respond-poach` | Accept or reject poach outcome |
| `POST` | `/league/:id/training-camp-reroll` | Developer reroll action |

## Notifications and Radio

| Method | Path | Notes |
|--------|------|-------|
| `GET` | `/league/:id/notifications` | Notification inbox |
| `POST` | `/league/:id/notifications/:notificationId/read` | Mark one read |
| `POST` | `/league/:id/notifications/read-all` | Mark all read |
| `POST` | `/league/:id/mark-notifications-read` | Legacy compatibility endpoint |
| `GET` | `/league/:id/radio/episodes` | Episode list |
| `GET` | `/league/:id/radio/episodes/:trigger` | Episode detail and asset URL |
| `POST` | `/league/:id/radio/generate/:trigger` | Queue radio generation |

## Commissioner Operations

| Method | Path | Notes |
|--------|------|-------|
| `POST` | `/league/:id/commissioner/ops/nudge` | Readiness nudge |
| `POST` | `/league/:id/commissioner/ops/force-ready` | Mark team ready |
| `POST` | `/league/:id/commissioner/ops/clear-kickoff` | Clear scheduled kickoff |
| `POST` | `/league/:id/commissioner/force-advance-week` | Override and advance |
| `POST` | `/league/:id/commissioner/force-sim-game` | Force sim a game |
| `POST` | `/league/:id/commissioner/force-pick` | Override draft pick |
| `POST` | `/league/:id/commissioner/rollback-draft-pick` | Roll back latest pick |
| `POST` | `/league/:id/commissioner/transfer-seat` | Move team seat |
| `POST` | `/league/:id/commissioner/transfer-commissioner` | Transfer commissioner role |
| `POST` | `/league/:id/commissioner/kick` | Kick member from league |
| `POST` | `/league/:id/commissioner/invite/create` | Create seat invite |
| `POST` | `/league/:id/commissioner/invite/revoke` | Revoke invite |
| `POST` | `/league/:id/commissioner/set-approval-gated` | Require join approval |
| `POST` | `/league/:id/commissioner/set-league-invite-code` | Shared league code management |
| `POST` | `/league/:id/redeem-invite` | Redeem invite code |
| `POST` | `/league/:id/commissioner/approve-join` | Approve join request |
| `POST` | `/league/:id/commissioner/reject-join` | Reject join request |
| `POST` | `/league/:id/commissioner/announcement/post` | Publish announcement |
| `POST` | `/league/:id/commissioner/announcement/delete` | Delete announcement |
| `POST` | `/league/:id/commissioner/manual/cut` | Manual cut |
| `POST` | `/league/:id/commissioner/manual/add` | Manual add |
| `POST` | `/league/:id/commissioner/manual/move` | Manual move |
| `POST` | `/league/:id/commissioner/manual/edit-contract` | Contract correction |
| `POST` | `/league/:id/commissioner/manual/edit-injury` | Injury correction |
| `GET` | `/league/:id/commissioner/log` | Commissioner log JSON |
| `GET` | `/league/:id/commissioner/log.csv` | Commissioner log CSV |

## Static and Public Endpoints

| Method | Path | Notes |
|--------|------|-------|
| `GET` | `/` | Basic status payload |
| `GET` | `/health` | Health check |
| `GET` | `/formations` | Offensive formations and defensive packages |
| `GET` | `/leaderboard` | Global leaderboard |

## Sanitization Rules

League responses are filtered before returning to clients:

1. hidden prospect truth fields are stripped,
2. scouting data is scoped to the caller’s team,
3. unrevealed college data is truncated,
4. computed helpers such as cap breakdown, playbook fit, and rankings are injected.
