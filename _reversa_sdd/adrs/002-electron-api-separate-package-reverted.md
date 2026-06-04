# ADR-002 — Electron API moved to separate package (then reverted)

> Status: Reverted
> Date: 2025 (inferred from commits #40184, #40733, #40736)
> Confidence: 🟢 CONFIRMADO — `feat(electron): move Electron API to a separate package (#40184)` → `chore(electron): revert #40184 (#40733)`

## Context

The Electron automation API was part of `playwright-core`. The team explored separating it into a dedicated package to improve tree-shaking, reduce bundle size for non-Electron users, and clarify the public API surface.

## Decision (Initial)

Move Electron API to a separate package (`playwright-electron` or similar). Commit #40184.

A companion change also added `electronApp.close()` timeout option for force-kill escalation (#40736).

## Reversal Decision

Both changes were reverted shortly after (#40733, #40736, cherry-picks #40733, #40736 on the stable branch).

## Reason for Reversal

🟡 INFERIDO — The reverts were applied to both `main` and cherry-picked onto stable/release branches, suggesting the change caused integration issues, broke existing consumers, or was premature for the release timeline.

## Current State

Electron API remains integrated in `playwright-core`. The separation may be revisited in a future major version.

## Consequences

- Electron users have a stable API location (no breaking import change)
- Non-Electron users continue to include Electron types in their bundles
- Future separation attempts should account for the integration issues that caused the revert
