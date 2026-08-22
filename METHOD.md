# Counterfeed method (first experiment)

Product: live counterparty feed for public MCP remotes.
Not a directory. Not a dashboard product. Machine-readable status plus substitutes.

## Scope
- Frozen list of public MCP remotes (~48). GitHub properties are on the list but not probed until released.
- No paid third-party monitors, no escrow, no crypto rails.
- Fiat invoice later if an operator wants the webhook.

## Probe
- Public documented HTTP MCP endpoints only.
- Verdicts: UP, DOWN, AUTH_BROKEN.
- UP includes a normal OAuth/401 challenge (server is alive).
- AUTH_BROKEN: 401 with no usable auth surface.
- Record timestamp, HTTP status, latency ms.

## Diff
- First successful pass is baseline. No SCHEMA_DRIFT until a later snapshot changes schema, auth, or capabilities.

## Matcher
- SUBSTITUTE only after DOWN, AUTH_BROKEN, or a path-killing SCHEMA_DRIFT.
- Next-best must be another public remote on the frozen list.

## Publish
- This repo: raw `status.json` and a static status page.
- Webhook waits for a paying operator.

## First pass
- 2026-08-22 17:15 America/New_York
- 48 probed, 43 UP, 1 DOWN, 4 AUTH_BROKEN
- DOWN: paypal (https://mcp.paypal.com/http 404)
- AUTH_BROKEN: actwise-ideation, adplane, adramp, agentic-news
