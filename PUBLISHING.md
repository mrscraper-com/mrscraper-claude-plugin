# Publishing MrScraper for Claude

Use this checklist for a public MrScraper Claude plugin release.

## Release gate

- [ ] Merge only reviewed changes into `main`.
- [ ] Keep the release version in
      `plugins/mrscraper/.claude-plugin/plugin.json`; do not duplicate it in
      the marketplace entry.
- [ ] Record user-visible changes in `CHANGELOG.md`.
- [ ] Confirm that the repository contains no credentials or private target
      data.
- [ ] Run both strict validations from a clean checkout:

  ```bash
  claude plugin validate . --strict
  claude plugin validate plugins/mrscraper --strict
  ```

- [ ] Confirm the GitHub validation workflow passes.
- [ ] Install the plugin from the public repository in a clean Claude profile,
      complete OAuth, and confirm all seven MCP tools load.
- [ ] Run the smoke-test prompt below.
- [ ] Create the matching Git tag and GitHub release for an explicit semantic
      version.

## Submission details

Keep these values ready for Anthropic's community marketplace form:

| Field | Value |
| --- | --- |
| Plugin name | `mrscraper` |
| Display name | `MrScraper` |
| Repository | `https://github.com/mrscraper-com/mrscraper-claude-plugin` |
| Plugin directory | `plugins/mrscraper` |
| Homepage | `https://docs.mrscraper.com/docs/getting-started/mcp-server` |
| Support | `support@mrscraper.com` |
| Privacy policy | `https://mrscraper.com/privacy-policy` |
| Acceptable use policy | `https://mrscraper.com/acceptable-use-policy` |
| MCP endpoint | `https://mcp.mrscraper.com/mcp` |
| Authentication | OAuth 2.1 browser authorization |

Suggested summary:

> Connect Claude to MrScraper for raw page fetching, managed structured
> extraction, Google discovery, and reusable saved scraper workflows. The
> included skills preserve source responses with a fetch-first workflow before
> adding backend extraction when it is explicitly requested or clearly useful.

The hosted service receives target URLs and tool inputs, including extraction
instructions. Results are returned to Claude for the user's requested task. The
OAuth connection can request `scrape:read`, `scrape:write`, and `account:read`
access. The plugin contains no static credentials.

Smoke-test prompt:

```text
Fetch https://www.scrapethissite.com/pages/simple/ and summarize the page.
```

## Submit to Anthropic

After the release commit is on the public `main` branch, use Anthropic's
[Console submission form](https://platform.claude.com/plugins/submit). A Team
or Enterprise organization owner or directory manager can instead use the
[Claude organization form](https://claude.ai/admin-settings/directory/submissions/plugins/new).

Anthropic reviews third-party plugins for the `claude-community` marketplace.
Approved entries are pinned to a repository commit, and the public catalog may
take until its next nightly sync to show the plugin.
