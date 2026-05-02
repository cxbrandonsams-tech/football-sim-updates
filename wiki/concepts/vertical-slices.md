---
title: Vertical Slices
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: [CLAUDE.md, product direction]
tags: [philosophy, product, development]
---
# Vertical Slices

Ship complete vertical slices over partial systems. Each feature should be fully functional end-to-end rather than partially building many features at once.

## The Principle

A vertical slice cuts through every layer of the stack — backend model, engine logic, API endpoint, frontend view — for a single feature. When it ships, the user can interact with the complete feature immediately. The alternative, horizontal slices (build all the models first, then all the APIs, then all the views), leaves everything half-finished for longer and makes integration bugs harder to catch.

## Examples

- **Almanac** shipped all 9 tabs (Records, Franchise, Seasons, Players, Games, Awards, Head-to-Head, Superlatives, Draft History) before moving on to narrative systems. Each tab was backend-to-frontend complete.
- **Narrative** shipped all 4 subsystems (records tracking, rivalry detection, dynasty/drought arcs, narrative news generation) as a cohesive unit before moving to multiplayer.
- **2D Visualization** shipped the full pipeline (formation positioning, route rendering, defensive paths, ball physics, animation loop, playback controls) as one deliverable rather than building formations first and deferring routes.

## Why It Matters

1. **User value sooner** — A complete Almanac is usable on day one. Nine half-built tabs are usable never.
2. **Integration tested** — Building end-to-end forces you to discover API mismatches, type errors, and UX gaps early.
3. **Scope control** — Finishing a slice creates a natural decision point: ship it and move on, or refine it. Horizontal layers create an illusion of progress without a shippable unit.

## When to Break the Rule

Infrastructure that multiple features depend on (auth, database schema, design system tokens) sometimes needs to be built horizontally. But even then, validate it by building one vertical slice through the infrastructure immediately.

## See Also

- [[engine-lock]]
- [[read-only-layers]]
- [[development-timeline]]
