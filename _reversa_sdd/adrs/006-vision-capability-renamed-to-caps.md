# ADR-006 — --vision flag deprecated in favor of --caps capability system

> Status: Accepted (--vision deprecated)
> Date: 2025 (inferred from program.ts deprecation message)
> Confidence: 🟢 CONFIRMADO — `packages/playwright-core/src/tools/mcp/program.ts:89`

## Context

The MCP server initially exposed a single `--vision` flag to enable screenshot-based visual tools. As the number of optional tool groups grew (pdf, devtools, testing, network, storage, etc.), a single boolean flag per capability became unscalable.

## Decision

Introduce a `--caps` flag accepting a comma-separated list of capability names. The `--vision` flag is preserved but:
1. Emits a deprecation warning: `"The --vision option is deprecated, use --caps=vision instead"`
2. Internally remaps to `caps: 'vision'`

Special rule: `--caps=tracing` implicitly adds `devtools` capability.

## Alternatives Considered

Individual boolean flags per capability — rejected; too many CLI flags as capabilities grow.

## Consequences

- Existing `--vision` users see a deprecation warning but no breakage
- New capabilities added via `--caps` without API churn
- `--vision` will eventually be removed in a future major version
- `PLAYWRIGHT_MCP_CAPS` env var mirrors the `--caps` flag for non-CLI config
