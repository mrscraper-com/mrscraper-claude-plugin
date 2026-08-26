# MrScraper for Claude

MrScraper connects Claude to a hosted MCP server for fetching public web pages,
managed structured extraction, Google discovery, saved scraper reruns, stored
results, and account usage. The plugin also includes four focused skills that
help Claude choose the right workflow and preserve raw page content.

## What this plugin adds

- The hosted Streamable HTTP endpoint at `https://mcp.mrscraper.com/mcp`.
- OAuth 2.1 authentication through Claude; no credential is stored in this
  repository.
- A fetch-first workflow that keeps raw page responses available for analysis,
  verification, and follow-up transformations.
- Managed extraction, site mapping, Google SERP discovery, saved reruns, and
  stored-result tools when those capabilities are useful.

## Requirements

- A current version of [Claude Code](https://code.claude.com/docs/en/setup).
- A [MrScraper](https://app.mrscraper.com) account.
- Permission to access and process the target content.

## Install

Add this repository as a marketplace and install the plugin:

```bash
claude plugin marketplace add mrscraper-com/mrscraper-claude-plugin
claude plugin install mrscraper@mrscraper-claude
```

In Claude's **Add marketplace** dialog, paste:

```text
mrscraper-com/mrscraper-claude-plugin
```

If the dialog expects a full Git repository URL, use:

```text
https://github.com/mrscraper-com/mrscraper-claude-plugin.git
```

Restart Claude or reload plugins after installation. Open `/mcp` if Claude asks
you to authenticate, then complete the MrScraper OAuth flow in your browser.
Never paste OAuth tokens or API keys into chat.

## Try it

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

The connection should expose these MCP tools:

| Tool | Purpose |
| --- | --- |
| `fetch` | Retrieve and preserve a known page's raw response. |
| `scrape` | Run managed structured extraction or bounded site mapping. |
| `serp` | Discover public pages through Google. |
| `rerun` | Reuse a saved AI or manual scraper configuration. |
| `results` | Browse and filter stored result records. |
| `result` | Retrieve one stored result or poll an asynchronous run. |
| `status` | Inspect subscription usage and request outcomes. |

## Fetch-first routing

When a public URL is already known, the skills direct Claude to fetch it first
and treat the raw response as the source of truth. Claude can read, summarize,
compare, or derive structured output locally without losing details to an
early extraction prompt.

This preference can still be faster for large same-layout sets. For roughly
100 known pages, Claude can safely fetch pages concurrently, retain every raw
response, and apply one reusable local extractor instead of requesting 100
separate backend-LLM extractions. Use `scrape` when managed extraction is
explicitly requested or has a clear benefit after the page structure and
desired schema are understood.

## Data and permissions

The plugin sends MCP tool inputs—including target URLs and extraction
instructions—to MrScraper's hosted service. Page responses and tool results are
then available to Claude for the requested task. Use it only with public or
otherwise authorized content, and follow the target site's requirements.

Review MrScraper's [MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server),
[Privacy Policy](https://mrscraper.com/privacy-policy), and
[Acceptable Use Policy](https://mrscraper.com/acceptable-use-policy) before use.

## Update or remove

```bash
claude plugin marketplace update mrscraper-claude
claude plugin update mrscraper@mrscraper-claude
claude plugin uninstall mrscraper@mrscraper-claude
```

## Support and security

- Product help: [MrScraper MCP documentation](https://docs.mrscraper.com/docs/getting-started/mcp-server)
- Bugs and feature requests: [GitHub Issues](https://github.com/mrscraper-com/mrscraper-claude-plugin/issues)
- Account help: [support@mrscraper.com](mailto:support@mrscraper.com)
- Security reports: see [SECURITY.md](SECURITY.md)

## Development

The repository is both an installable Claude marketplace and the source of the
`mrscraper` plugin:

```text
.claude-plugin/marketplace.json
plugins/mrscraper/
├── .claude-plugin/plugin.json
├── .mcp.json
└── skills/
```

Validate both manifests and all plugin components before a release:

```bash
claude plugin validate . --strict
claude plugin validate plugins/mrscraper --strict
```

The plugin uses semantic versions from its plugin manifest. Bump that version
for every release and record user-visible changes in [CHANGELOG.md](CHANGELOG.md).
Use [PUBLISHING.md](PUBLISHING.md) for the release and Anthropic submission
checklist.

## License

[MIT](LICENSE)
