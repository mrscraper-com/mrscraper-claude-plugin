# Changelog

All notable changes to the MrScraper Claude plugin are documented here. The
project follows [Semantic Versioning](https://semver.org/).

## 0.5.0 - 2026-11-24

- Updated the skills for MrScraper MCP server 0.6.0, whose tools take exactly
  the inputs on MrScraper's API documentation pages. The `mrscraper-fetch`
  skill lists each page tool's inputs with the documented descriptions. An
  input left out is not sent, so MrScraper's own default applies; left out,
  `browserRendering` lets MrScraper switch to a browser when a request is
  blocked. The `mrscraper-serp` skill says the same for `country` and
  `numResults`.
- New inputs: `maxAge` on the four page tools reuses a cached result (0, a
  fresh scrape, is sent when it is left out); `screenshot` on `scrapeHtml`
  adds a screenshot; `getScreenshot` also takes a viewport size such as
  `1280x800`; and `scrapeJson` takes `waitForSelector`, `warmStart`, and
  `blockResources` and returns the page HTML unless `html` is false. `timeout`
  goes up to 330 seconds.
- `scrapeMarkdown` returns only Markdown and `getScreenshot` only the
  screenshot: their `html` and `markdown` inputs are gone, and
  `getScreenshot` no longer takes `blockResources`. Every other input that
  the API documentation doesn't list is gone too. `saveResult` is no longer
  an input: the four page tools always save their result to the MrScraper
  dashboard.
- The retry guidance uses `browserRendering`, `waitForSelector`, `timeout`,
  `warmStart`, `geoCode`, `maxRetries`, and `maxAge`.
- The README shows the MCP 0.6.0 tool descriptions.
- Skills are identical to the MrScraper Cursor 0.6.0, Grok 0.5.0, Antigravity
  0.5.0, and OpenCode 0.6.0 plugins.

## 0.4.0 - 2026-11-20

- Rewrote the skills for MrScraper MCP server 0.5.0, which follows the
  MrScraper Integrations Standard and has seven tools: `status`, `scrapeHtml`,
  `scrapeMarkdown`, `getScreenshot`, `scrapeBrand`, `scrapeJson`, and
  `webSearch`. `scraperAPI` is gone; use `scrapeHtml`, `scrapeMarkdown`, or
  `getScreenshot`, and `scrapeBrand` or `scrapeJson` for brand data and JSON
  extraction. `webSearch` now takes `query`, `country`, and `numResults`
  instead of `url`, `region`, `num_results`, and `timeout`, and all tool
  inputs are camelCase. The README and publishing notes list the seven tools.
- Removed the OAuth scope pin from `.mcp.json`, so Claude requests the scopes
  the server advertises: `scrape:read` for the six scraping and search tools
  and `account:read` for `status`. Connections that already hold `scrape:read`
  keep working; `scrape:write` is no longer needed.
- Skills are identical to the MrScraper Cursor 0.5.0, Grok 0.4.0, Antigravity
  0.4.0, and OpenCode 0.5.0 plugins.

## 0.3.0 - 2026-11-02

- Updated the `mrscraper-serp` skill for MrScraper MCP server 0.3.0, which
  moved `webSearch` to MrScraper's new web search endpoint. Results are a
  ranked list (rank, title, url, description, source); `region` sets the
  results' country and the new `num_results` asks for 10 to 100 results. The
  `raw`, `format`, `language`, `page`, and `render_js` options are gone, and
  so is the search results URL example. Skills are identical to the MrScraper
  Cursor 0.4.0, Grok 0.3.0, Antigravity 0.3.0, and OpenCode 0.4.0 plugins.

## 0.2.3 - 2026-10-30

- Reworded search as web search in the plugin and marketplace descriptions,
  READMEs, publishing notes, and skills. The `webSearch` tool is unchanged.
  Skills are identical to the MrScraper Cursor 0.3.2, Grok 0.2.2, Antigravity
  0.2.2, and OpenCode 0.3.2 plugins again.
- Added the ClaudePluginHub badge to the README.

## 0.2.2 - 2026-10-22

- Pinned OAuth to the `scrape:read`, `scrape:write`, and `account:read` scopes.
  The hosted server now requires `scrape:write` for `scraperAPI`. Connections
  made with 0.2.0 or 0.2.1 hold only `scrape:read` and `account:read`, so
  `scraperAPI` returns 403 `insufficient_scope` until the connection is
  authorized again.
- Updated the `mrscraper` skill to name the scope each tool needs.

## 0.2.1 - 2026-10-16

- Added the plugin icon and privacy policy URL to `plugin.json` for the Claude
  directory listing.
- Updated continuous validation to Claude Code 2.1.296, which recognizes those
  fields.

## 0.2.0 - 2026-10-14

- Updated the skills for the hosted MCP server's new tools: `scraperAPI`
  (pages as HTML, Markdown, or screenshots), `webSearch` (Google), and `status`
  (account usage). The `fetch`, `scrape`, `serp`, `rerun`, `results`, and
  `result` tools no longer exist.
- Removed the `mrscraper-scrape` skill; managed extraction, saved reruns, and
  stored results are available in the MrScraper dashboard.
- Pinned OAuth to the `scrape:read` and `account:read` scopes the tools use.

## 0.1.4 - 2026-10-02

- Passed `acknowledged=true` on manual reruns after the user accepts the
  compliance warning, which the MrScraper MCP server now requires.

## 0.1.3 - 2026-09-01

- Pinned the hosted MCP connection to the documented `scrape:read`,
  `scrape:write`, and `account:read` OAuth scopes.
- Restored the required compliance warning before the first manual scraper
  rerun in a conversation.
- Updated continuous validation to Claude Code 2.1.252.

## 0.1.2 - 2026-08-26

- Strengthened fetch-first routing, including reusable local extraction for
  large same-layout page sets.
- Added guidance for fetch and managed extraction execution modes.
- Added saved-rerun controls, exact result filters, and compact result polling.
- Replaced placeholder targets with public Scrape This Site examples.
- Added publication, data-handling, support, and security documentation.
- Moved version ownership exclusively to the plugin manifest.

## 0.1.1 - 2026-08-24

- Moved the hosted MrScraper connection to Claude's native `.mcp.json` plugin
  configuration.

## 0.1.0 - 2026-08-24

- Added the initial MrScraper Claude marketplace, MCP connection, and skill
  pack.
