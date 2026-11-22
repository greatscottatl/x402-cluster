# x402-cluster

[![x402 Structured Data & URL Scraper MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper/badges/score.svg)](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper)

Zero-signup web scraping, HTML-to-JSON extraction, and payload compliance checks for AI agents—powered by Cloudflare Workers and **x402** micropayments (**$0.01 USDC** per call on Base L2).

- **Live MCP Endpoint (Streamable HTTP):** `https://x402-cluster.ian-944.workers.dev/v1/mcp.json`
- **Execution Endpoint:** `https://x402-cluster.ian-944.workers.dev/v1/execute`
- **Official MCP Registry:** `io.github.greatscottatl/x402-cluster`
- **Payment Protocol:** HTTP `402 Payment Required` (EIP-3009 `TransferWithAuthorization`, Base Mainnet Chain ID `8453`, USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`)

## Connect via MCP

Add to Cursor, VS Code, or any Streamable HTTP MCP client (`mcp.json`):

```json
{
  "mcpServers": {
    "x402-cluster": {
      "url": "[https://x402-cluster.ian-944.workers.dev/v1/mcp.json](https://x402-cluster.ian-944.workers.dev/v1/mcp.json)"
    }
  }
}
```

## Available Tools ($0.01 USDC / call)

| Tool | Purpose | Max Input |
|---|---|---|
| `extract_from_url` | Fetch a public webpage URL, strip boilerplate, and return strict typed JSON matching `target_schema` in one hop. | Public URL |
| `extract_structured_data` | Convert raw text, receipts, emails, or HTML snippets already in memory into typed JSON conforming to `target_schema`. | 6,000 bytes |
| `parse_web_schema` | Fast flat key-value entity extraction from unstructured text when you only need a list of field names. | 6,000 bytes |
| `validate_compliance` | Audit a JSON payload against PII, KYC, or custom policy rules before executing downstream actions. | JSON object |

## 🚀 Quickstart: Call from an AI Agent

This cluster natively supports the Model Context Protocol (MCP) and x402 monetization. Each execution costs exactly **$0.01 USDC on Base L2**, authorized via a gasless EIP-3009 signature.

### Example: Extract Structured JSON from a URL

```javascript
const payload = {
  tool: "extract_from_url",
  url: "https://example.com/pricing",
  target_schema: { 
    plan_name: "string", 
    price_usd: "number", 
    features: ["string"] 
  }
};

const response = await fetch("https://x402-cluster.ian-944.workers.dev/v1/execute", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    // Pass your signed EIP-3009 TransferWithAuthorization voucher
    "X-402-Authorization": "Bearer <YOUR_SIGNED_EIP3009_VOUCHER>" 
  },
  body: JSON.stringify(payload)
});

const data = await response.json();
console.log(data);
```
