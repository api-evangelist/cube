<!-- fetched 2026-10-13 from https://cube.dev/docs/product/apis-integrations/sql-api by sweep-shape-compat.py; text extracted from the provider's own page -->

Cube Core - Cube Documentation 
 Documentation Index
 Fetch the complete documentation index at: /llms.txt 
 Use this file to discover all available pages before exploring further.
 Skip to main content 
 Cube Documentation home page 
 Search...
 ⌘ K Ask Assistant ⌘ I 
 Demos 
 Changelog 
 Community 
 Get Started 
 Get Started 
 Search... 
 Navigation 
 SQL API 
 Cube Core
 Documentation 
 Admin 
 Embedding 
 Reference 
 Cube Core 
 Recipes 
 API 
 Data Modeling 
 Cubes 
 Views 
 View groups 
 Measures 
 Dimensions 
 Hierarchies 
 Segments 
 Joins 
 Pre-aggregations 
 Access policies 
 Context variables 
 Packages 
 Configuration 
 Environment variables 
 Configuration options 
 Core Data APIs 
 Overview 
 Querying data APIs 
 SQL API 
 Query format in the SQL API 
 Joins in the SQL API 
 Authentication and Authorization 
 SQL API reference 
 REST (JSON) API 
 GraphQL API 
 Embed APIs 
 Overview 
 Chat API 
 Generate Session 
 Dashboard Comments 
 Other APIs 
 Control Plane API 
 Orchestration API 
 Cube Store 
 Cube Store SQL commands 
 CLI 
 Cube CLI 
 JavaScript SDK 
 Javascript sdk 
 React 
 Vue 
 Angular 
 SDK Reference 
 On this page 
 Transport Postgres protocol 
 HTTP protocol 
 Fundamentals 
 Configuration Cube Core 
 Example 
 Cube Cloud 
 Query planning 
 Streaming 
 Session limit 
 Cache control 
 Troubleshooting Can't find rewrite 
 SQL API
 Cube Core
 Connect any Postgres-compatible client or BI tool to Cube using the Postgres-protocol SQL API.
 SQL API 
 The SQL API enables Cube to deliver data over the Postgres-compatible
protocol to a wide range of data visualization tools .
In general, if an application connects to PostgreSQL database,
it can connect to Cube as well. 
 See SQL API reference for the list of supported SQL commands,
functions, and operators. Also, check query format for
details about supported queries. 
 ​ 
 Transport 
 The SQL API supports the following transports: 
 Transport
 Description
 When to use
 Postgres
 Same protocol that is used by the psql utility and other Postgres clients
 Use by default
 HTTP
 JSON-based protocol that is also used by the REST (JSON) API 
 Use when you need to run a SQL API query from an embedded analytics application and REST (JSON) API is not an option
 ​ 
 Postgres protocol 
 You can use the psql utility to connect to the SQL API: 
 # Cube Core 
 PGPASSWORD = password \ 
 psql -h localhost \ 
 -p 15432 \ 
 -U user cube 
 # Cube Cloud 
 PGPASSWORD = password \ 
 psql -h awesome-ecom.sql.gcp-us-central1.cubecloudapp.dev \ 
 -p 5432 \ 
 -U cube awesome-ecom 
 Then, you can run queries in the Postgres dialect, just like the following one: 
 SELECT 
 users.state, 
 users.city, 
 orders.status, 
 MEASURE(orders.count) 
 FROM orders 
 CROSS JOIN users 
 WHERE 
 users.state != 'us-wa' 
 AND orders.created_at BETWEEN '2020-01-01' AND '2021-01-01' 
 GROUP BY 1 , 2 , 3 
 LIMIT 10 ; 
 You can also introspect the data model in a Postgres-native way by querying tables
in information_schema or using backslash
commands : 
 SELECT * 
 FROM information_schema.tables 
 WHERE table_schema = 'public' ; 
 \d 
 ​ 
 HTTP protocol 
 You can use the curl utility to run a SQL API query over the HTTP protocol: 
 curl \ 
 -X POST \ 
 -H "Authorization: TOKEN" \ 
 -H "Content-Type: application/json" \ 
 -d '{"query": "SELECT 123 AS value UNION ALL SELECT 456 AS value UNION ALL SELECT 789 AS value"}' \ 
 http://localhost:4000/cubejs-api/v1/cubesql 
 See the /v1/cubesql endpoint reference for more details. 
 ​ 
 Fundamentals 
 In the SQL API, each cube or view from the data model 
is represented as a table. Measures, dimensions, and segments are represented as
columns in these tables. SQL API can execute regular queries ,
 queries with post-processing , and queries with
pushdown that can reference these tables and columns. 
 Under the hood, the SQL API uses Apache DataFusion as
its query engine. It’s responsible for query planning and execution.
As part of query planning, the SQL API also uses egg (an e-graph term
rewriting library) to analyze incoming SQL queries and find the best
query plan out of a wide variety of possible plans to execute. 
 Overall, query planning is a seamless process.
SQL API does its best to execute a query as a regular query 
or a query with post-processing . If that is not possible,
then the query would be executed as a query with pushdown .
There are trade-offs associated with each query type: 
 Query type
 In-memory cache
 Pre-aggregations
 SQL support
 Regular queries 
 ✅ Used
 ✅ Used
 🟡 Very limited
 Queries with post-processing 
 ✅ Used
 ✅ Used
 🟡 Limited
 Queries with pushdown 
 ✅ Used
 ❌ Not used
 ✅ Extensive
 Read more about Query pushdown in the SQL API in the blog. 
 ​ 
 Configuration 
 ​ 
 Cube Core 
 SQL API is disabled by default. To enable the SQL API, set CUBEJS_PG_SQL_PORT 
