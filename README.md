# AgentToolWorks MCP servers

Remote [Model Context Protocol](https://modelcontextprotocol.io) servers that AI agents call mid-task, billed per call from one prepaid credit balance. Operated by ECOM FR LLC. Website: [agenttoolworks.com](https://agenttoolworks.com).

This repository holds the public registry manifests (`server.json`) for each server. The servers are hosted; there is nothing to install or run locally.

| Server | Endpoint | What it does |
|---|---|---|
| [VerifyDesk](https://agenttoolworks.com/servers/verifydesk) | `https://verifydesk.agenttoolworks.com/mcp` | Company lookup in the French registry, EU VAT validation (VIES), offline IBAN validation, sanctions screening against the OFAC and UN lists |
| [JobsRadar](https://agenttoolworks.com/servers/jobsradar) | `https://jobsradar.agenttoolworks.com/mcp` | Job search across Greenhouse, Lever, Ashby, SmartRecruiters, Personio and Pinpoint company boards in one call, deduplicated and normalized (Workable too in the [Apify Actor](https://apify.com/agenttoolworks/jobsradar-multi-board-job-search)) |
| [InvoiceForge](https://agenttoolworks.com/servers/invoiceforge) | `https://invoiceforge.agenttoolworks.com/mcp` | Generate, validate and read EN 16931 and Peppol BIS Billing 3.0 e-invoices (UBL and CII) |
| [Store Catalog](https://agenttoolworks.com/scrapers/shopify-woocommerce) | `https://storecatalog.agenttoolworks.com/mcp` | Read any Shopify or WooCommerce store: list products a page at a time, search by keyword, one product in full with variants, barcodes, stock and weights |

## Connect

1. Get a key with 100 free credits, no card: [agenttoolworks.com/signup](https://agenttoolworks.com/signup). One key works on every server.
2. Add a server to your client. Claude Code:

```bash
claude mcp add --transport http verifydesk \
  https://verifydesk.agenttoolworks.com/mcp \
  --header "Authorization: Bearer atw_live_your_key"
```

Cursor, Windsurf, VS Code and Claude Desktop each use a slightly different config shape; the exact snippet for each is in the [docs](https://agenttoolworks.com/docs).

## Tools and prices

1 credit = $0.01 at the Starter rate. A call that fails on our side is billed zero. `get_usage` is free on every server.

| Server | Tool | Credits |
|---|---|---|
| VerifyDesk | `verify_company`, `screen_sanctions`, `enrich_company` | 1 |
| VerifyDesk | `verify_vat`, `validate_iban` | 0.2 |
| JobsRadar | `search_jobs`, `get_company_jobs` | 1 |
| JobsRadar | `list_supported_companies` | 0.2 |
| InvoiceForge | `generate_invoice`, `validate_invoice`, `extract_invoice` | 1 |
| InvoiceForge | `describe_coverage` | 0.2 |
| Store Catalog | `list_products`, `get_product`, `search_products` | 1 |
| Store Catalog | `inspect_store` | 0.2 |

Prepaid packs: $10 for 1,000 credits, $45 for 5,000, $80 for 10,000. No subscription, credits never expire. Full [pricing](https://agenttoolworks.com/pricing).

## Also on the Apify Store

Two of our data products also run as Apify Actors (the Store Catalog readers are the same code as its MCP server), paid per result through Apify, no AgentToolWorks account needed. AI agents can call them through [Apify's hosted MCP server](https://docs.apify.com/platform/integrations/mcp).

| Actor | What it does | Price |
|---|---|---|
| [Shopify & WooCommerce Scraper and Price Tracker](https://apify.com/agenttoolworks/shopify-woocommerce-scraper) | Every product of any Shopify or WooCommerce store: variants, SKUs, barcodes, stock, weights, images. Tracks price drops, restocks, new and removed products between runs. [More](https://agenttoolworks.com/scrapers/shopify-woocommerce) | $1.50 per 1,000 products, $0.005 per change |
| [Job Scraper for Greenhouse, Lever, Ashby & Workable (JobsRadar)](https://apify.com/agenttoolworks/jobsradar-multi-board-job-search) | The JobsRadar search as an Actor, Workable included | $0.90 per 1,000 postings |

MCP clients can load either one with `https://mcp.apify.com?tools=agenttoolworks/shopify-woocommerce-scraper` (an Apify token is required).

## Reliability

Every server is measured daily against production by an agent scenario suite, and the results are published as measured, including degraded runs: [agenttoolworks.com/status](https://agenttoolworks.com/status).

## Data sources

Official public sources only, listed per tool on each server page. Sanctions screening is a due diligence signal, not a legal determination. InvoiceForge checks the rules it lists and does not transmit invoices; it is not an accredited e-invoicing platform.

## Support

[support@agenttoolworks.com](mailto:support@agenttoolworks.com). [Terms](https://agenttoolworks.com/terms), [privacy](https://agenttoolworks.com/privacy), [refunds](https://agenttoolworks.com/refund).
