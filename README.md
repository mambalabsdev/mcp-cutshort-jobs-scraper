# Cutshort Jobs Scraper MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-cutshort-jobs-scraper/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-cutshort-jobs-scraper) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-cutshort-jobs-scraper%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-cutshort-jobs-scraper&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-cutshort-jobs-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-cutshort-jobs-scraper) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-cutshort-jobs-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-cutshort-jobs-scraper) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-cutshort-jobs-scraper)](https://github.com/mambalabsdev/mcp-cutshort-jobs-scraper/blob/main/LICENSE) [![mcpservers.org](https://img.shields.io/badge/mcpservers.org-listed-blue)](https://mcpservers.org/servers/mambalabsdev/mcp-cutshort-jobs-scraper)

An MCP server for the Mamba Labs Cutshort Jobs Scraper actor on Apify. Cutshort jobs as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes skill or role keywords and Indian cities, or Cutshort URLs, and returns one row per job with title, company, locations, remote type, experience, salary as shown, skills, posted date, and description.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-cutshort-jobs-scraper": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-cutshort-jobs-scraper"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `search_cutshort_jobs` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find Python developer jobs in Bangalore on Cutshort."
- "List remote DevOps jobs on Cutshort with salaries and skills."

## Tool

`search_cutshort_jobs`. One tool. Example arguments:

```json
{
  "keywords": [
    "python"
  ],
  "cities": [
    "Bangalore"
  ],
  "max_jobs_per_search": 20
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `keywords` | array | no | Skill or role keywords, for example python, java, devops, or product management. Each keyword is matched to a Cutshort listing page, and the row says which page it used. From Clay, wrap a column in a one item list. |
| `cities` | array | no | Indian cities, for example Bangalore, Mumbai, Delhi, Hyderabad, Pune, or Chennai. Each keyword runs once per city. Leave empty for all of India. |
| `start_urls` | array | no | Cutshort listing pages (https://cutshort.io/jobs/...) or job pages (https://cutshort.io/job/...). |
| `max_jobs_per_search` | number | no | Jobs to return per keyword and city, 1 to 50. A Cutshort listing page shows its newest 50 jobs. |
| `remote_only` | boolean | no | yes keeps only jobs Cutshort labels remote_only or remote_okay. Jobs left out are not charged. |
| `include_description` | boolean | no | yes (default) adds the full job description as plain text. The price is the same either way. |
| `dedupe` | boolean | no | yes (default) returns a job once per run even when several searches list it. Repeats are not charged. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `job-row`, one job | $0.002 | $0.0019 | $0.0018 | $0.0017 |
| `apify-actor-start`, per run start | $0.005 | $0.005 | $0.005 | $0.005 |

Repeats, filtered jobs, empty searches, summaries, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/cutshort-jobs-scraper](https://apify.com/mambalabs/cutshort-jobs-scraper)

## License

MIT. See [LICENSE](LICENSE).
