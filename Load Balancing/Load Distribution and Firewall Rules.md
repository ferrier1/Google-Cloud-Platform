# Load Distribution and Firewall Rules

## Load DIstribution

Every backend is configured with a **balancing mode**. This is the metric that the load balancer uses to determine how loaded a particular backend is and how much capacity is actually has. The **balancing modes** can either be:
  - **CPU Utilization**
  - Requests per second

Maximum values are set for both, beyond this maximum value the backend cannot deal with traffic. If the backend is part of a MIG, this is when the MIG will try and spin up a new instance from the template.
Short burtsts of traffic above the limmit can occur, its only sustained high traffic that will result in the MIG taking action.

  1. Incoming requests are first sent to the **region closest to the user**, if that region has capacity.
  2. Traffic is distrubuted among zone instances based on capity.
  3. Round robin distribution across instances in a zone.
  4.  Round robin can be overridden by session affinity. (client IP or cookies)


## Firewall Rules

To allow the load balancer to be able to send traffic to the various backends and also for ther healthcheck to be able to poll specific instnaces to check if they are healthy, firewall rules are required.
  - Allow traffic from the following IP's to reach instances:
    - **130.211.0.0/22**
    - **35.191.0.0/26**

These are the IP ranges that the **load balancer** and the **health checker** use to connect to the backends.

- The firewall rule must allow the **port** that the global forwarding rule has been configured to use to forward stuff onto backends.

