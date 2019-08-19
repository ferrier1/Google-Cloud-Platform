# Cloud Spanner

Cloud Spanner takes all the limitations of Cloud SQL and attempts to resolve them

- **Horizontally scalable relational database** - unique
- Typlically, RDBMS do not scale well
    - This is down to CAP theorm

## Transactional Consistency vs. Scalability

- Cross-region availability
    - Globally available, exists in multiple regions at the same time, but it is still strongly consistent across all those regions
- Many of the advantages of the RDBMS but without the disadvantages
    - Horizontally scalable is almost infinite

|   | Spanner| Traditional RDBMS |Traditional non-relational|
|:----|:-------|:---------|:--------------|
| Schema | Yes | Yes | No |
| SQL |Yes|Yes|No|
|Consistency|Strong|Strong|Eventual|
|Availability|High|Failover|High|
|Scalability|Horizontal|Vertical|Horizontal|
|Replication|Automatic|Configurable|Configurable|