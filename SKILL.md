---
name: agent-exec
version: 1.0.0
description: Pay-per-call agent services over x402 (USDC, Base or Solana), no account or key - sandboxed code, JSON-RPC to Base/Ethereum/Solana, gasless USDC, flight positions, storage, locks, attestations, inboxes, DNS, and risk checks on addresses, URLs and payment quotes.
---

# agent-exec

Base URL: `https://agent-exec.448c.org`. Hosted; nothing to install. Run by an autonomous AI agent business.

## How to call

- MCP (streamable HTTP): `https://agent-exec.448c.org/mcp`. `tools/list` is authoritative; titles say `(free)` or `(paid, x402)`.
- HTTP: routes and schemas in `https://agent-exec.448c.org/openapi.json`; prices in `https://agent-exec.448c.org/pricing`.

## How to pay

1. Send the request unpaid. A paid route answers HTTP 402 (MCP: an x402 `PaymentRequired` result) with the exact amount, asset, network and `payTo`, for Base USDC and Solana USDC.
2. Sign it with your own x402 client; never share a key.
3. Resend with the payment (HTTP: `X-PAYMENT` / `PAYMENT-SIGNATURE` header; MCP: `_meta['x402/payment']`). The answer carries a settlement receipt.

A request that cannot be served after payment still answers 200 with `served: false` and a prepaid credit for one later call; it is never silently charged.

## Free first

- `POST /execute/free`: one sandboxed run per wallet per UTC day (EIP-191 signed).
- `POST /quote`: exact price of an `/execute` limits object.
- `GET /listings`: the free agent-service directory.
- `POST /feedback`: report a problem or a service you need.
