# ADR-003 — MCP Extension Protocol v2 (versioned Chrome extension relay)

> Status: Accepted
> Date: 2025 (inferred from commits #40191, #40193, #40678)
> Confidence: 🟢 CONFIRMADO — multiple commits show v1/v2 transition

## Context

The Chrome extension ↔ Playwright CDP relay used in MCP extension mode was initially unversioned (implicitly v1). As the MCP extension feature evolved (multi-tab support, page close via extension, tab creation), the extension protocol needed changes that were not backward-compatible with existing extensions.

## Decision

Introduce a versioned extension protocol:
- **v1**: Original protocol, limited tab and page lifecycle support
- **v2**: Adds multi-tab support, page close, tab creation, improved lifecycle

MCP server supports both v1 and v2 simultaneously (`feat(mcp): support both v1 and v2 extension protocol #40191`). Default bumped to v2 (`chore(mcp): bump default extension protocol to v2 #40678`).

## Alternatives Considered

🟡 INFERIDO — Alternative of making v1 changes backward-compatible was likely rejected due to protocol message shape conflicts.

## Consequences

- Extensions using v1 continue to work (backward compatible via dual support)
- New extensions should use v2 for full feature access
- MCP server must maintain v1/v2 dispatch logic indefinitely until v1 is deprecated
- Clear error thrown for tab creation attempts via v1 (`fix(mcp): throw clear error for tab creation in extension protocol v1 #40261`)
