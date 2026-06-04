# ADR-007 — Client remote-object switch replaced with factory registry

> Status: Accepted
> Date: 2025 (commit #40672)
> Confidence: 🟢 CONFIRMADO — `refactor(client): replace remote-object switch with a factory registry (#40672)`

## Context

The client layer needed to instantiate the correct `ChannelOwner` subclass when a new object arrived from the server (identified by its protocol type name). The original implementation used a large `switch` statement mapping type names to constructors.

## Decision

Replace the `switch` statement with a factory registry — a `Map<string, Constructor>` where type names are registered at module load time. Each `ChannelOwner` subclass registers itself.

## Alternatives Considered

Keeping the switch — rejected because it required modifying a central file for every new type, creating a merge bottleneck.

## Consequences

- New protocol types register themselves without touching the central dispatch
- Type registration is explicit and co-located with the class definition
- Potential for duplicate registrations if a type name is reused — a tradeoff accepted given the controlled codebase
- Slightly harder to discover all registered types (must grep for `registerType` or equivalent)
