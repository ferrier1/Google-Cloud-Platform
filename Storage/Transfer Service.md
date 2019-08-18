# Transfer Service

## Importing Data

- The transfer service helps get data **into Cloud Storage**, not out.
- Can import data from:
  - AWS - S3 bucket
  - HTTP/HTTPS location on the web
  - local files (can also use gsutil)
  - Another Cloud Storage Bucket

#### Transfer Service or gsutil?
 
 gsutil can also be used to get data into cloud storage buckets.

- Perfer Transfer Service when transferring from AWS
- **If copying local files over from on-premise, use gsutil**

### Transfer Service Features

- Can do one-time and **recurring transfers**
- Delete files from destination if they are not present in the source - to keep source and dest in perfect sync
- Delete from source after copy 
- Possible to set up synchronisation of source and destination based on file filters. Possible to keep AWS and GCP data in sync.