# Cube GraphQL API

Cube exposes a GraphQL API that sits on top of its semantic layer, allowing front-end applications and embedded analytics tools to query measures, dimensions, and time dimensions defined across any connected SQL database or data warehouse. The schema is dynamically generated per deployment based on the cubes (data models) defined by the user, so every Cube instance presents its own cube-specific types alongside the fixed base types (filters, ordering, `TimeDimension`, and the root `cube` query).

The API supports filtering with `FloatFilter`, `StringFilter`, and `DateTimeFilter` input types, multi-level `AND`/`OR` boolean logic, time granularity (`second`, `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year`), pagination (`limit`/`offset`), timezone control, and query caching hints. It does **not** support WebSocket transport, subscriptions, segments, compare date range queries, or data model metadata queries.

**Endpoint:** `https://<your-cube-deployment>/graphql`

In Cube Cloud, find your specific endpoint by navigating to **Overview → API credentials → GraphQL API**.

**Authentication:** Requests must include a valid API token in the `Authorization` header as `Authorization: Bearer <CUBE_API_TOKEN>`. Tokens are issued from the Cube Cloud dashboard or configured via the `CUBEJS_API_SECRET` environment variable in self-hosted deployments. The API is enabled by default and secured using API scopes and CORS; it can be disabled by removing the `graphql` scope from `CUBEJS_DEFAULT_API_SCOPES`.

**Documentation:** https://docs.cube.dev/reference/core-data-apis/graphql-api

**References:**
- Documentation: https://docs.cube.dev/reference/core-data-apis/graphql-api
- GitHub: https://github.com/cube-js/cube/blob/master/packages/cubejs-api-gateway/src/graphql.ts
