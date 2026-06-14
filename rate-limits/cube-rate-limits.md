# Cube Rate Limits

## Cube Cloud

Cube Cloud enforces query limits that vary by plan tier. Rate limits are applied
per deployment and reset on a daily basis unless otherwise noted.

| Plan       | Daily Request Limit | Notes                                  |
|------------|---------------------|----------------------------------------|
| Free       | 1,000 requests/day  | Hard limit; queries fail beyond quota  |
| Starter    | Extended limit      | Higher quota; exact number per account |
| Premium    | Unlimited queries   | No enforced daily cap                  |
| Enterprise | Unlimited queries   | No enforced daily cap; SLA-backed      |

## Self-Hosted Cube Core

Cube Core (open-source, self-hosted) has no built-in request-rate limiting from
Cube itself. Operators are responsible for configuring their own rate limiting at
the infrastructure layer (e.g., API gateway, reverse proxy, or load balancer).

## Concurrency

Cube manages query concurrency internally through its query queue. Each Cube
deployment processes queries sequentially per data source connection by default;
increasing `CUBEJS_CONCURRENCY` allows parallel query execution up to the data
source's own limits.

## Pre-aggregation Refresh

Pre-aggregation refresh jobs run on a background scheduler and do not count
against API request quotas but do consume database compute.

## References

- [Cube Pricing](https://cube.dev/pricing)
- [Cube Configuration: Environment Variables](https://cube.dev/docs/reference/configuration/environment-variables)
- [Caching and Pre-aggregations](https://cube.dev/docs/product/caching)
