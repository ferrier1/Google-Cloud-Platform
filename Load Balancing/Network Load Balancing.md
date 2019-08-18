 # Network Load Balancing
 
 
 ![lb_types_diagram.png](attachments/9b6e0c13-34b7-436f-98ef-b32450e3617e/a294d0d4.png)
 
As the above diagram shows, the network load balancer is external meaning it deals with traffic from the internet, but it is regional. The instances to which it distributes traffic are located in a single region.
 
 
 | <h4>OSI Network Stack </h4>| <h4>Load Balancer</h4> |
|:-------------------------------:|:-------:|
| Application Layer | HTTP(S) |
| Presentation Layer | |
| Session Layer| SSL Proxy |
| Transport Layer | TCP Proxy |
| <h4>Network Layer</h4> | <h4>Network</h4> |
| Data Link Layer | |
| Physical Layer | |

The network load balancer operates at the network layer of the OSI stack.
  - Based on incomming IP protocol data, such as address, port and protocol type.
  - **Pass-through, regional** load balancer.  **It does not proxy** connections from clients.
    - It does not create a new internal connection to the backend, it will pass through the connection from the client to the VM instance.
  - Its regional because all VM instances are located in the same region.
  - They can work with UDP, TCP and SSL traffic but in these cases you could prefer to use a load balancer operating at the higher layer in the stack.
  - Network load balancer is useful when load balancing traffic on ports that are not supported by the SSL proxy and TCP proxy load balancers.
    - SSL and TCP proxy load balancers only operate on a specific set of ports, anything outside of this range may need to be done on network load balancer.


### Load Balancing Algorithm

The load balancing algorithm for a network load balancer uses 5 different metrics in order to determine which instance it will connect to.
It picks an instance baseds on a hash of:
  - source IP and port
  - destination IP and port
  - protocol

This can be thought of as a 5 tuple hash. Therefore it is much harder to get session affinity and each new connection may go to a different instance.

Regardless of the session affinity, all packets for a connection are directed to the chosen instance until the connection is closed and have no impact on load balancing decisions for new incoming connections.

This can result in an imbalance between backends if long-lived connections are in use.

### Target Pools

  - Network load balancing forwards traffic to target pools. 
    - It may not use managed instance groups or any instance groups directly.
    - **It is possible to have a MIG associated with a target pool, but a target pool can be stand alone as well.**
  - A target pool is a different logical partition, its simply a **group of instances** which recieve incoming traffic from forwarding rules.
  - Can only be used with forwarding rules for TCP and UDP traffic.
  - There will be a main target pool but also **backup pools** which recieve traffic if the first pool is unhealthy.
  - The network LB makes the decision to send traffic to the backup pool based on the **failover ratio**.
    - **FailoverRatio** is the ratio of failed instances to healthy instances in a target pool.
- If primary target pools ratio is **below the failover ratio** then traffic is sent to the backup pool

##### Health Checks
Just as with managed instance groups, **target pools also have health checks**.

-  Configured to check instance health in target pool.
-  Network load balancing uses legacy health checks for determining instance health.
    - A legacy health check is limited to the HTTP protocol. If you use a network load balancer to balance TCP traffic, you need to run an HTTP service on the VMs being load balanced so that they can respond to health check probes.

##### Firewall Rules

 - HTTP health check probes are sent from the IP ranges:
   - 35.191.0.0/16
    - 209.85.152.0/22
    - 209.85.204.0/22
- The load balancer as well as the health check uses these IP ranges to connect to the instances.
- Firewall rules need to be configured to allow traffic from these ranges.



