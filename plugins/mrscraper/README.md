# MrScraper

This Claude plugin connects to the hosted MrScraper MCP server and adds focused
skills for raw page fetching, managed structured extraction, Google discovery,
saved scraper reruns, stored results, and account usage.

When a public URL is known, fetch is the normal first content-acquisition step.
It preserves the page response so Claude can inspect every available detail,
answer follow-up questions, and apply reusable local extraction logic. Even for
roughly 100 same-layout pages, concurrent fetches followed by one local batch
extractor can be faster and more complete than repeating backend-LLM extraction
for every page. Use scrape when managed extraction is explicitly requested or
still offers a clear benefit after the source and output schema are understood.

The plugin connects to `https://mcp.mrscraper.com/mcp` and authenticates through
OAuth 2.1. A MrScraper account is required. Do not paste OAuth tokens or API
keys into Claude.

See the repository [README](../../README.md) for installation, usage, data
handling, update, and support instructions.