to a port number you’d like to connect to with a Postgres-compatible tool. 
 Credential
 Environment variable, etc.
 Host
 Host you’re running Cube at
 Port
 Set via CUBEJS_PG_SQL_PORT 
 User name
 Set via CUBEJS_SQL_USER 
 Password
 Set via CUBEJS_SQL_PASSWORD 
 Database
 Any valid string, e.g., cube 
 You can also use
 checkSqlAuth ,
 canSwitchSqlUser , and CUBEJS_SQL_SUPER_USER 
to configure custom authentication . 
 ​ 
 Example 
 The following Docker Compose file will run Cube with the SQL API enabled on
port 15432, accessible using user as the user name, password as the password,
and any string as the database name: 
 services: 
 cube: 
 image: cubejs/cube:latest 
 ports: 
 - 4000:4000 
 - 15432:15432 
 environment: 
 - CUBEJS_DEV_MODE=true 
 - CUBEJS_API_SECRET=SECRET 
 - CUBEJS_DB_USER=cube 
 - CUBEJS_DB_PASS=12345 
 - CUBEJS_DB_HOST=demo-db-examples.cube.dev 
 - CUBEJS_DB_NAME=ecom 
 - CUBEJS_DB_TYPE=postgres 
 - CUBEJS_PG_SQL_PORT=15432 # SQL API credential 
 - CUBEJS_SQL_USER=user # SQL API credential 
 - CUBEJS_SQL_PASSWORD=password # SQL API credential 
 volumes: 
 - .:/cube/conf 
 After running it with docker compose up , you can finally connect and execute
an example request . 
 Development mode is an authentication bypass. Cube is in development mode when
 CUBEJS_DEV_MODE=true — and also under cubejs dev-server , the cubejs-dev-server 
bin, or the devServer option, which turn it on with the variable unset. It switches
off JWT verification on the REST (JSON) and GraphQL APIs. Playground’s endpoints are
served with no authentication too: anyone who can reach the instance is handed a
ready-to-use API token, can mint others carrying any security context, can read your
data model files, and can overwrite your data model and your .env . With
 CUBEJS_DEV_MODE=true specifically, and no
 CUBEJS_SQL_PASSWORD 
set, the SQL API accepts any credentials as well, allowing arbitrary SQL against
connected data sources. Use it only on a local development machine, never in
production. See
 CUBEJS_DEV_MODE . 
 ​ 
 Cube Cloud 
 SQL API is enabled by default. To find your SQL API endpoint and credentials
in Cube Cloud, go to the Overview page, click API credentials ,
and choose the SQL API tab. 
 By default, the SQL API is enabled on port 5432, the user name is cube , and
a random string is generated for the password. You can customize these with
 CUBEJS_PG_SQL_PORT , CUBEJS_SQL_USER , and CUBEJS_SQL_PASSWORD environment
variables by navigating to  Settings → Configration . 
 ​ 
 Query planning 
 The SQL API executes queries as regular queries , queries with
post-processing , or queries with pushdown . 
 ​ 
 Streaming 
 By default, query results are loaded in a single batch. However, a more effective
 streaming mode can be used for large result sets. To enable it, set the
 CUBESQL_STREAM_MODE 
environment variable to true . 
 When the streaming mode is enabled, the maximum row limit 
does not apply to SQL API queries with an explicit LIMIT clause. This means
you can use a very large LIMIT value to retrieve large result sets. If a query does not include an explicit LIMIT clause,
 CUBEJS_DB_QUERY_DEFAULT_LIMIT 
still applies even in streaming mode. To retrieve large result sets without an
explicit LIMIT , increase CUBEJS_DB_QUERY_DEFAULT_LIMIT as needed. 
 Queries that are not streamed are capped by
 CUBESQL_NON_STREAMING_QUERY_MAX_ROW_LIMIT ,
which defaults to the value of CUBEJS_DB_QUERY_LIMIT . It also acts as the threshold
above which a query is streamed rather than loaded in a single batch. 
 ​ 
 Session limit 
 Each concurrent connection to the SQL API consumes some resources and attempting
to establish too many connections at once can lead to an out-of-memory crash.
You can use the CUBEJS_MAX_SESSIONS environment variable to adjust the session
limit. 
 ​ 
 Cache control 
 You can use the cube_cache session variable with the SET command 
to control in-memory cache behavior.
It works the same way as cache control in the REST (JSON) API . 
 Example: 
 SET cube_cache = 'must-revalidate' ; 
 ​ 
 Troubleshooting 
 ​ 
 Can't find rewrite 
 Query planning is a resource-intensive task, and sometimes you can get the following
error: Error during rewrite: Can't find rewrite due to 10002 AST node limit reached. 
Use the following environment variables to allocate more resources for query planning:
 CUBESQL_REWRITE_MAX_NODES , CUBESQL_REWRITE_MAX_ITERATIONS , CUBESQL_REWRITE_TIMEOUT . 
 Querying data APIs
 Query format in the SQL API
 x github linkedin 
 Powered by This documentation is built and hosted on Mintlify, a developer documentation platform 
 Assistant 
 Responses are generated using AI and may contain mistakes.
