# Cube

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
