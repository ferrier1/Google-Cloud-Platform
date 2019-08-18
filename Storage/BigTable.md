# BigTable

## Fast scanning, NoSQL

<br>

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Fast scanning, NoSQL | HBase, Cassandra (columnar database) | BigTable | 

- BigTable is similar to HBase.
- Unlike Datastore, BigTable is very fast at scanning sequential key values, not random lookups.
- Columnar database, good for sparse data.
- Need to be careful with key design, hot spotting can kill performance if all queries are hitting the same shard of data.
- Optimized for time-series data.
- Managed service
- Low-latency
- Scales well.
- Cost-effective.
- Bigtable is able to support over a petabyte of data and is useful for high-speed analytics as well, where as Datastore is not.
  