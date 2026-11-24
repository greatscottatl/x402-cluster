# x402-cluster

**Official Website & API Keys:** [x402-site-6gt.pages.dev](https://x402-site-6gt.pages.dev/)

[![x402 Structured Data & URL Scraper MCP connector – tool definition quality and endpoint health on Glama](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper/badges/score.svg)](https://glama.ai/mcp/connectors/dev.workers.ian-944.x402-cluster/x402-structured-data-and-url-scraper)

Zero-signup static & headless-browser web scraping, HTML-to-JSON extraction, and payload compliance checks for AI agents—powered by Cloudflare Workers, Browser Run, and **x402** micropayments (**$0.01–$0.05/call**).

- **Live MCP Endpoint (Streamable HTTP):** `https://x402-cluster.ian-944.workers.dev/v1/mcp.json`
- **Execution Endpoint:** `https://x402-cluster.ian-944.workers.dev/v1/execute`
- **Official MCP Registry:** `io.github.greatscottatl/x402-cluster` (`v3.4.0`)
- **Prepaid API Keys (Credit Card):** [Buy 1,000 Credits ($10 USD)](https://buy.stripe.com/bJeeVd123fOz71reI60kE00) — instant `sk_live_...` key delivery
- **Crypto Rail:** HTTP 402 Payment Required (`EIP-3009 TransferWithAuthorization`, Base Mainnet Chain ID `8453`, USDC `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`)

## Try It Free (No API Key Required)

Test any URL with `preview_extract` (3 free calls/hr per IP). It runs the exact same headless Chromium + LLM pass as a paid run—missing or blocked fields return real `null`s, while populated fields return masked with their type and length so you can verify DOM visibility before spending anything:

```bash
curl -X POST https://x402-cluster.ian-944.workers.dev/v1/execute \
  -d '{
    "tool": "preview_extract",
    "url": "https://news.ycombinator.com",
    "target_schema": {
      "top_story_title": "string",
      "points": "number"
    }
  }'
```

**Sample response:**

```json
{
  "top_story_title": "<populated: string (42 chars)>",
  "points": "<populated: number>"
}
```

## Connect via MCP

Add to Cursor, Claude Desktop, VS Code, or any Streamable HTTP MCP client (`mcp.json`):

```json
{
  "mcpServers": {
    "x402-cluster": {
      "url": "https://x402-cluster.ian-944.workers.dev/v1/mcp.json",
      "headers": {
        "Authorization": "Bearer sk_live_YOUR_API_KEY"
      }
    }
  }
}
```

## Billing Policy & Failed Runs

x402 charges per successful extraction attempt, not per perfect schema match.

- **Billed:** The headless browser successfully loads the URL and the LLM completes its extraction pass. If the requested data simply isn't in the DOM (e.g., hidden behind a CAPTCHA, login wall, or unexpected structure) and returns `null`/missing fields, **you are still charged**. The compute and LLM tokens were fully spent trying to extract it.
- **Not Billed:** Infrastructure failures. If the headless browser times out, Cloudflare crashes, or the Worker throws a `500` error, you are not charged.

**Best Practice:** Always test your target sites with the free `preview_extract` tool first. This lets you verify the LLM can actually see the data on that specific DOM before wiring it up to a paid, automated workflow.
