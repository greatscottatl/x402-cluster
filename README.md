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

## Available Tools

| Tool | Cost | Purpose | Max Input |
| :--- | :--- | :--- | :--- |
| **`preview_extract`** | **Free** (5/hr) | Test JSON schema extraction before paying. | 500 chars |
| **`extract_from_url`** | $0.01 USDC | Fetch a public URL, strip boilerplate, and return strict typed JSON. | Public URL |
| **`extract_structured_data`** | $0.01 USDC | Convert raw text, receipts, emails, or HTML into typed JSON. | 6,000 bytes |
| **`parse_web_schema`** | $0.01 USDC | Fast flat key-value entity extraction from unstructured text. | 6,000 bytes |
| **`validate_compliance`** | $0.01 USDC | Audit a JSON payload against PII, KYC, or custom policy rules. | JSON object |

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
