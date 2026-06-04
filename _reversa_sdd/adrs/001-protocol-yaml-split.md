# ADR-001 — Split protocol.yml into per-interface files

> Status: Accepted
> Date: 2025 (inferred from commit #40645)
> Confidence: 🟢 CONFIRMADO — `chore: split protocol.yml (#40645)`

## Context

The entire Playwright RPC protocol was originally defined in a single monolithic `protocol.yml` file. As the protocol grew to cover 19+ interfaces (Page, Frame, Browser, BrowserContext, Network, Handles, Android, Electron, Tracing, Worker, etc.), the file became difficult to navigate and maintain.

## Decision

Split `protocol.yml` into one YAML file per interface/domain, stored in `packages/protocol/spec/`. Each file defines a subset of the protocol (e.g., `page.yml`, `frame.yml`, `network.yml`).

The generated output files (`channels.d.ts`, validators) are produced from all spec files combined by `npm run watch`.

## Consequences

- Easier to locate and modify a specific interface's contract
- Smaller diffs on protocol changes — reviewers see only the affected interface
- Requires knowledge of which file owns which interface
- New interfaces need a new file created (not just appended to one file)
