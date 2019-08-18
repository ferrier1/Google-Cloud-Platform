# Internal Load Balancing


An internal load balancer recieved traffic from the **internal** network and then distributes it across instances in a region.

  - **Private load balancing IP address** that only instances inside your VPC can access.
  - VPC traffic stays **internal** - less latency, more security.
    - No public IP address needed.
  - Useful to balance requests from frontend instances to backend instances.
   
Here is a block diagram of a regional internal load balancer that serves traffic to VM instances on a subnet.
  
  ![internal_lb.PNG](attachments/6bdd7680-c5ec-43c1-8275-36d142e544c3/c37e3dae.PNG)

The backend is a single subnet in the us-central region. The instances in this subnet are served by the internal load balancer. Instances can be in seperate subnets as long as they are within the same VPC and region.
The backend instances have been split among 2 zones.
The IP address of the VIP is from the same range as the subnet.

### Load Balancing Algorithm

  -  The backend instance for a client is selected using a hashing algorighm that takes instance health into consideration.
  -  Uses a 5 tuple hash:
      -  client source IP
      -  client port 
      -  destination IP (load balancer IP)
      -  destination port
      -  protocol (TCP or UDP)
  - When using a 5 tuple hash, you typically do not get session affinity.
  - To introduce session affinity you can hash on only some of the 5 parameters.
    - 3 tuple hash (client IP, dest IP, protocol)
    - 2 tuple hash (client IP, dest IP)


### Health Checks

Based on the kind of traffic being served, you can choose from the following health checks:

- **HTTP & HTTPS health checks**
  - These are the high fidelity health checks because they verify that the web server is up and serving traffic, not just that the instance is healthy.
- **SSL health checks**
  - Use SSL health checks if traffic is not HTTPS but it is encrypted via SSL(TLS).
- **TCP health Checks**
  - For all TCP traffic that is not HTTP(S) or SSL, you configure TCP health check.


### High Availability

 - Internal load balancing is a managed service and is highly available. **no additional config** needed to ensure high availability.
 - Internal load balancing is a regional service, in order to increase the reliability of the service you can **configure multiple instance groups in different zones**.
   - **You cant spread across different regions.**
- With multiple instance groups all instances are treated as if they are in a **single pool** and the load balancer distributes traffic amongst them using the load balancing algorithm.


### Traditional (Proxy) Internal Load Balancing

The ILB on GCP behaves a bit differently to traditional proxy internal load balancers.

 - Configure an internal IP on a load balancing device and clients instance connects to this IP.
 - Traffic coming to the IP is terminated at the load balancer.
 - The load balancer selects a backend and establishes a new connection to it.
 - In effect, there are 2 conenctions:
   - Client<->Load Balancer
   - Load Balancer<->Backend


### GCP Internal Load Balancing

 - Not Proxied - differes from traditional model
   - Pass through, the same connection is end to end.
 - Lightweight load-balancing as a managed service built on top of google's Andromedia network virtualization stack.
 - Provides software-defined load balancing that directly delivers the traffic from the client instance to a backend instance.


### 3-Tier Web App

Below is an example use case where global users connect to the front end using an external HTTP(S) load balancer. Front end instances are connected to the backend instances using an **internal load balancer**


![3-tier-ilb.PNG](attachments/6bdd7680-c5ec-43c1-8275-36d142e544c3/df6b3076.PNG)