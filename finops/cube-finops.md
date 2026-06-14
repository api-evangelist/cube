# Cube FinOps

## Cost Model

Cube Cloud pricing is developer-seat-based with per-tier flat monthly rates.
There are no per-query or per-GB charges on paid tiers (Starter and above),
making cost predictable at scale. The Free tier caps usage at 1,000 daily
requests at no charge.

## Cost Drivers

| Driver                     | Notes                                                         |
|----------------------------|---------------------------------------------------------------|
| Developer seats            | Billed per developer on Starter ($40/mo) and Premium ($80/mo)|
| Viewer / Explorer roles    | Available on Premium and above; separate seat counts apply    |
| Production deployment      | Compute costs included in Starter+ plans                      |
| Cube Store caching         | Included in Starter+; reduces downstream warehouse query costs|
| BYOC (Enterprise)          | Customer pays cloud infrastructure; Cube charges license only |

## Cost Optimization Strategies

### Pre-aggregations
Define pre-aggregations in the semantic layer so Cube materializes expensive
warehouse queries into Cube Store. Repeated dashboard or API requests hit the
cache rather than the warehouse, reducing both latency and warehouse spend.

### Query Caching
Cube's in-memory and Cube Store caches serve repeated identical queries without
issuing new warehouse SQL. Enable aggressive cache TTLs for dimensions that
change infrequently.

### Right-sizing Seats
Only developers who author or deploy Cube models require Developer seats.
Read-only consumers (dashboards, embedded apps) may be served under Explorer or
Viewer roles on Premium+, which are typically lower-cost than full Developer seats.

### Self-Hosting for Variable Workloads
For workloads with spiky or unpredictable query volumes, self-hosting Cube Core
on auto-scaling infrastructure can reduce cost compared to cloud-tier per-seat
pricing. Operators trade managed operations for infrastructure flexibility.

### Monitor Request Volume on Free Tier
The Free tier's 1,000 daily request cap can be exhausted quickly by dashboard
auto-refresh or embedded analytics. Monitor usage in the Cube Cloud observability
panel and upgrade before limits impact end-users.

## Enterprise Procurement

Enterprise deals are custom-negotiated and may include:
- Volume discounts on Developer seats
- Dedicated single-tenant deployments (BYOC)
- Multi-year contract pricing
- Bring Your Own LLM to avoid third-party AI inference costs

Contact Cube sales at https://cube.dev/contact for enterprise quotes.

## References

- [Cube Pricing](https://cube.dev/pricing)
- [Cube Store (Caching)](https://cube.dev/docs/product/caching)
- [Pre-aggregations](https://cube.dev/docs/product/caching/using-pre-aggregations)
