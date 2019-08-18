# IP Addresses


###  IP Addreses

-   Can be assigned to resources such as VM's.
-   Each VM has an internal IP address that must be drawn from the subnets IP range. This can be manually chosen but most of the time it's done automatically.
-   The internal IP address is what other instances in the VPC use to communicate with the VM.
-   A VM can also have one or more secondary IP addresses. A secondary range can be set on a subnet and the secondary IP address is drawn from this range.
-   If a VM needs to receive external traffic, then it must have an external IP address.


### Internal IP Addresses

-   Internal IP addresses are used for communication within a VPC.
-   Cannot be used across VPC's unless we have special configuration such as shared VPC or VPN connection between VPC's.
-   Can be ephemeral or static, typically ephemeral.
-   VM's know their internal IP address and hostname and this information is available to the network DNS service associated with the VPC.

### External IP Addresses

-   Used to communicate across VPC's.
-   Can be considered a security risk due to external communication.
-   Traffic using external IP addresses can cause additional billing charge.
-   Can be ephemeral or static.
-   VM's are not aware of their external IP address (will not be listed with ifconfig). Able to see via web console/SDK.

| Ephemeral   |      Static      |  
|:----------|:-------------|
| Available only until the VM is stopped, restarted or deleted. Change every 24 hours.  | Permanently assigned to a project and available until explicitly detached from the VM instance.
| No distinction between regional and global IP addresses. | Regional or global resources: <br> - **Regional**: Allows resources of the same region to use the address. Cant attach IP address to resources in different region. <br> - **Global**: Useable in any region. Used for global forwarding rules in global load balancing.  | 
| |Unassigned static IP's incur a cost. Once assigned to VM, they are free to use.|


### Alias IP Ranges


A single service on a VM requires just one IP address. Multiple services running on the same VM may need different IP addresses.

Subnets have primary and secondary CIDR ranges. Use IP aliasing to set up multiple IP addresses drawn from the primary or secondary CIDR range.

![alias_range.png](attachments\7470cb93.png)

In the example above the subnet has a primary and secondary IP range. The VM on the left takes its primary IP address from the primary range and the containerized services running on the VM are using the secondary range.
This allows for each container running on the VM to have its own IP address useable on the network.
VPC's automatically setup routes for the IP's in the subnet, this includes both primary and secondary subnets. 
Containers don’t need to do their own routing, it's all handled by the VPC.
Using alias IP ranges allows us to separate infrastructure from containers. Infrastructure (the host VM) will draw from the primary range and containers from the secondary range of the same subnet.