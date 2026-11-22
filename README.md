# x402-cluster

**Official Website & API Keys:** [x402.pages.dev](https://x402-site-6gt.pages.dev/)

[![x402 Structured Data & URL Scraper MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper/badges/score.svg)](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper)

Zero-signup static & headless-browser web scraping, HTML-to-JSON extraction, and payload compliance checks for AI agents—powered by Cloudflare Workers, Browser Run, and **x402** micropayments (**$0.01–$0.05/call**).

- **Live MCP Endpoint (Streamable HTTP):** `https://x402-cluster.ian-944.workers.dev/v1/mcp.json`
- **Execution Endpoint:** `https://x402-cluster.ian-944.workers.dev/v1/execute`
- **Official MCP Registry:** `io.github.greatscottatl/x402-cluster` (`v3.4.0`)
- **Prepaid API Keys (Credit Card):** [Buy 1,000 Credits ($10 USD)](https://buy.stripe.com/bJeeVd123fOz71reI60kE00) — instant `sk_live_...` key delivery
- **Crypto Rail:** HTTP 402 Payment Required (`EIP-3009` `TransferWithAuthorization`, Base Mainnet Chain ID `8453`, USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`)

## Connect via MCP

Add to Cursor, Claude Desktop, VS Code, or any Streamable HTTP MCP client (`mcp.json`):

```json
{
  "mcpServers": {
    "x402-cluster": {
      "url": "[https://x402-cluster.ian-944.workers.dev/v1/mcp.json](https://x402-cluster.ian-944.workers.dev/v1/mcp.json)",
      "headers": {
        "Authorization": "Bearer sk_live_YOUR_API_KEY"
      }
    }
  }
}
