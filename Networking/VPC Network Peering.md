# VPC Network Peering

Another way to connect networks across GCP is to use VPC Network Peering. This can be used to connect networks in different projects and different organizations.
VPC network peering differs very significantly to shared VPC in two ways:
1. The networks peered using VPC network peering are administratively separate. They each have their own firewall rules and policies.
2. You can peer networks from different organizations. Shared VPC networks can only work between projects in the same organization.


## VPC Network Peering

- Allows private 1918 connectivity across two VPC networks. The instances on each network can communicate using internal IP addresses.
- Networks can be in the same or in different projects.
- Often used to build SaaS ecosystems in GCP. Services can be made available privately across different VPC networks and organizations. Services can be consumed using private IP addressing from another organization. 
- VPC network peering is useful for the following organizations:
  - Organizations with several administrative domains. These domains exist within the same organization but have different administrators. VPC network peering can connect these networks.
  - Organizations that want to peer with other organizations on GCP.


### VPC Network Peering Benefits

There are several reasons to use VPC network peering as opposed to using external public IP addressing to route between VPC's:

 - **Lower latency** as compared with public IP networking as there is no external DNS or route lookup and it does not traverse the internet.
- **Better security** as services don’t need to expose an external IP address to talk to other services in other networks. External IP addresses are always a security concern.
- **Cost effective** as using internal IP addresses for traffic avoids egress bandwidth pricing. Google charges for external IP egress traffic even if the 2 IP's are in the same zone. Using internal IP addresses to communicate cross network will only incur normal network pricing.


### VPC Network Peering Properties

 - Peered networks are **administratively separate**. Routes, firewalls, VPNs, and traffic management is applied separately. This means you can have different teams or admins manage each network independently. **However the network appears as one to instances** in either VPC because they can communicate to other instances using internal IP addresses.
 - One VPC network can peer with multiple networks with a limit of 25. Each side of the VPC peering is configured separately. One side can be ready to establish but can't until the other side is also ready. 
 - Only directly peered networks can communicate. **The peering is not transitive.**


## Peered Networks and Internal Load Balancing

Internal load balancing is within a particular region.

![vpc_peering_lb.png](attachments\d508e9e9.png)

In the above diagram, network-B is peered with two networks, network-A and network-C. Network-A has a load balancer in it, it will load balance all traffic to all VM instances that connect to it. The load balancer in network-A will automatically apply to the VM instances network-B with no additional configuration required. The load balancer will basically treat the VM instances in network-B as if they were in network-A.

Network-C is not directly peered with network-A so instances in each cannot communicate. The load balancer also does not apply to network-C instances.

## Peered Networks and Firewalls

![vpc_peering_fw.png](attachments\e2c9de85.png)

In the above diagram, the two networks are peered together using VPC peering. The VM instances can talk to each other using internal IP addresses. Firewall rules are configured and managed separately in each network. The administrator of network-B can decide that subnet-3 is not allowed to receive traffic from subnet-1 and subnet-2.
Firewall rules are very important in VPC peering's as they are the only way of blocking access to certain instances. Peering networks allows access to all instances in the network.

## Peered Networks and Shared VPC's


![vpc_peering_shared_vpc.png](attachments\5569da9c.png)

Host project P1 in the above diagram has a shared VPC with two service projects attached. The peering to project P2 is completely legit and behaves just like any other VPC peering. All the VM's in the diagram can communicate using internal IP addresses. Direct peering between two shared VPC's is also possible.

## Peered Networks and Multiple NIC's

![vpc_peering_multiple_nic.png](attachments\90ee6527.png)

In the above diagram VM1 has two NIC's, one in network-A and one in network-B each has an IP address for its respective network. IP2 belongs to network-B the other network interface IP1 belongs to network-A.  Network-B and network-C are peered with each other. All instances in network-C can access IP2 on VM1** but not IP1**. **Network-A is standalone, not peered**. IP3 and IP2 can communicate with each other. IP1 on network-A cannot see any instances in network-B or network-C.
