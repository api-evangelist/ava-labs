---
name: Monitor addresses with AvaCloud webhooks
description: Create and manage an AvaCloud webhook that fires on address_activity, and verify delivered payloads with the shared secret.
api: openapi/ava-labs-data-api-openapi.yml
operations: [createWebhook, listWebhooks, getWebhook, addAddressesToWebhook, removeAddressesFromWebhook, generateOrRotateSharedSecret, getSharedSecret, deactivateWebhook]
---

# Monitor addresses with AvaCloud webhooks

Managed under `/v1/webhooks` on the Data API host; requires the `x-glacier-api-key` header.

## Steps
1. `createWebhook` — register a delivery URL and the addresses to watch for the `address_activity` event type. Optionally set `includeLogs` / `includeInternalTxs`.
2. `generateOrRotateSharedSecret` — obtain the shared secret used to verify inbound payloads; `getSharedSecret` retrieves the current one.
3. `addAddressesToWebhook` / `removeAddressesFromWebhook` — adjust the watched address set without recreating the webhook.
4. `listWebhooks` / `getWebhook` — inspect existing subscriptions.
5. `deactivateWebhook` — stop deliveries.

## Verifying deliveries
Each POST payload carries `webhookId`, `eventType`, `messageId`, and `event`. Verify the signature against the shared secret before trusting it. See `asyncapi/ava-labs-webhooks.yml`.

## Conventions
Errors follow the `{ statusCode, error, message }` envelope (`errors/ava-labs-problem-types.yml`). Webhook writes are not documented as idempotent — do not blindly retry create calls.
