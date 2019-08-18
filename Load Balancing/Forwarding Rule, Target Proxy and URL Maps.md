# Forwarding Rule, Target Proxy and URL Maps

## Global Forwarding Rule

These are rules that are configured on the cloud platform that  determine where particular traffic will be sent.

 - Route traffic by IP address, port and protocol to a load balancing proxy
 - Can only be used with **global** load baancing HTTP(S) SSL Proxy and TCP Proxy
   - All other LB's that GCP offeres are **regional** so cant use **global** forwarding rules.
   - **Regional** forwarding rules can be used with regional load balancing and individual instances.
   - Regional load balancing includes network and internal.


## Target Proxy

The target proxy is referenced by the global forwarding rule.

 - Designed to handle traffic that is forwarded by the global forwarding rule.
 - Route the incoming requests to a URL map to determine where they should be sent.
   - Target proxy uses the URL map to determine where the traffic for that URL should be sent
- This is only relevent for HTTP(S) LB's. In the case of TCP or SSL Target Proxies, traffic is sent straight to the backend service, there is no URL map.
- Specific to a protocol, different types of proxy for:
  - HTTP
  - HTTPS
  - SSL
  - TCP
- Needs SSL cert if it terminated HTTPS connections
  - Limmit of 10 SSL certs
- Can connect to backend services via HTTP or HTTPS
  - Server will need SSL cert also for HTTPS


## URL Map

A mapping to ensure that the incomming URL is mapped to the correct backend service.

- Used to direct traffic to different instances based on the incoming URL
  - http://www.example.com/login -> backend-service-1
  - http://www.example.com/shop -> backend-service-2


Below is an example URL Map with no rules except the default.

In this case, all traffic is sent to the same groups of instances.

The `/*` path matcher is created automatically and directs all traffic to the same backend service.

@startuml
->
:Target Proxy;
partition URL-Map {
->
:Default setting for service;
}
->
:Backend Service;
@enduml

Below is how a configured URL Map might look.
The URL Map is configured with host rules, path matchers and path rules. Based on these, the traffic is routes to the appropriate backend service.

@startuml
->
:Target Proxy;
partition URL-Map {
->
:Host rules;
->
:Path matcher;
->
:Path rules;
}
->
:Backend Service;
@enduml

 - **Host Rules** reference the domain of the URL: example.com
   - Requests for different domains can be forwarded to different backend services.
- **Path Matcher/Rules** specifies what backend server the different URL paths will map to. You can have /video, video/hd and video/sd all map to different backends.
  - A default `/*` path matcher is created automatically. Traffic that does not match other path rules are sent to this default service.

Below is an example of how a default rule might be used.

@startuml
->
:Target Proxy;
partition URL-Map {
->
:Host rule: 
example.com;
->
if (Path Matcher)
  ->
  :URL Map default:
  No Match - /*;
  ->
  :Backend service:
  www;
  detach
else
  ->;
  :Instance Group;
->
:Path Rules;
->
:Backend Services;
detach
@enduml

URL Maps can be complex and granular as shown below.

![complex_url_map.png](attachments/8fa5954d-fde7-4504-b2f6-64b574012390/b43b4796.png)