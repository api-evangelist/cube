# Cube

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Cube is a semantic layer and headless BI platform that sits between your data
warehouse and any downstream consumer — BI tools, front-end applications, AI
agents, or embedded analytics products. Engineers define metrics, dimensions,
joins, and access rules once in code; Cube exposes them through SQL, REST,
GraphQL, and MDX APIs simultaneously.

## APIs

| API | Endpoint | Description |
|-----|----------|-------------|
| GraphQL API | `/graphql` | Query measures, dimensions, and segments via GraphQL over HTTP |
| REST API | `/cubejs-api/v1` | JSON-based query API with load, meta, and SQL endpoints |
| SQL API | Port `15432` | PostgreSQL-wire-compatible interface for BI tools |
| MDX API | `/mdx` | MDX protocol for Excel and Power BI (Enterprise) |

## Resources

- **Website:** https://cube.dev
- **Documentation:** https://cube.dev/docs
- **GitHub:** https://github.com/cube-js
- **LinkedIn:** https://www.linkedin.com/company/cube-dev
- **Pricing:** https://cube.dev/pricing

## Plans

See [plans/cube-plans.md](plans/cube-plans.md) for a breakdown of Free, Starter,
Premium, and Enterprise tiers.

## Rate Limits

See [rate-limits/cube-rate-limits.md](rate-limits/cube-rate-limits.md) for
per-plan quota details and concurrency notes.

## FinOps

See [finops/cube-finops.md](finops/cube-finops.md) for cost drivers and
optimization strategies.

## GraphQL API Notes

See [graphql/cube-graphql.md](graphql/cube-graphql.md) for endpoint details,
example queries, and supported operations.

## Maintainer

Kin Lane — kin@apievangelist.com
