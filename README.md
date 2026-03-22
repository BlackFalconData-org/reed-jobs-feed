# Reed.co.uk Jobs Feed — UK Job Listings with Salary & Contact

Extract structured data from [reed.co.uk](https://reed.co.uk) — structured job listings from reed.co.uk — the UK's #1 job site. Salary details, employer profiles, incremental mode, and MCP-ready output.

**[Run on Apify →](https://apify.com/blackfalcondata/reed-jobs-feed)**

---

## Key features

🔍 **Smart search with filters**

Search by keyword, location, and multiple filters. Smart input resolution ensures you always get results.

📄 **Detail enrichment**

Fetch full job descriptions, salary data, employer profiles, and contact information for each listing.

🔄 **Incremental mode**

Only get new or changed listings since your last run. Content hash per listing — no duplicates, no re-processing.

⚡ **Compact output for AI agents**

Core-fields-only mode optimized for MCP and AI agent workflows. Description truncation to control output size.

---

## Use cases

<!-- WRITE: 4-6 use case paragraphs. Bold the title. 2-3 sentences each. -->

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured data on a schedule. Export to CSV, JSON, or directly to your database.

**Market research**
Monitor listings, track trends, and analyze market dynamics with structured, deduplicated data.

**AI and LLM workflows**
Use compact mode and description truncation to feed data into AI agents, MCP servers, and LLM pipelines without exceeding token budgets.

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
| `query` | string | — | Job search keywords (e.g. 'software engineer', 'nurse', 'marketing manager'). |
| `location` | string | — | City, region, or postcode (e.g. 'London', 'Manchester', 'EC2R'). |
| `maxResults` | integer | `50` | Maximum total results to return (0 = unlimited). |
| `jobType` | enum | — | Filter by contract type. |
| `workType` | enum | — | Filter by hours. |
| `postedBy` | enum | — | Filter by recruiter type. |
| `salaryFrom` | integer | — | Filter: minimum salary (annual £). |
| `salaryTo` | integer | — | Filter: maximum salary (annual £). |
| `salaryPerHour` | boolean | `false` | When true, salary filters are treated as hourly rates instead of annual. |
| `graduate` | boolean | `false` | Only show graduate positions. |
| `employerId` | integer | — | Filter by specific Reed employer ID. |
| `includeDetails` | boolean | `true` | Fetch full job details (description, salary type, external URL). Costs 1 extra API call per job. |
| `descriptionMaxLength` | integer | `0` | Truncate description to N characters. 0 = no truncation. |
| `compact` | boolean | `false` | Core fields only — optimized for AI-agent and MCP workflows. |
| `incrementalMode` | boolean | `false` | Only return new/changed jobs since previous run. Requires a stable stateKey. |
| `stateKey` | string | — | Identifier for the tracked job universe (e.g. 'london-devs'). Different queries should use different keys. |

---

## FAQ

<!-- WRITE: 4-6 Q&A pairs relevant to this product -->

**Is it legal to scrape reed.co.uk?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check the target site's terms of service for your specific use case.

**How does incremental mode work?**
Each listing gets a content hash. On subsequent runs, only new or changed listings are emitted — saving time, compute, and storage.

---

## Known limitations

<!-- WRITE: 4-6 honest limitations -->

- <!-- WRITE: limitation 1 -->
- <!-- WRITE: limitation 2 -->

---

## Related products by Black Falcon Data

| Product | Description |
|:--------|:------------|
| [StepStone Jobs API](https://github.com/BlackFalconData-org/stepstone-jobs-api) | Job listings from 18 European portals |
| [Company Jobs Tracker](https://github.com/BlackFalconData-org/company-jobs-tracker-api) | Track new/removed jobs per company |
| [Indeed Jobs Feed](https://github.com/BlackFalconData-org/indeed-jobs-feed) | Indeed job listings with salary data |
| [Glassdoor Jobs Feed](https://github.com/BlackFalconData-org/glassdoor-jobs-feed) | Glassdoor listings with company ratings |
| [Arbeitsagentur Jobs Feed](https://github.com/BlackFalconData-org/arbeitsagentur-jobs-feed) | Germany's federal job portal (1M+ listings) |
| [Naukri Jobs Feed](https://github.com/BlackFalconData-org/naukri-jobs-feed) | India's largest job portal |
| [Bilbasen Scraper](https://github.com/BlackFalconData-org/bilbasen-scraper) | Denmark's largest car marketplace |

---

*Last updated: 2026 03*
