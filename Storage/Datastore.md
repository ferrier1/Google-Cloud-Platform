# Datastore

## Document database, NoSQL

<br>

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Document database, NoSQL | CouchDB, MongoDB (key-value/indexed database) | DataStore |

- Document data -  XML, JSON, HTML has a pattern
- **Alternative to MongoDB**
- Key-value structure
- Typically not used for OLTP or OLAP
- Fast lookup on keys is the primary use case. **Very fast hash based indexes**

The speciality of DataStore is that query execution time depends on the size of returned data, **not the size of the data set.**
Returning $10$ rows will take the same length of time whether the dataset is $10$ rows or $10, 000, 000, 000$ rows.
Ideal for random lookups, non sequential.

- Indexes are very fast to read, but slow to write
  - Dont use for write intensive applications