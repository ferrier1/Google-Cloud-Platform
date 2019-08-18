# Cloud SQL + Cloud Spanner


<br>
Both of these are relational databases with triggers, constraints, lots of structure, tables, entity relationships etc...
<br>
<br>

- **Cloud SQL is open source**
- **Cloud Spanner is proprietary**
- Both are ACID complient so are suitable for OLTP.
- Too slow and too many consistency checks for data warehousing/business analytics (OLAP). - Use BigQuery here.
- OLTP needs strict write consistency, OLAP does not.

Generally if datasets are really massive and un-structured, use BigQuery. For write critical, small, structured datasets, use Cloud SQL or Spanner.

Spanner offeres **horizontal scaling** - Add more and more instances to support growing datasets. 

Cloud SQL uses either Postgres or MySQL storeage engines.

Spanner is proprietary.

Cloud SQL is limited to 10TB of storage.

Cloud SQL is regional