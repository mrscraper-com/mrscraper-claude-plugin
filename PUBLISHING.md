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

Keep these values ready for the developer portal:

| Field | Value |
| --- | --- |
| Plugin name | `mrscraper` |
| Display name | `MrScraper` |
| Repository | `https://github.com/mrscraper-com/mrscraper-claude-plugin` |
| Plugin path | `plugins/mrscraper` |
| Homepage | `https://docs.mrscraper.com/docs/getting-started/mcp-server` |
| Support | `support@mrscraper.com` |
| Privacy policy | `https://mrscraper.com/privacy-policy` |
| Acceptable use policy | `https://mrscraper.com/acceptable-use-policy` |
| MCP endpoint | `https://mcp.mrscraper.com/mcp` |
| Authentication | OAuth 2.1 with dynamic client registration and client ID metadata documents |
| Icon | `plugins/mrscraper/assets/mrscraper-plugin-logo.png` (512×512 PNG) |

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

Anthropic's directory and its `claude-plugins-official` and `claude-community`
marketplaces take submissions only through the
[developer portal](https://claude.ai/directory/manage), launched on
2026-09-25. The earlier Console form (`platform.claude.com/plugins/submit`) is
[no longer supported](https://claude.com/docs/directory/publish#move-an-earlier-submission-to-the-developer-portal),
and pull requests to `anthropics/claude-plugins-community` are closed
automatically. Submitting requires a paid claude.ai plan: on Team, an Owner;
on Enterprise, an Owner or a member with the Directory permission.

1. Retire any Console submission. In
   [Plugin submissions](https://platform.claude.com/plugins/submissions),
   select **Withdraw**; if there is no **Withdraw** button, email
   `directory@anthropic.com` to have it moved to the portal. Until then, the
   portal can refuse this repository and folder with **Already submitted by
   another organization**.
2. Submit `https://mcp.mrscraper.com/mcp` as an **MCP connector**. Connector
   submissions are scanned automatically and listed as Community connectors
   by default. The server ships MCP App widgets, so prepare 3–5 PNG carousel
   screenshots at least 1000px wide, cropped to the widget, with each prompt
   supplied separately. Reviewers also need credentials for a populated test
   account. See
   [Submit a connector](https://claude.com/docs/connectors/building/submission).
3. From the same organization, submit a **Plugin bundle**. Connect a GitHub
   account that can push to this repository, enter the repository and plugin
   path above, select **Validate**, and fix every **Blocking** finding. Keep
   the GitHub push webhook; setting it up needs repository admin access. See
   [Submit your plugin](https://claude.com/docs/plugins/submit).
4. Pair the connector and plugin listings.
5. Every new plugin listing gets a human review. When a version passes, select
   **Publish** on the plugin's page; by default, that asks an Anthropic
   reviewer to publish it. The plugin is installable only once its status is
   **Published**, not **Approved**. See
   [Track your directory submission](https://claude.com/docs/directory/submission-status).

For a stuck plugin, select **Get help** or **Contact Anthropic** in the plugin's
menu in the portal, or email `directory@anthropic.com`. For the connector,
email `mcp-review@anthropic.com`.

The `claude-community` mirror on GitHub syncs nightly and pins each entry to a
commit, so Claude Code's catalog can lag the directory. Until the listing is
live, users can install from this repository's own marketplace, which
Anthropic doesn't review; see [README.md](README.md#install).
