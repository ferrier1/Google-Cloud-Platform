# VPCs And Subnets

#### Overview

- Provides global flexible networking for cloud resources
- Resources in GCP projects are split across VPC's
- Routes and forwarding rules must be configured to allow traffic within a VPC and the outside world
- Firewall rules must also be configured 
- VPN, peering, shared VPC's are some ways to connect VPC's or a VPC with on prem network

#### Virtual Private Cloud

A global private isolated virtual network partition that provides managed networking functionality

- Global because a network can have instances in multiple regions in the world - the instances that form the network can be in any zone in any region
- Private because you need to setup special permissions for people to access your network. Must explicitly allow traffic into and out of your VPC using firewall rules. Adding new resources like firewall rules can be locked down with IAM
- Virtual because the actual machines may not be located in the same place
- Managed because a lot of the details of running a network are abstract from the user



Multi-tenancy is supported. VPC's can be shared across GCP projects. A shared VPC means that routing and firewall rules can span multiple projects. Or a VPC can belong to a single project.

Very scalable, easy to add new VM's, containers and any other resources to the network. 7000 VM's per VPC is the hard limit.


#### Projects and VPC's

Typically in a GCP organisation you will have several projects where each project corresponds to a business/billing unit.

A project might represent the resources that belong to a certain team. 
Each project will have multiple networks for different functions. If you need to separate instances in the same project from talking with internal IP's, its common to put them in different networks under the same project.

A single project has a quota of 5 networks - can increase for £££

A single network has a limit of 7000 instances - note limit not quota (cant increase)


#### Subnets

Logical partition of the network.

- Defined by an IP address range
- CIDR notation
- IP ranges cannot overlap between subnets in the same network
- Subnets are regional. They can only contain resources from a single region.
- Subnets can contain resources from different zones within a region

To modify the size of a subnet once it has been created use the following command:

```bash
gcloud compute networks subnets expand-ip-range <subnet-name> \
--prefix-length <new-length> --region <region>
```
