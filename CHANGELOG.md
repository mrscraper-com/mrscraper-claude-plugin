# Changelog

All notable changes to the MrScraper Claude plugin are documented here. The
project follows [Semantic Versioning](https://semver.org/).

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
- Added guidance for fetch Super Mode and managed extraction execution modes.
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
