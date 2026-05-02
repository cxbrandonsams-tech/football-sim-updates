---
title: "Source: ARCHITECTURE.md"
type: source
created: 2026-04-05
updated: 2026-04-24
sources: [docs/ARCHITECTURE.md]
tags: [architecture, overview]
---

# Source: ARCHITECTURE.md

**File:** `docs/ARCHITECTURE.md`
**Date:** 2026-04-24
**Status:** Active

## Summary

Comprehensive system design covering the full application stack. Two-service architecture: React SPA on Vercel + Express API on Fly.io. Documents the domain model (League → Teams → Players → Games), persistence layer (SQLite with JSON blob storage per league plus supporting tables), JWT authentication, multi-league isolation, API server patterns, and multiplayer operations.

## Key Takeaways

- Each league is a single JSON blob — deserialized, mutated, re-serialized per write
- Frontend is Tailwind-only with 7 primary top-nav buttons (Dashboard / Team / Scouting / Game Day / League / Almanac / Draft) and a 3-column layout (17rem/1fr/17rem)
- All sections now on Stitch/M3 design system as of 2026-04-13. Primetime visual identity: Outfit headlines + DM Sans body + JetBrains Mono stats, Material Symbols Outlined icons, monochrome base with 6 accent tokens (neon, cyan, steel, gold, earth, football). Legacy Figma chrome fully replaced.
- MatchViz in `components/matchviz/` with field.ts coordinate system, tokens.ts identity builder
- Multiplayer operations shipped 2026-04-24: async advance, readiness pre-flight, scheduling, notifications, replay archive, Commissioner League Ops, and CPU roster floor repair

## Wiki Pages Updated
- [[simulation-engine]]
- [[multiplayer-gameday]]

## See Also
- [[source-engine-state]]
- [[source-game-design]]
