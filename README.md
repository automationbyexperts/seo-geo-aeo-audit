# SEO, GEO & AEO Audit: AI Search Readiness Checker

Audit any website for Google SEO and AI search visibility in one run. Get 0-100 SEO, GEO & AEO scores per page, AI-crawler & llms.txt checks, schema validation, and a prioritized fix list with a shareable HTML report. No API keys needed - just enter a URL.

This repo shows how to call the [SEO, GEO & AEO Audit: AI Search Readiness Checker](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef) Apify Actor from your own code: a Python and a JavaScript example, the input they send, and a sample of the output. Everything runs in the Apify cloud, so there is nothing to host, scale or maintain on your side.

- **Run it in the browser:** [fayoussef/seo-geo-aeo-audit on Apify](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef)
- **Guide and docs:** [automationbyexperts.com/apify/seo-geo-aeo-audit](https://automationbyexperts.com/apify/seo-geo-aeo-audit)
- **Actor ID for the API:** `fayoussef/seo-geo-aeo-audit`

## Use cases

- [Audit a website for AI search readiness](https://apify.com/fayoussef/seo-geo-aeo-audit/examples/ai-search-readiness-audit?fpr=youssef): Crawls the homepage and the 25 most important pages, runs 45 plus checks and scores the site 0 to 100 for classic SEO, GEO (visibility in ChatGPT, Perplexity and Gemini answers) and AEO (featured snippets). Returns a prioritised issue list and a self contained HTML report.
- [Run a quick 5 page SEO check on a small business site](https://apify.com/fayoussef/seo-geo-aeo-audit/examples/quick-5-page-seo-check?fpr=youssef): A fast first look: the homepage plus the four key pages the Actor discovers on its own, scored for SEO, AI search visibility and answer engine readiness. Fits inside the free plan limit, so it is the right size for a lead magnet or a first call with a client.
- [Full 100 page SEO and GEO audit for a content site](https://apify.com/fayoussef/seo-geo-aeo-audit/examples/full-site-seo-geo-audit-100-pages?fpr=youssef): Audits up to 100 pages of a blog, docs or ecommerce site and returns every issue per page, from blocked AI crawlers and JavaScript only content to missing schema, thin titles and slow pages. Use the issues view to hand your developer a to do list sorted by impact.

## Quick start

1. Create a free [Apify account](https://console.apify.com/sign-up?fpr=youssef) and copy your API token from [Settings > Integrations](https://console.apify.com/settings/integrations).
2. Set it as an environment variable: `export APIFY_TOKEN=...` (PowerShell: `$env:APIFY_TOKEN="..."`).
3. Edit [`input.json`](input.json) and run one of the examples below.

### Python

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

### JavaScript / Node.js

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

### cURL (plain HTTP)

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

## Pricing

Pay per use on Apify: you are charged per event (results produced), with no subscription to this Actor. The current rate is shown on the [Actor's Store page](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef). Free-plan runs are capped; an [Apify plan](https://apify.com/pricing?fpr=youssef) unlocks full runs.

## More Actors by AutomationByExperts

- [Bulk AI Image Generator (NO API KEY)](https://github.com/automationbyexperts/bulk-ai-image-generator)
- [Bulk LLM Runner GPT, Claude, Perplexity, Kimi (No API Key)](https://github.com/automationbyexperts/bulk-llm-runner)
- [AutoTrader Canada Car Scraper: Prices, VIN, Mileage & Dealers](https://github.com/automationbyexperts/autotrader-canada-scraper)
- [Spitogatos.gr Scraper: Greek Property Listings & Agent Phones](https://github.com/automationbyexperts/spitogatos-scraper)
- [Canada411 Scraper: Business Phones, Addresses](https://github.com/automationbyexperts/canada411-scraper)
- [wallapop Scraper (Spain,Italy,Portugal)](https://github.com/automationbyexperts/wallapop-scraper)
- [Full catalog of our web scraping APIs](https://github.com/automationbyexperts/web-scraping-apis)

## Support

Questions, bugs or a custom scraper: open an issue here, use the Issues tab on the [Apify page](https://apify.com/fayoussef/seo-geo-aeo-audit?fpr=youssef), or email youssefarhan24@gmail.com.

## License

The example code in this repo is MIT licensed. The Actor itself runs on Apify under its own terms.
