# Reed.co.uk Jobs Feed

Extract structured job listings from [reed.co.uk](https://reed.co.uk), the UK's #1 job site. Get salary details, employer profiles, external apply URLs, and 28 structured fields per listing. Powered by Reed's official public API — no proxy needed, no blocking.

**[Run on Apify →](https://apify.com/blackfalcondata/reed-jobs-feed)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, job type (permanent/contract/temp), work type (full-time/part-time), salary range, graduate roles, and specific employers.

📄 **Detail enrichment**

Fetch full job descriptions, salary period (annual/hourly), contract type, employment type, yearly salary normalization, and external apply URLs.

🔄 **Incremental mode**

Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control token budgets.

💰 **Structured salary data**

Min/max salary, yearly normalization, currency, and salary period extracted as discrete fields — not just a text string.

---

## Use cases

**Job market intelligence**
Track hiring trends across industries, locations, and salary bands. Monitor how many new roles appear daily for specific skills or regions.

**Recruitment pipeline automation**
Feed structured job data into your CRM or ATS. Use incremental mode to only process new listings, reducing API calls and storage.

**Salary benchmarking**
Compare salary ranges across roles, locations, and employers. Yearly normalization lets you compare hourly, daily, and annual rates on equal footing.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

**Academic research**
Study labour market dynamics, skill demand, regional employment patterns, and wage distribution with structured, machine-readable data.

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

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Willhaben Jobs Feed](https://github.com/BlackFalconData-org/willhaben-jobs-feed) | Austria's largest classifieds — jobs with salary |
| [DBA Listings Scraper](https://github.com/BlackFalconData-org/dba-listings-scraper) | Denmark's largest classifieds marketplace |

---

*Last updated: 2026-03-22*
