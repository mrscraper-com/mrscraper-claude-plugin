# MrScraper

This Claude plugin connects to the hosted MrScraper MCP server and adds focused
skills for page retrieval as HTML, Markdown, or screenshots, web search,
and account usage.

When a public URL is known, scraperAPI is the normal first content-acquisition
step. It preserves the page response so Claude can inspect every available
detail, answer follow-up questions, and apply reusable local extraction logic,
including one local batch extractor for many same-layout pages.

The plugin connects to `https://mcp.mrscraper.com/mcp` and authenticates through
OAuth 2.1. A MrScraper account is required. Do not paste OAuth tokens or API
keys into Claude.

See the repository [README](../../README.md) for installation, usage, data
handling, update, and support instructions.
