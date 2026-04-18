# Reed.co.uk Jobs Feed

Extract structured job listings from [reed.co.uk](https://reed.co.uk), the UK's #1 job site. Get salary details, employer profiles, external apply URLs, and 28 structured fields per listing. No proxy needed, no blocking.

**[Reed Scraper - UK’s #1 Job Site on Apify →](https://apify.com/blackfalcondata/reed-scraper?fpr=1h3gvi)**

---

## Key features





**Search with filters** — Search by keyword and location. Filter by job type, work type, posted by, and more.

**Detail enrichment** — Fetch full job descriptions, salary data for each listing.

**Incremental mode** — Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

**Change classification** — Track cross-run repost detection across runs. Build audit trails of how listings evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Description truncation** — Cap description length per listing to control output size and cost.

**Result cap** — Stop after N listings (up to 5.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every listing returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases





**Data pipeline automation**
Integrate with your ETL pipeline to collect structured listings from reed.co.uk on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data from reed.co.uk.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired listings. Perfect for price-tracking, churn analysis, and alerting pipelines.

**Compensation benchmarking**
Aggregate salary ranges across roles, industries, and locations on reed.co.uk to inform pricing decisions, hiring plans, or candidate negotiations.

**AI / LLM training data**
Structured JSON per listing is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "software engineer",
  "location": "London",
  "maxResults": 10,
  "includeDetails": true
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Job search keywords (e.g. 'software engineer', 'nurse'). |
| `location` | string | — | City, region, or postcode (e.g. 'London', 'Manchester', 'EC2R'). |
| `maxResults` | integer | `50` | Maximum total results to return (0 = unlimited). |
| `jobType` | enum | — | `permanent`, `contract`, or `temp`. |
| `workType` | enum | — | `full-time` or `part-time`. |
| `postedBy` | enum | — | `agency` or `employer`. |
| `salaryFrom` | integer | — | Minimum salary (annual £, or hourly if `salaryPerHour` is true). |
| `salaryTo` | integer | — | Maximum salary (annual £, or hourly if `salaryPerHour` is true). |
| `salaryPerHour` | boolean | `false` | Treat salary filters as hourly rates. |
| `graduate` | boolean | `false` | Only show graduate positions. |
| `employerId` | integer | — | Filter by specific Reed employer ID. |
| `includeDetails` | boolean | `true` | Fetch full job details (description, salary type, external URL). |
| `descriptionMaxLength` | integer | `0` | Truncate description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only — optimized for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Only return new/changed jobs since previous run. |
| `stateKey` | string | — | Identifier for the tracked job universe (e.g. 'london-devs'). |

---

## FAQ

**What is Reed.co.uk?**
Reed is the UK's largest job site, listing over 100,000 active roles from recruitment agencies and direct employers across all industries.

**Is this actor free to run?**
You pay per result: $0.01 per run + $0.002 per job listing. No subscription, no monthly fee. The underlying Reed API is free — you only pay for Apify compute.

**How fast is it?**
Detail enrichment runs at 50 concurrent API calls with zero backoff. 1,000 jobs with full detail enrichment takes approximately 2 seconds of API time.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs with the same `stateKey`, only new or changed listings are emitted. Unchanged listings are skipped.

**Can I filter by hourly rate?**
Yes. Set `salaryPerHour: true` and use `salaryFrom`/`salaryTo` as hourly rates (e.g. `salaryFrom: 25` for £25/hour minimum).

**What data is NOT available?**
Remote/hybrid status is not exposed by Reed's API. Contact details (recruiter email/phone) are behind Reed's application wall and cannot be extracted.

---

## Known limitations

- Remote/hybrid status is not available from Reed's API — `isRemote` is always null.
- Contact details (recruiter email, phone) are behind Reed's apply wall and cannot be extracted.
- Reed's API returns 500 for pagination beyond ~100,000 results. For very broad queries, use filters to narrow results.
- Salary data depends on what employers provide — some listings show "Competitive salary" with no numeric values.
- The API key is per-developer, not per-actor. Rate limits (if any) are shared across all uses of the same key.


## Output fields

Every listing returns the same 28-field schema. Missing values are `null` — never omitted.

- `jobId`
- `reedJobId`
- `title`
- `company`
- `employerId`
- `employerProfileId`
- `employerProfileUrl`
- `location`
- `salaryMin`
- `salaryMax`
- `salaryMinYearly`
- `salaryMaxYearly`
- `currency`
- `salaryPeriod`
- `salaryText`
- `employmentType`
- `contractType`
- `isRemote`
- `description`
- `descriptionHtml`
- `url`
- `externalUrl`
- `applicationCount`
- `datePosted`
- `expirationDate`
- `portalUrl`
- `scrapedAt`
- `source`


## Sample output

One object per listing. Here is a real example from a production run:

```json
{
  "jobId": "reed-56448344",
  "reedJobId": 56448344,
  "title": "Software Engineer",
  "company": "Vermillion Analytics",
  "employerId": 676874,
  "employerProfileId": null,
  "employerProfileUrl": null,
  "location": "London",
  "salaryMin": 45000,
  "salaryMax": 65000,
  "salaryMinYearly": 45000,
  "salaryMaxYearly": 65000
}
```

*Truncated — full records contain 28 fields. See Output fields for the complete schema.*


**[Try Reed Scraper - UK’s #1 Job Site now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/reed-scraper?fpr=1h3gvi)**


## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.002 |

See the [actor on Apify](https://apify.com/blackfalcondata/reed-scraper?fpr=1h3gvi) for current pricing.

---

## Related products by Black Falcon Data





- [StepStone Scraper](https://apify.com/blackfalcondata/stepstone-scraper?fpr=1h3gvi) — Job listings from 18 European portals
- [Indeed Job Scraper](https://apify.com/blackfalcondata/indeed-job-scraper?fpr=1h3gvi) — Indeed job listings with salary data
- [Glassdoor Job Scraper](https://apify.com/blackfalcondata/glassdoor-job-scraper?fpr=1h3gvi) — Glassdoor listings with company ratings
- [Arbeitsagentur Scraper](https://apify.com/blackfalcondata/arbeitsagentur-scraper?fpr=1h3gvi) — Germany's official job portal (1M+ listings)
- [SEEK Scraper](https://apify.com/blackfalcondata/seek-scraper?fpr=1h3gvi) — Australia & NZ's largest job board
- [Naukri Scraper](https://apify.com/blackfalcondata/naukri-scraper?fpr=1h3gvi) — India's largest job portal


## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. [Sign up free](https://console.apify.com/sign-up?fpr=1h3gvi) — $5 credit included
2. Open the actor and paste your input
3. Click Start — results download as JSON, CSV, or Excel

Need more volume? [See pricing](https://apify.com/pricing?fpr=1h3gvi).

---


## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---
---

*Last updated: 2026-03-22*
