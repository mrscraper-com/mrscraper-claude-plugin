# MrScraper for Claude

This marketplace packages MrScraper's MCP-oriented skills together with the
hosted MrScraper MCP server for Claude.

## Add the marketplace

Paste this GitHub `owner/repo` value into Claude's **Add marketplace** dialog:

```text
pray-mrscraper/mrscraper-claude-plugin
```

If the dialog specifically expects a Git repository URL, use
`https://github.com/pray-mrscraper/mrscraper-claude-plugin.git`.

From Claude Code CLI, add the marketplace and install the plugin:

```bash
claude plugin marketplace add pray-mrscraper/mrscraper-claude-plugin
claude plugin install mrscraper@mrscraper-claude
```

The plugin connects to `https://mcp.mrscraper.com/mcp`. When prompted, finish
the OAuth authorization flow in your browser. Do not paste OAuth tokens or API
keys into chat.

## Try it

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

The included skills encourage `fetch` as the normal first step when a URL is
known because it preserves the page response for flexible agent-led analysis.
Use `scrape` when you specifically need backend structured extraction,
pagination, schema-shaped output, or a reusable saved scraper.

## Contents

- `plugins/mrscraper/.claude-plugin/plugin.json`: Claude plugin manifest
- `plugins/mrscraper/skills/`: MCP-oriented MrScraper skill pack
- `.claude-plugin/marketplace.json`: repository marketplace catalog

## Development validation

```bash
claude plugin validate . --strict
```

This repository is for marketplace testing before the equivalent packaging is
integrated into the official MrScraper repositories.
