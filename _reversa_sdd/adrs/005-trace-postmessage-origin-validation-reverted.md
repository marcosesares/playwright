# ADR-005 — Trace viewer postMessage origin validation (reverted)

> Status: Reverted
> Date: 2026-06 (commits #41004, #40973)
> Confidence: 🟢 CONFIRMADO — `Revert "fix(trace-viewer): validate origin of postMessage trace blob" (#41004)`

## Context

The trace viewer receives trace data from a parent window via `postMessage`. A fix was added to validate the `event.origin` of these messages as a security measure against cross-origin content injection.

## Decision (Initial)

Add origin validation to the `postMessage` handler in the trace viewer.

## Reversal Decision

The validation was reverted on both `main` and cherry-picked to the release branch.

## Reason for Reversal

🟡 INFERIDO — The origin validation broke legitimate trace viewer usage scenarios where the trace viewer is embedded in contexts with different origins (e.g., VS Code extensions, CI report viewers, local file serving). The strict validation prevented these valid use cases.

## Current State

No `postMessage` origin validation in trace viewer. The trace data is trusted as-is.

## Consequences

- Trace viewer is accessible from cross-origin embeddings
- 🔴 LACUNA — Security posture of trace viewer when embedded in untrusted contexts is unclear. May need a more nuanced approach (allowlist of known origins vs. reject-all).
