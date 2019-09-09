# GKE Networking

## VPC Native Clusters

Kubernetes mandates direct Pod-to-Pod connectivity. There is more than one way to achieve this. By default Kubernetes uses static routes for Pod networking, this requires Kubernetes control plane to maintain therse routes to each node. This comes at a scaling cost.

In GKE, there is the option to create clusters in **VPC Native mode**, this provides container native networking.
It enables the connectivity between all pods in a VPC without the overhead of static route scaling.

Kubernetes makes very liberal use of IP addresses. This simplifies the system and makes it easier to use. This makes IP address management a challenge however.

VPC Native mode solves this issue by providing the ability to define, up front cluster scale requirements. This allowes Kubernetes to reduce its overall IP footprint.

## IP Addresses

The Kubernetes networking model relies heavily on IP addresses. Services, Pods, Containers, and nodes communicate using IP addresses.

- **Cluster IP** - The IP address assigned to a Service. This address is stable for the lifetime of the Service.
- **Pod IP** - The IP address assigned to a given Pod. This is ephemeral.
- **Node IP** - The IP address assigned to a given node.

## Subnets

Following subnet resources required:

- Primary Subnet for the Nodes
    - Secondary range for Pods - non-routeable
    - Secondary range for Services
- Master CIDR /28 range for VPC peer - non-routeable outside VPC

### Nodes

Node IP's are taken from the primary range of the subnet associated with the cluster

### Pods

Each Node, by default allocates a /24 block from the Pod address range.
It is possible to configure Nodes to allocate a specific range of IPs for nodes to limit the number of pods each node can run.

### Services

Each cluster needs to reserve a range of IP's for Kubernetes Service cluster IP addresses.
