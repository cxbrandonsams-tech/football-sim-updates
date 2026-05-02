---
title: System Status Matrix
type: synthesis
created: 2026-04-05
updated: 2026-04-25
sources: [ENGINE_STATE, LOCKED_VALUES, CLAUDE.md, project memory]
tags: [status, overview]
---

> **Updated 2026-04-25.** See `CLAUDE.md` for the canonical current system state.

# System Status Matrix

Current lock status, last updated date, and owner document for every system in the project.

## Status Definitions

- **LOCKED** — Frozen after validation. Changes require statistical justification. See [[engine-lock]].
- **FROZEN** — Constants are immutable. New constants can be added for new mechanics.
- **EXTENSIBLE** — Core is stable but designed for additive expansion.
- **COMPLETE** — Feature-complete for current scope. Bug fixes only.
- **ACTIVE** — Currently under development.

## Matrix

| System | Status | Last Updated | Owner Document |
|--------|--------|-------------|----------------|
| Core Engine | LOCKED | Mar 29, 2026 | ENGINE_STATE |
| Ratings | LOCKED | Mar 27, 2026 | game-design.md |
| Tuning Constants | FROZEN | Apr 8, 2026 | LOCKED_VALUES |
| League Structure | LOCKED | Mar 27, 2026 | FRANCHISE_SOURCE_OF_TRUTH |
| Coaching (HC/OC/DC) | COMPLETE / MONITORED | Apr 25, 2026 | FRANCHISE_SOURCE_OF_TRUTH §2 |
| Playbooks | EXTENSIBLE | Apr 5, 2026 | game-design.md |
| Tendencies + Front-Office Personalities | LOCKED | Apr 8, 2026 | FRANCHISE_SOURCE_OF_TRUTH §6 |
| Scouting (4-stage confidence system) | COMPLETE | Apr 13, 2026 | game-design.md |
| Hall of Fame / Ring of Honor | LOCKED | Apr 3, 2026 | FRANCHISE_SOURCE_OF_TRUTH |
| Narrative | LOCKED v1 | Apr 5, 2026 | FRANCHISE_SOURCE_OF_TRUTH |
| Frontend UI (legacy Figma chrome) | COMPLETE | Apr 6, 2026 | CLAUDE.md |
| Frontend UI (Stitch redesign) | COMPLETE | Apr 13, 2026 | [[frontend-stitch-redesign]] |
| 2D Visualization | COMPLETE | Apr 5, 2026 | CLAUDE.md (matchviz section) |
| Almanac | COMPLETE | Apr 5, 2026 | FRANCHISE_SOURCE_OF_TRUTH |
| Multiplayer Game Day | COMPLETE / EXTENSIBLE | Apr 24, 2026 | [[multiplayer-gameday]] |
| Commissioner League Ops | COMPLETE / EXTENSIBLE | Apr 24, 2026 | [[multiplayer-gameday]] |
| Notifications | COMPLETE | Apr 24, 2026 | API reference |
| Replay Archive | COMPLETE | Apr 24, 2026 | [[almanac]] / API reference |
| Playbook Fit | COMPLETE | Apr 5, 2026 | game-design.md |
| Seeded Balance CI | COMPLETE | Apr 25, 2026 | testing-guide.md / deployment-guide.md |

The Frontend UI is split into two rows for historical tracking. The legacy Figma chrome row marks when the original views were feature-complete; the Stitch redesign row marks when all views were rebuilt on the Stitch/Primetime design system (completed 2026-04-13). See [[frontend-stitch-redesign]].

The original coach carousel/attribute subsystem remains archived from the 2026-04-08 cutover, but the current lightweight HC/OC/DC system is active and monitored by the seeded balance gate. See FRANCHISE_SOURCE_OF_TRUTH §2.

## Reading the Matrix

Systems marked LOCKED or FROZEN are governed by [[document-ownership]] rules. Their owner document is the single source of truth. EXTENSIBLE systems accept new additions (e.g., new playbook schemes) but their existing definitions are stable. ACTIVE systems are in flux and may not yet have a finalized owner document.

## See Also

- [[engine-lock]]
- [[document-ownership]]
- [[development-timeline]]
- [[near-term-roadmap]]
