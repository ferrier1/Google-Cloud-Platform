# Cloud Storage

## Blob Storage

<br>
<br>

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Storing media, Blob Storage | File system - maybe HDFS | Cloud Storage |


Cloud Storage points:

- Created in the form of Buckets
- Buckets are globally unique
  - Name (globally unique)
  - Location
  - Storage Class

Bucket Storage Classes Summary:
- Multi-regional
  - Use this for "hot" data that is frequently accessed from all over the world.
- Regional
  - Data intensive applications inside a specific region.
  - Appropriate for storing data that is used by GCE instances.
  - Better performance for data-intensive applications, as opposed to storing data in a multi-regional location.
- Nearline
  - Accessed once a month - very cheap storage, if accessed infrequently
  - Up front commitment to keep data there for at least 30 days
  - Read/write charges are significant for frequent access.
- Coldline
  - Accessed once a month - very cheap storage, if accessed infrequently
  - Unlike other *"cold"* storage services offered by other providers. The underlying storage technology used is the same as *"hot"* storage like regional and multi-regional. This means the latency and throughout is the same. Its only if you do need to access it, its going to be very expensive.

Items stored inside a storage bucket can be of any class below the bucket itself. Items default to the buckets class however.

Cloud storage is used when you need to store large immutable blob like data.

#### Bucket Storage Classes:

|Storage Class|Characteristics|Use Cases|Price(per GB, per month)|
|:--------------|:--------------|:----------|:-------------------------|
| Multi-Regional Storage | - $99.95\%$ availability SLA <br> - Geo-redundant. Cloud storage stores data redundantly in at least $2$ regions seperated by at least $100$ miles.| Storing data that is frequently accessed from around the world, such as serving website content, streaming videos or gaming and mobile apps.| $\$0.026$|
| Regional Storage | - $99.9\%$ availability SLA <br> - Lowest cost per GB stored <br> - Data is stored in single geographic region | Storing frequently accessed data in the same region as your GCE instance or DataProc. | $\$0.02$ |
|Nearline Storage| - $99.0\%$ availability SLA <br> - Very low cost per GB stored <br> - Data retrieval costs <br> - Higher per-operation costs <br> - 30-day minimum storage duration| Data you do not expect to access frequently. Back-up and | $\$0.01$|
| Coldline Storage | - $99.0\%$ availability SLA <br> - Lowest cost per GB stored <br> - Data retrieval costs <br> - Higher per-operation costs <br> - 90-day minimum storage duration | Data you expect to access infrequently (once per year). Disaster recovery, or archiving. | $\$0.007$ | 


### Working with Cloud Storage

The following tools are ways in which access data in buckets:

- XML and JSON APIs
- Command line (gsutil)
- GCP Console (web)
- SDKs


### Domain-Named Buckets

GCP makes it easy to store static data like images and CSS for example for a website using cloud storage. It does this by understanding a bucket can be a valid DNS name if it contains the  correct syntax.

- Cloud Storage considers bucket names that contain dots to be domain names.
- Must be valid DNS name syntax.
  - E.g bucket names with multiple dots in a row like *web...static.example.com* is not valid.
- If you devide to use bucket names as domain names then you must end with a recognized top-level domain such as .com
- Need to pass domain ownership verification

#### Domain Verification

There are a number of ways to prove ownership of a domain, including:

- Adding a special Meta tag to the sites homepage.
- Uploading a a html file that access data in the top level directory for instance: <br >```yourdomain.com/.top-level/pki-validation```
- Verify ownership from the search console by finding your provider


### Mobile-Specific Use Cases

| <h4>When you need: </h4>| <h4>Use</h4> |
|:-------------------------------|:-----------------| 
| Storage for Compute, Block Storage along with mobile SDKs | Cloud Storage for Firebase | 
| Fast random access with mobile SDK's | Firebase Realtime DB | 


Cloud storage for Firebase is meant for mobile app developers who need to store and serve user generated content such as photographs/videos. Firebase adds a layer of security to the storage of this data.

Firebase Realtime DB is a NoSQL JSON document database that helps to keep data synced across all clients in realtime and it reamains available even if the app goes offline. Its similar to Datastore.

## Permissions

Permissions can be viewed for a storage bucket using the following:
```bash
gsutil acl get gs://acl-test-4325/
```
This will return a json output wiut the ACL associated with the file. Below is an example of a newly created bucket with default permissions:

```json
[
  {
    "entity": "project-owners-1004155386974",
    "projectTeam": {
      "projectNumber": "1004155386974",
      "team": "owners"
    },
    "role": "OWNER"
  },
  {
    "entity": "project-editors-1004155386974",
    "projectTeam": {
      "projectNumber": "1004155386974",
      "team": "editors"
    },
    "role": "OWNER"
  },
  {
    "entity": "project-viewers-1004155386974",
    "projectTeam": {
      "projectNumber": "1004155386974",
      "team": "viewers"
    },
    "role": "READER"
  }
]
```

In order to make the bucket private:

```bash
gsutil acl set private gs://acl-test-4325/
```
```json
[
  {
    "entity": "project-owners-1004155386974",
    "projectTeam": {
      "projectNumber": "1004155386974",
      "team": "owners"
    },
    "role": "OWNER"
  }
]
```
To make the bucket public for read access:

```bash
gsutil acl ch -u AllUsers:R gs://acl-test-4325/
```
```json
[
  {
    "entity": "project-owners-1004155386974",
    "projectTeam": {
      "projectNumber": "1004155386974",
      "team": "owners"
    },
    "role": "OWNER"
  },
  {
    "entity": "allUsers",
    "role": "READER"
  }
]
```

### Life Cycle Management

In order to automatically delete a bucket or perform other actions after a given period of time a life cycle policy can be set.
By default no life cycle policy is set.

Define a policy using JSON:

```json
{
"rule": [{
"action": {"type": "Delete"},
"condition": {"age": 30}
}]
}
```
This policy states the files in the bucket on the codition that their age has gone over 30 days.

Attach the policy to the bucket using gsutil:

```bash
gsutil lifecycle set policy.json gs://my-bucket
```


### Versioning