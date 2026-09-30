# SEO, GEO & AEO Audit: Website SEO Checker and AI Search Readiness (ChatGPT, Perplexity, AI Overviews)

[![Run on Apify](https://img.shields.io/badge/Apify-Run%20the%20Actor-00A67E?logo=apify&logoColor=white)](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef)
![Checks](https://img.shields.io/badge/Checks-45%2B-2ea44f)
![Scores](https://img.shields.io/badge/Scores-SEO%20%7C%20GEO%20%7C%20AEO-1C7ED6)
![Report](https://img.shields.io/badge/Report-shareable%20HTML-8B5CF6)
![Export](https://img.shields.io/badge/Export-JSON%20%7C%20CSV%20%7C%20Excel-F59E0B)

> ### ▶️ [Run the SEO, GEO & AEO Audit on Apify](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef)
> Audit any website for **Google SEO and AI search visibility** in one run: **0 to 100 SEO, GEO and AEO scores** per page, AI crawler and **llms.txt** checks, schema validation, a prioritized fix list and a **shareable HTML report**. Just enter a URL.

**SEO, GEO & AEO Audit** crawls your homepage and key pages and runs 45+ deterministic checks for Google search (SEO), AI search engines like ChatGPT, Perplexity, Gemini and Google AI Overviews (GEO, Generative Engine Optimization), and featured snippets and voice search (AEO, Answer Engine Optimization). It is built for agencies, SEO and content teams, founders and developers. This repository documents the Apify Actor and gives working Python, JavaScript and cURL examples for calling it through the API.

- **Run it in the browser:** [fayoussef/seo-geo-aeo-audit on Apify](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/seo-geo-aeo-audit](https://automationbyexperts.com/apify/seo-geo-aeo-audit)
- **Actor ID for the API:** `fayoussef/seo-geo-aeo-audit`

## What the SEO, GEO & AEO audit checks

- **SEO (Google)**: title and meta description, H1 and heading hierarchy, canonical, noindex traps, mobile viewport, image alt text, internal links, Open Graph, content depth, HTTPS, sitemap.xml, clean URLs.
- **GEO (AI search engines)**: AI crawler access in robots.txt (GPTBot, ClaudeBot, PerplexityBot, Google-Extended and 10+ more), llms.txt and llms-full.txt, JSON-LD, Organization and author schema, E-E-A-T signals, server-side rendering, freshness.
- **AEO (answer engines and voice)**: FAQPage and HowTo schema, question headings, 40 to 60 word direct answers, list and table snippets, BreadcrumbList, Speakable, local NAP.
- **A prioritized fix list** per page and for the whole site.
- **A client-ready HTML report** you can share with a link.

## Output: what you get

One dataset row per audited page, plus a site summary and an HTML report in the key-value store:

| Field | Description |
|---|---|
| `url` | Audited page |
| `overallScore` / `grade` | Overall 0 to 100 score and letter grade |
| `seoScore` / `geoScore` / `aeoScore` | 0 to 100 scores |
| `issues` / `passedChecks` / `criticalCount` | Failed and passed checks, with details |
| `topIssues` | Prioritized list of what to fix |
| `schemaTypes` / `questionHeadings` / `wordCount` | Structured data, question headings, content depth |
| `SUMMARY` | Site-wide scores and top issues (key-value store) |
| `REPORT` | Shareable HTML report (key-value store) |

## Input

Only the website URL is required:

| Field | What it does |
|---|---|
| `websiteUrl` | The site to audit, e.g. `https://yourdomain.com` |
| `maxPages` | Number of pages to audit (default 10) |
| `includeHtmlReport` | Generate the shareable HTML report |

## Use cases

- **Agencies and freelancers**: client and prospect audit reports in minutes.
- **SEO and content teams**: weekly SEO, GEO and AEO scores to catch regressions.
- **Founders and marketers**: check whether ChatGPT, Perplexity and Claude can see your site.
- **Lead generation**: audit prospect websites in bulk through the API.
- **AI agents**: let an agent audit sites through the Apify MCP server.

Ready-made examples you can run in one click:

- [Audit a website for AI search readiness](https://apify.com/fayoussef/seo-geo-aeo-audit/examples/ai-search-readiness-audit?fpr=youssef): Crawls the homepage and the 25 most important pages, runs 45 plus checks and scores the site 0 to 100 for classic SEO, GEO (visibility in ChatGPT, Perplexity and Gemini answers) and AEO (featured snippets). Returns a prioritised issue list and a self contained HTML report.

## Quick start

### 1. In the browser (no code)

1. Open the Actor on Apify and click **Try for free**.
2. Paste your website URL and optionally set **Pages to audit**.
3. Click **Start**, then open the **Output** tab for scores and the **REPORT** for the HTML report.

### 2. Through the API

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

#### Python

```bash
pip install apify-client
python examples/python/run_actor.py
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("fayoussef/seo-geo-aeo-audit").call(run_input={'websiteUrl': 'https://books.toscrape.com', 'maxPages': 25, 'includeHtmlReport': True})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)
```

#### JavaScript / Node.js

```bash
npm install apify-client
node examples/javascript/run_actor.mjs
```

```javascript
import { ApifyClient } from "apify-client";

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor("fayoussef/seo-geo-aeo-audit").call({
    "websiteUrl": "https://books.toscrape.com",
    "maxPages": 25,
    "includeHtmlReport": true
});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items);
```

#### cURL (plain HTTP)

Runs the Actor and returns the dataset items in one synchronous call:

```bash
curl -X POST "https://api.apify.com/v2/acts/fayoussef~seo-geo-aeo-audit/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d @input.json
```

Synchronous calls time out after 300 seconds. For larger runs use the client libraries above, or start the run with `POST /v2/acts/fayoussef~seo-geo-aeo-audit/runs` and read the dataset when it finishes.

## Sample output

One record, from [`sample-output.json`](sample-output.json). Export the full dataset as JSON, CSV, Excel or HTML from the Apify Console, or read it through the API as shown above.

```json
{
  "url": "https://yourdomain.com/",
  "pageTitle": "Your Domain - Home",
  "grade": "B",
  "overallScore": 74,
  "seoScore": 82,
  "geoScore": 68,
  "aeoScore": 61,
  "issuesFound": 9,
  "criticalCount": 1,
  "topIssues": [
    "robots.txt blocks AI crawlers: GPTBot, PerplexityBot - the site cannot be cited by those AI engines.",
    "No FAQPage schema - missing eligibility for FAQ rich results and AI answer extraction."
  ],
  "schemaTypes": [
    "Organization",
    "WebSite"
  ],
  "wordCount": 640
}
```

## Integrations and automation

- **Schedule it** weekly to track SEO, GEO and AEO scores over time.
- **Send results** to Google Sheets, Airtable, Slack, a webhook, Make, Zapier or n8n with Apify integrations.
- **Use it from AI agents** through the Apify MCP server.

## FAQ

### What is GEO (Generative Engine Optimization)?
Optimizing a website so AI search engines like ChatGPT, Perplexity, Gemini and Google AI Overviews can crawl, understand and cite it.

### What is AEO (Answer Engine Optimization)?
Optimizing content to be picked as the direct answer in featured snippets, voice assistants and answer boxes.

### How do I check if ChatGPT and Perplexity can crawl my site?
Run the audit: the GEO section checks robots.txt for GPTBot, ClaudeBot, PerplexityBot, Google-Extended and more, plus llms.txt and server-side rendering.

### Does it check llms.txt?
Yes, both llms.txt and llms-full.txt.

### Do I need an API key?
No. Just enter a URL.

### Can I audit many websites through the API?
Yes. Call the Actor once per site from your own code or an automation tool.

### Can I share the report with a client?
Yes. The HTML report in the key-value store is client-ready.

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## Related tools by AutomationByExperts

- [Bulk AI Image Generator: Nano Banana & GPT Image](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner: ChatGPT, Claude & Gemini in Bulk](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader.ca Scraper: Canada Car Listings, VIN & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Real Estate Listings](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Phone Numbers & Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [Wallapop Scraper: Spain, France, Italy, Portugal & UK](https://github.com/automationbyexperts/wallapop-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom tool: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
