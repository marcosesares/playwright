# ADR-004 — Replace vendored yauzl with upstream package

> Status: Accepted
> Date: 2026-06 (commit #41102)
> Confidence: 🟢 CONFIRMADO — `fix(yauzl): use upstream yauzl 3.3.2 instead of vendored copy (#41102)`

## Context

Playwright vendored a custom copy of `yauzl` (a ZIP file reading library) to maintain control over its behavior and ensure compatibility with trace file parsing. Over time, maintaining a vendored copy creates drift from upstream bug fixes and security patches.

The upstream `yauzl` 3.3.2 release addressed the concerns that originally motivated vendoring.

## Decision

Remove the vendored copy of `yauzl` and depend directly on `yauzl@3.3.2` from npm.

## Alternatives Considered

Continue vendoring — rejected because upstream now provides the needed behavior.

## Consequences

- Security patches and bug fixes from upstream automatically available
- Reduces maintenance burden (no diff to maintain against upstream)
- Risk: future upstream changes could break compatibility — must monitor yauzl updates carefully
- Trace file ZIP parsing behavior is now tied to upstream release cadence
