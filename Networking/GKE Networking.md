# GKE Networking

## VPC Native Clusters

Kubernetes mandates direct Pod-to-Pod connectivity. There is more than one way to achieve this. By default Kubernetes uses static routes for Pod networking, this requires Kubernetes control plane to maintain therse routes to each node. This comes at a scaling cost.

In GKE, there is the option to create clusters in **VPC Native mode**, this provides container native networking.
It enables the connectivity between all pods in a VPC without the overhead of static route scaling.

Kubernetes makes very liberal use of IP addresses. This simplifies the system and makes it easier to use. This makes IP address management a challenge however.

VPC Native mode solves this issue by providing the ability to define, up front cluster scale requirements. This allowes Kubernetes to reduce its overall IP footprint.
