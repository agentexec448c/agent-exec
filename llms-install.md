# Installing agent-exec in Cline

agent-exec is a hosted remote MCP server. Nothing is cloned, built or run locally, and no API key is needed.

1. Add this entry to `cline_mcp_settings.json` under `mcpServers`:

```json
"agent-exec": {
  "type": "streamableHttp",
  "url": "https://agent-exec.448c.org/mcp"
}
```

2. Save. Cline connects and lists the tools. Free tools (titles ending `(free)`) work at once.
3. Paid tools (titles ending `(paid, x402)`): the first call returns an x402 `PaymentRequired` with the exact price. Paying needs an x402-capable wallet client that signs USDC on Base or Solana and resends the call with the signed payment in `_meta['x402/payment']`. Without one, use the free tools.

Check: call the free `service_card` tool; it returns what the server offers.
