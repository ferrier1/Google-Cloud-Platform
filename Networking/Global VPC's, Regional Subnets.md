# Global VPC's, Regional Subnets


#### Projects and VPC's

The defining characteristic of a VPC is the fact that all instances which lie on the VPC whether in the same subnet or not can talk to other instances in the same VPC using internal 1918 addresses. This is assuming the routes and firewall rules have been implemented correctly.

![gcp_project_1.png](attachments\801c0fb4.png)


You cannot send traffic from one VM or instance to another unless there is an explicit firewall rule allowing you to do so.

VPC's are isolated so instances within one VPC cannot communicate with instances in another VPC using 1918 addressing and must use external internet routable addressing.

![gcp_project_2.png](attachments\03bd931d.png)


Within a network the resources communicate with each other often and are **trusted**.

Resources in other networks are treated as external **even if they are in the same project**.

### VPC's are Global, Subnets are Regional

Resources in a VPC can span the globe and are not limited to any particular region or zone.


![gcp_project_3.png](attachments\41fe2b8f.png)

All 3 instances exist in the same VPC and so can communicate using 1918 address space. The machines on the left can exist in the same subnet within the VPC as they are in the same region. In the example above, this VPC will be split into 2 subnets. The instances in us-east1 are in the same region but different zones. Subnets can be multi-zonal but not multi-regional.  
As this is a virtual network they actual location of the instances is immaterial.

#### Recap

- Networks are global - instances can be in different regions/zones.
- Subnets are regional - instances can be in different zones.

![gcp_network_1.png](attachments\6c38683e.png)


In the example above, the network is made up of 3 different subnets.

- Subnet 1 is in zone A, region 1 and has the address space of 10.240.0.0/24
- Subnet 2 is in zone A, region 2 and has the address space of 192.168.1.0/24
- Subnet 3 spans zone A and B in region 2 and has the address space of 10.2.0.0/16

Instances within a subnet must have an IP taken from the range of the subnet. Each subnet has non overlapping ranges as they each belong to the same VPC. Subnet 3 demonstrates how a subnet can be multi-zonal but remain regional. Each instance in the above example will be able to communicate using 1918 address space (providing firewall rules and routing is correct) as they all belong to the same network.


### Differences with Traditional Networking

Traditional networks have a range of IP addresses assigned to it. Each subnet is comprised of a smaller range of IP addresses from the network range.

GCP networks are a collection of subnets that have their own IP ranges. The network itself **does not** have its own IP range associated with it. This means that subnet IP ranges do not have to fit into the networks larger IP range.



### Types of VPC Network

There are 2 types of VPC network to choose from when creating a new VPC:

- Auto Mode - Automatically sets up a single subnet in each region. With this mode you can manually create more subnets later.
- Custom Mode - No subnets are set up by default. All subnets must be manually configured.



#### The "default" Network

Every GCP project has an **auto-mode** network set up by default. It comes with a number of routes and firewall rules preconfigured.

This allows you to get up and running with GCP without thinking about networks.