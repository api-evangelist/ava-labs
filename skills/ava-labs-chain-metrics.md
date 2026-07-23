---
name: Pull chain and staking metrics
description: Use the AvaCloud Metrics API to list chains and retrieve EVM chain performance and staking metrics for Avalanche L1s.
api: openapi/ava-labs-metrics-api-openapi.yml
operations: [listChains, getChain, getEvmChainMetrics, getStakingMetrics]
---

# Pull chain and staking metrics

Read-only analytics against the Metrics API (`https://metrics.avax.network`). The Metrics API is unauthenticated.

## Steps
1. `listChains` — enumerate supported chains and their identifiers.
2. `getChain` — fetch metadata for a specific chain.
3. `getEvmChainMetrics` — retrieve aggregated performance metrics (transactions, gas, active addresses) for an EVM chain over a time range.
4. `getStakingMetrics` — retrieve Primary Network staking metrics.

## Conventions
- Cursor pagination (`pageToken`/`pageSize` → `nextPageToken`) where result sets are large. See `conventions/ava-labs-conventions.yml`.
- Errors use the `{ statusCode, error, message }` JSON envelope. See `errors/ava-labs-problem-types.yml`.
