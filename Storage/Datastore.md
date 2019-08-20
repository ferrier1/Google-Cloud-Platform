# Datastore

## Document database, NoSQL

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Document database, NoSQL | CouchDB, MongoDB (key-value/indexed database) | DataStore |

Datastore was the origional App Engine database

- Document data -  XML, JSON, HTML has a pattern
- Non-relational (NoSQL)
    - Semi-structured, ACID transactions
        - Unusual for NoSQL database to be ACID complient, due to consistency trade off
- NoOps
- **Alternative to MongoDB**
- Key-value structure - flexible schema definition
- **Typically not used for OLTP or OLAP**
- Fast lookup on keys is the primary use case. **Very fast hash based indexes**
- Scales from 0 to terabytes in size
    - Very cost effective
    - Grows with app
- Good choice for web/mobile apps
- **ACID transactions**
- SQL-like query language (GQL)
- Can be **global in scope**

## Datastore Query Performance

- Like most databases, Datastore uses an indexing file to speed up searching
- By default the built-in index is good for simple query types
- A **composite index** will be necessary for complex queries
    - Defined in custom index config file
        - yaml format
        - Apply using gcloud
            - `gcloud datastore create-indexes`

The speciality of DataStore is that query execution time depends on the size of returned data, **not the size of the data set.**
Returning $10$ rows will take the same length of time whether the dataset is $10$ rows or $10, 000, 000, 000$ rows.
Ideal for random lookups, non sequential.

- Indexes are very fast to read, but slow to write
    - Dont use for write intensive applications

## Firestore

**Firestore** is considered a superset of Datastore and should be used for new projects
