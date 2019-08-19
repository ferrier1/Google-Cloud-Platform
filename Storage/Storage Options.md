 # Storage Options
 
 ## Overview Scenarios

 - Block Storage for compute VM's - **Persistent disks or SSD's.**
 - Immutable blocs like video/images - **Cloud Storage.**
 - OLTP (transaction processing) - **Cloud SQL** (MySQL or Postgres) or **Cloud Spanner** (Google proprietary).
 - NoSQL HTML/XML - **Datastore**.
 - NoSQL Key-values - **BigTable**. (Similar to HBase)
 - Getting data into Cloud Storage - Transfer service.

 


**Databases are an abstraction on file storage. File storage is an abstraction on block storage.** Block storage refers to the kind of storage carried out by application directly. If you refer to data using a physical hardware address, that is block storage. If you refer to data using a logical hierarchical directory address, that is file storage. One level of abstraction higher would be to refer to the data using a query language like SQL.
**Block storage is one level below file storage in abstractions.**


### Use Cases

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Storage for Compute, Block Storage | Persistent (hard disks or SSD) | Persistent (hard disks or SSD) | 
| Storing media, Blob Storage | File system - maybe HDFS | Cloud Storage |
| SQL interface on top of data  | Hive (SQL-like, but really its MapReduce on HDFS) | BigQuery |
| Document database, NoSQL | CouchDB, MongoDB (key-value/indexed database) | DataStore |
| Fast scanning, NoSQL | HBase, Cassandra (columnar database) | BigTable | 
| Transaction Processing (OLTP) | RDBMS | Cloud SQL, Cloud Spanner | 
| Analytics/Data Warehouse (OLAP) | Hive (SQL-like, but really its MapReduce on HDFS) | BigQuery |


### Mobile-Specific Use Cases

| <h4>When you need: </h4>| <h4>Use</h4> |
|:-------------------------------|:-----------------| 
| Storage for Compute, Block Storage along with mobile SDKs | Cloud Storage for Firebase | 
| Fast random access with mobile SDK's | Firebase Realtime DB | 


### GCP to Open source matchup

|<h4>Open Source</h4>| <h4>GCP</h4>|
|:--------------------------:|:-------------:|
|MongoDB| Datastore|
|HBase|BigTable|
|Hive|BigQuery|

## Summary

- Block Storage for compute VM's  - Persistent disks or SSD's
- Immutable file blob storage like video/images - Cloud Storage DataProc does not use HDFS but Cloud Storage underneath  
- OLTP - Cloud SQL or Cloud Spanner
- OLAP - BigQuery
- NoSQL Documents (HTML/XML) - Datastore
- NoSQL Key-values - BigTable (~HBase)
- Getting data into Cloud Storage - Transfer Service


![storage_options.svg](attachments/3hf75ape.svg)