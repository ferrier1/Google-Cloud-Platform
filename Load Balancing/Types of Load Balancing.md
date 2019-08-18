# Types of Load Balancing


A load balancer is used to direct traffic to a server that has capacity to give a response.

Below is an example of a external LB as it handles requests directly from users.

![external_lb.png](attachments/3291ade9-4058-4ff3-a565-591d6d136665/9b5b5448.png)

Internal LB's handle traffic from other instances on your network.


## Load Balancing

- Load babancing and autoscaling for groups of instances.
- Scale app to support heavy traffic.
- Scale app back down.
- Typlically used in conjunction with a MIG so it has the ability to detect and remove unhealthy VM's, healthy VM's automatically re-added.
- LB will route traffic to the closes VM to the user.
- Fully managed service (no device config), redundant and highly available.

### Load Balancer Options

Below is a digram of the categories of load balancers offered by GCP.

![lb_types_diagram.png](attachments/3291ade9-4058-4ff3-a565-591d6d136665/d0fed95c.png)


As a general rule, always load balance at the highest layer possible in the OSI Stack.

- HTTPS - Application Layer
- SSL Proxy - Session Layer
- TCP Proxy - Transport Layer
- Network - Network Layer

If its possible to have HTTP/HTTPS load balancing then that is the best choice. The higher in the stack you go, the more information and intellegence the application has and the better the load balancing will be.


### Health Checks

- **HTTP & HTTPS health checks**
  - These are the high fidelity health checks because they verify that the web server is up and serving traffic, not just that the instance is healthy.
- **SSL health checks**
  - Use SSL health checks if traffic is not HTTPS but it is encrypted via SSL(TLS).
- **TCP health Checks**
  - For all TCP traffic that is not HTTP(S) or SSL, you configure TCP health check.

Just as in load balancing, the health check should always be at the highest layer possible.