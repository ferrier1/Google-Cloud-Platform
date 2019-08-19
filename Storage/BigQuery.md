# BigQuery

## SQL interface on top of file data

| <h4>When you need:</h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| SQL interface on top of data  | Hive (SQL-like, but really its MapReduce on HDFS) | BigQuery |
| Analytics/Data Warehouse (OLAP) | Hive (SQL-like, but really its MapReduce on HDFS) | BigQuery

SQL is important in this case due to the masses of analytics businesses to with data. Business analysts who write SQL to generate reports for analytics will use BigQuery for this.

- Much faster with lower latency than Hive due to proprietary columnar data format. This makes it an option for real time processing, something Hive would never be used for. DataStore and BigTable have lower latency that BigQuery however.
- **Its not ACID complient** so cant be used for transaction processing (OLTP).
- Good for analytics/business intelligence/data warehousing (OLAP).
    - OLTP requires strict write consistency (ACID), OLAP does not.

Appears similar to Hive, due to use cases and SQL-like abstraction for non-relational data. But the underlying implementation is quite different from Hive.
**BigQuery does not rely on HDFS.**

Can do cloud storage federation.

BigQuery is fully managed data warehouse for analytics.

### Quota

BigQuery's quota on max rows per second per project is 100,000 when streamins inserts.
