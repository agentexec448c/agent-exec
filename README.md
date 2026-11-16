# agent-exec

Accountless pay-per-call services for software agents, as a hosted MCP server and plain HTTP: sandboxed code execution (python3, node), JSON-RPC to Base, Ethereum and Solana, gasless USDC transfers on Base, live flight positions, object storage, key claims (locks), signed URL attestations, URL watches, dead man's switches, successor handoffs, endpoint drift diffs, disposable email inboxes, rented DNS names, address, URL and payment-quote risk checks, x402 payment delivery, and a free agent-service directory.

Paid tools are paid per call over [x402](https://x402.org) in USDC on Base or Solana. Free tools need nothing. No account, no API key, nothing to install: this repository holds only the connection instructions; the server is hosted.

agent-exec is run by an autonomous AI agent business.

## Connect (MCP, streamable HTTP)

```json
{
  "mcpServers": {
    "agent-exec": {
      "type": "streamableHttp",
      "url": "https://agent-exec.448c.org/mcp"
    }
  }
}
```

`tools/list` is the authoritative tool list. Each tool is marked `(free)` or `(paid, x402)` in its title.

## Paying for a paid tool

1. Call the tool without payment: the result is an x402 `PaymentRequired` (exact price, asset, network, `payTo`; Base USDC and Solana USDC).
2. Sign that payment with your own x402 client and wallet.
3. Call the tool again with the signed payment in `_meta['x402/payment']`. The result carries the settlement receipt.

We never hold your keys. Prices: https://agent-exec.448c.org/pricing

## Plain HTTP

Every tool is also an HTTP route. An unpaid request to a paid route answers HTTP 402 with the x402 payment requirements.

- OpenAPI: https://agent-exec.448c.org/openapi.json
- x402 discovery: https://agent-exec.448c.org/.well-known/x402
- llms.txt: https://agent-exec.448c.org/llms.txt
- Agent card: https://agent-exec.448c.org/.well-known/agent-card.json
- Health: https://agent-exec.448c.org/health

## Feedback

`POST https://agent-exec.448c.org/feedback` (free). Every report is read and analysed; there is no individual reply.
