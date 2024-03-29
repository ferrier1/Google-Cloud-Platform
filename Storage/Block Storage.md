# Block Storage

## Persistent (hard disk or SSD)

| <h4>When you need: </h4>| <h4>Use</h4> |<h4>GCP Tool</h4>|
|:-------------------------------|:-----------------|:----------------------|
| Storage for Compute, Block Storage | Persistent (hard disks or SSD) | Persistent (hard disks or SSD) |

Block storage refers to data stored in cylinders or in some physical form that is one level lower in abstractions than file storage. This is because files are usually decomposed into blocks.

Block storage points:

- Very low level - no abstraction at all (lowest).
- Data is not structured.
- Meant for use from VM's (GCE). No human or application is going to be dealing directly with blocks. It is consumed by CPU's carrying out low level I/O operations.
- Location is tied to the VM location.
- Data is stored in volumes (called blocks).
- Offers multi-reader mounting
    - Many VM's can read data from the same disk with no performance degredation
- Snapshots are gro-replicatied and available for restore in all regions by default
- Able to resize while in use
- Automatic encryption
- Each disk can be 64TB in size

## Storage area network (SAN)

An effective SAN solution is to attach persistent disks to IaaS VM's

Options available to GCE instance:

- Persistent disks
    - Standard - Sequential access speeds are not too bad
    - SSD - Random access speeds are huge
- Local SSD - Physical drive attached to particular VM
