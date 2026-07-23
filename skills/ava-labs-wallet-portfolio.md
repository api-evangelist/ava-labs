---
name: Look up an address's wallet portfolio and history
description: Use the AvaCloud Data API to resolve an address's chains, native and token balances, and recent transactions across Avalanche L1s.
api: openapi/ava-labs-data-api-openapi.yml
operations: [listAddressChains, getNativeBalance, listErc20Balances, listErc721Balances, listTransactions, listNativeTransactions, getTxByHash]
---

# Look up an address's wallet portfolio and history

Read-only workflow against the AvaCloud Data API (`https://glacier-api.avax.network`).

## Auth
Send an API key in the `x-glacier-api-key` header (obtain one at https://avacloud.io/). Unauthenticated calls work but are rate-limited; a `429` means back off. See `authentication/ava-labs-authentication.yml`.

## Steps
1. `listAddressChains` — discover which networks the address has been active on so you only query relevant chains.
2. `getNativeBalance` — fetch the native (AVAX/gas-token) balance for a chain.
3. `listErc20Balances` (and `listErc721Balances` for NFTs) — enumerate token holdings.
4. `listTransactions` / `listNativeTransactions` — page recent activity using cursor pagination: pass `pageSize` and the returned `nextPageToken` back as `pageToken`.
5. `getTxByHash` — drill into a specific transaction.

## Conventions
- Pagination is cursor-based (`pageToken`/`pageSize` → `nextPageToken`). See `conventions/ava-labs-conventions.yml`.
- Errors use a flat `{ statusCode, error, message }` JSON envelope. See `errors/ava-labs-problem-types.yml`.
- Select network via mainnet vs testnet (Fuji) or the `chainId` path param.
