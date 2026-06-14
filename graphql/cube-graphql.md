# Cube GraphQL API

## Overview

Cube exposes a GraphQL API via the `/graphql` endpoint, enabling data delivery over
HTTP to GraphQL-enabled applications. It provides access to all measures, dimensions,
segments, and filters defined in the Cube semantic layer.

## Endpoint

```
https://<your-cube-deployment>/graphql
```

In Cube Cloud, find your specific endpoint by navigating to **Overview → API credentials → GraphQL API**.

## Authentication

Requests must include a valid API token in the `Authorization` header:

```
Authorization: Bearer <CUBE_API_TOKEN>
```

## Querying

The GraphQL API mirrors the Cube REST query model. The root query field is `cube`,
accepting a `where` filter argument and returning typed result objects for each
cube defined in your semantic layer.

### Example Query

```graphql
{
  cube(
    where: { orders: { status: { equals: "completed" } } }
    limit: 10
    offset: 0
    orderBy: { orders: { createdAt: asc } }
  ) {
    orders {
      count {
        value
      }
      totalAmount {
        value
      }
      createdAt {
        day
      }
    }
  }
}
```

## Supported Operations

- **Measures** — Numeric aggregations defined in the semantic layer (e.g., `count`, `sum`, `avg`)
- **Dimensions** — Attributes to group or filter by (e.g., `status`, `createdAt`)
- **Segments** — Pre-defined filter sets applied as boolean flags
- **Time dimensions** — Date/time fields with granularity options (`day`, `week`, `month`, `quarter`, `year`)

## Granularities for Time Dimensions

| Granularity | Description        |
|-------------|--------------------|
| `second`    | Per-second buckets |
| `minute`    | Per-minute buckets |
| `hour`      | Hourly buckets     |
| `day`       | Daily buckets      |
| `week`      | Weekly buckets     |
| `month`     | Monthly buckets    |
| `quarter`   | Quarterly buckets  |
| `year`      | Yearly buckets     |

## References

- [GraphQL API documentation](https://cube.dev/docs/product/apis-integrations/graphql-api)
- [GraphQL API reference](https://cube.dev/docs/reference/graphql-api)
