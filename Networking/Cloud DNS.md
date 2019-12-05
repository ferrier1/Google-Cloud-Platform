# Cloud DNS

Cloud DNS is a fully managed service provided by Google. It is a high performance, resilient, global domain name system service that publishes your domain names to the global DNS in a cost-effective way.
They promise to provide a reliable, low-latency lookup for your domain from anywhere in the world.

- Hierarchical distributed database that lets you store IP addresses and other data and look them up by name. - Publish zones and records into the DNS without having to manage your own server.
- No burden of managing your own server.
- Every Cloud DNS instance lives within a project.

## Record Types

Just like a regular DNS server there are several record types:

- A - Address record, maps hostnames to IPv4 addresses.
- SOA - Start of authority - specifies authoritative information on a managed zone. This record is created when you create your managed zone for a particular suffix.
- MX - Mail exchange is used to route requests to mail servers.
- NS - Name Server record, delegates a DNS zone to an authoritative server.

## Resource Record Changes

Cloud DNS holds a resource records sets collection. This collection holds the current state of the DNS records that  make up a particular managed zone. You can read this collection but you don’t modify it directly. In order to modify a record in the record collection, you raise a change request containing additions or deletions can be done in bulk or a single atomic transaction. These changes are first picked up by the authorities servers and then the DNS resolvers when their cache expires.

## Cloud DNS Concepts

### Managed Zones

A managed zone is an entity that manages DNS records for a given suffix (example.com). It is maintained by the cloud DNS. Exactly the same as a normal zone. A project can contain multiple (10000) managed zones.

### Public Zones

A public zone is visible to the internet. You can create DNS records in a public zone to publish your service on the Internet.

### Private Zones

Private zones enable you to manage custom domain names for virtual machines, load balancers and other GCP resources without exposing underlying DNS data to the internet.
A private zone is a container of DNS records that can only be queried by one or more VPC that you authorize.
A private zone can only be queried by resources in the same project where it is defined. Possible to override this restriction using **DNS peering**.
To use private zones with Shared VPC you must create your private zone in the host project, and you must add the appropriate Shared VPC network to the list of authorized networks for that zone.

Private zones do not support DNS security extensions (DNSSEC) or custom resource record sets of type NS.

### Forwarding Zones

A forwarding zone is a type of Cloud DNS **private zone** that sends requests for that zone to the IP address of its forwarding targets.

### Peering Zones

A pewering zone is a type of Cloud DNS **private zone** that follows the name resolution order of another VPC network and can be used to resolve the names that are defined in the other VPC network.