---
title: Document Ownership
type: concept
created: 2026-04-05
updated: 2026-04-05
sources: [DOCS_GUARDRAILS.md]
tags: [governance, documentation, ownership]
---
# Document Ownership

Each system has exactly one canonical document. When documents conflict, the owner document wins.

## The Ownership Map

| Domain | Owner Document | What It Owns |
|--------|---------------|--------------|
| Config constants | LOCKED_VALUES | All frozen tuning values in `config.ts` |
| Engine metrics | ENGINE_STATE | Statistical targets, validation ranges |
| Player ratings | game-design.md | Position-specific ratings, which ratings affect simulation |
| Non-engine design | FRANCHISE_SOURCE_OF_TRUTH | Legacy scoring, draft rules, contract structure |
| Documentation rules | DOCS_GUARDRAILS.md | Ownership map itself, update policies |

## Why Single Ownership

When the same fact lives in two documents, they will eventually contradict each other. A rating definition in both `game-design.md` and a README creates ambiguity about which version is correct. Single ownership eliminates this class of bug entirely.

## Conflict Resolution

If two documents make conflicting claims:

1. Identify which document owns the domain
2. The owner document is correct
3. Update the non-owner document to match
4. If ownership is unclear, escalate to DOCS_GUARDRAILS.md — it owns the ownership map

## The Update Rule

Every code change must update its owner document. This is not optional. A change to a tuning constant requires an update to LOCKED_VALUES. A change to a rating formula requires an update to game-design.md. Code and documentation stay synchronized because the ownership model makes it clear which document needs updating.

## Anti-Patterns

- **Duplicated definitions** — The same constant defined in both a README and a config file with no clear owner.
- **Orphaned docs** — Documentation that describes a system but is not recognized as the owner, leading to staleness.
- **Implicit ownership** — "Everyone knows game-design.md owns ratings" is not enough. The ownership must be explicit in DOCS_GUARDRAILS.md.

## See Also

- [[engine-lock]]
- [[system-status-matrix]]
- [[read-only-layers]]
