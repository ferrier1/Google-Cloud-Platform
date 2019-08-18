# Routes


A route is a mapping of an IP range to destination. Routes tell the VPC network where to send packets destined for a particular IP address.

For example all internet-bound packets to a proxy server.

### Two Default Routes for a Network

When a new network is created there are 2 default routes automatically installed:

1.  Directs packets to destinations in the outside world (external IP address). This is the default route for internet traffic.
2.  Allows instances on a VPC to send packets directly to each other (internal IP addresses). One route for every subnet that is created. This is so traffic from the rest of the network can reach that particular subnet.

### Firewall Rules

The existence of a route does not mean that the packet will get to the destination. Firewall rules must be explicitly created to allow packets to move through/into/out of a network.

### What is a Route made of?

-   Name: Human readable name
-   Network: The name of the network to which this route applies
-   Destination Range: The destination IP range this route applies to
-   Instance Tags: Instance tags that this route applies, applies to all instances in destination if empty
-   Priority: Used to break ties in case of multiple matches. If multiple routes are found to the same destination, the one with the highest priority is chosen

In addition to the properties above, every route must also have one  of the following:

-   Next Hop Instance: Fully qualified URL. Instance must already exist
-   Next Hop IP: IP address
-   Next Hop Network: URL of network
-   Next Hop Gateway: URL of gateway
-   Next Hop VPN Tunnel: URL of VPN tunnel

Every route in a VPC might map to 0 or more instances.

Routes apply to an instance if the tag of the route and instance match. This is how to be more specific with routing.

All routes together form something called a Routes Collection?