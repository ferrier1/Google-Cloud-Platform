# Filestore

- Cloud Filestore is a managed file storage service for applications that require a filesystem interface and shared filesystem for data
- It gives a simple, native exterience for starting up **managed NAS** with GCE and GKE
- Able to fine-tune Filestores performance and capacity independently leads to predictability fast performance for file-based workloads

## Benefits

- **Fast**
    - Cloud Filestore offers low latency for file operations
    - For workloads that are latency sensitive, like content management systems, databases, random input/output, or other metadata intensive apps
- **Consistent**
    - Pay a predictable price for predictable performance
    - Users can independently choose the IOPS and storage capacity they need
- **Simple**
    - Filestore is a fully managed, NoOps service that is integrated with the rest of the Google Cloud ecosystem
    - Works well with GKE so containers can reference the same shared data
    - Easy to mount Filestore to GCE VM's


## Performance Tiers

|| <h4>Standard </h4>| <h4>Permium</h4> |
|:--:|:-------------------------------|:-----------------|
|Max read throughput| 180MB/s| 700MB/s |
|Max write throughput| 120MB/s|350MB/s|
|Max IOPS|5000|30000|