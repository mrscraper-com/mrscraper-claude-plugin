# Changelog

All notable changes to the MrScraper Claude plugin are documented here. The
project follows [Semantic Versioning](https://semver.org/).

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
