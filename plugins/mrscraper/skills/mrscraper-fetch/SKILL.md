---
name: mrscraper-fetch
description: |
  Fetch HTML from a known public URL with MrScraper, with optional browser rendering, real-device Super Mode, locale routing, selector waits, homepage navigation, resource blocking, retries, token limits, and page-load timeouts. Use when the user wants to read, summarize, cite, inspect, archive, or flexibly analyze a page. Use mrscraper-scrape for backend LLM extraction of defined fields or structured records, and mrscraper-serp when no target URL is known.
---

# Fetch Page Content with MrScraper MCP

Use the fetch tool supplied by the MrScraper MCP server when the user already
has a URL and needs that page's response. Use
[mrscraper](../mrscraper/SKILL.md) for connection and authentication checks,
saved runs, account status, or broader routing.

## Page Retrieval Context

fetch calls MrScraper's
[page-fetching service](https://docs.mrscraper.com/docs/features/unblocker) once.
Browser rendering executes page JavaScript, locale routing selects a
geo-specific country, selector waits allow delayed content to appear, and
homepage navigation establishes a normal navigation path before loading the
target.

Page-loading controls can help render a site that does not work with a basic request.

Start with the URL alone and add only the controls the target needs. Plan-token
usage is based on runtime and bandwidth: one token per 30 seconds and one token
per 0.2 MB, rounded up per component. Resource blocking can reduce bandwidth
for text-focused pages. Retries stop when the request succeeds, max_retries is
reached, or the running token total reaches token_cap. The initial request
always runs even when it exceeds that cap. See the
[Token Plan](https://docs.mrscraper.com/docs/getting-started/api-token) for the
maintained calculation.

## Step 1 — Define the Outcome

Confirm the target URL and what the user wants:

- Read, summarize, cite, or inspect the page.
- Check whether specific text appears.
- Archive the response.
- Load JavaScript-rendered or geo-sensitive content.

Use [mrscraper-scrape](../mrscraper-scrape/SKILL.md) when the requested outcome
needs backend extraction of a structured record or set of fields. Use
[mrscraper-serp](../mrscraper-serp/SKILL.md) when discovery must happen first.

## Step 2 — Run the Fetch

The client may namespace the tool name; select fetch from the MrScraper MCP
provider. Start with one call containing only the required URL:

    {
      "url": "https://example.com"
    }

The result is available in MCP structuredContent and as formatted JSON text:

    {
      "status_code": 200,
      "data": "<html>...</html>",
      "headers": {
        "content-type": "text/html"
      }
    }

Prefer structuredContent. Check isError, error, and status_code before using
data. Non-JSON page bodies are preserved exactly.

## Step 3 — Choose Page-Loading Options

Use browser rendering when the page depends on JavaScript:

    {
      "url": "https://example.com/products",
      "browser_rendering": true
    }

If ordinary browser rendering still cannot load the page, route it through a
real device with Super Mode:

    {
      "url": "https://example.com/products",
      "browser_rendering": true,
      "super_mode": true
    }

Use super_mode only after ordinary browser rendering fails. It requires
browser_rendering=true.

Wait for delayed content with a CSS selector:

    {
      "url": "https://example.com/products",
      "browser_rendering": true,
      "wait_for_selector": ".product-card"
    }

Use geographic routing or homepage navigation when the target requires it:

    {
      "url": "https://example.com/product",
      "browser_rendering": true,
      "geo_code": "ID",
      "home_page": true
    }

Use geographic routing for geo-specific content.

Bound resource use for a browser-rendered page:

    {
      "url": "https://example.com",
      "browser_rendering": true,
      "block_resources": true,
      "max_retries": 3,
      "token_cap": 10000,
      "timeout": 60
    }

### Parameters

| MCP input | Default | Request mapping | Use |
| --- | --- | --- | --- |
| url | required | Query url | Absolute HTTP or HTTPS target URL. |
| browser_rendering | false | Query browserRendering | Execute page JavaScript. |
| super_mode | false | Query super | Route browser rendering through a real device; requires browser_rendering=true. |
| geo_code | omitted | Query geoCode | Route through an ISO 3166-1 alpha-2 country. |
| wait_for_selector | omitted | Query waitForSelector | Wait for a CSS selector; requires browser_rendering=true. |
| home_page | false | Query homePage | Visit the site root before the target page. |
| block_resources | false | Query blockResources | Block nonessential resources during loading. |
| max_retries | 3 | Query maxRetries | Maximum retries after failure; zero disables retries. |
| token_cap | omitted | Query tokenCap | Retry token budget; the initial request still runs. |
| timeout | 30 | Query timeout | Page-load timeout in seconds; transport receives another 30 seconds. |

Authentication is handled by the MCP client's OAuth 2.1 connection and is
never a tool input.

## Step 4 — Inspect and Retry Deliberately

Start with the simplest call that can load the page. If the response is
incomplete or missing dynamic content:

1. Inspect the initial response.
2. Retry once with browser_rendering=true when JavaScript is relevant.
3. Add super_mode only when ordinary browser rendering still fails.
4. Add wait_for_selector, geo_code, or home_page only when the target requires
   that behavior.
5. Inspect the revised result before considering another retry.

Do not repeat identical calls. Treat wait_for_selector as a CSS selector, not a
duration. Browser rendering loads a page; it does not click controls, submit
forms, or provide an authenticated interactive browser session.

## Step 5 — Deliver the Result

Answer the user's request from data. Keep the full envelope when headers or
diagnostics matter. When the user requests an archive, save the successful
response or its data value with the environment's local file-writing
capability; fetch itself has no output-path input.
