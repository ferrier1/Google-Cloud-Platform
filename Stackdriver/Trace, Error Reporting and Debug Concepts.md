# Trace, Error Reporting and Debug Concepts

## Trace

  - Find performance bottlenecks - latency 
  - Collects data from GAE, HTTP(s) load balancers, or apps with Stackdriver trace SDK
  - Integrated with App Engine Standard - automatically enabled
  - Available for GCE, GKE and GAE flex
    - Required enabling Stackdriver Trace API or SDK - depsnds on library
  - Can be installed on non-GCP resources

It measures the latency (specifically in loading times) as your app goes through different microservices along the entire chain. It helps to answer questions such as:
  - How long does it take my application to handle a given request?
    - Why is it taking my application so long to handle a request?
    - Why do some of my requests take longer than others?
  - What is the overall latency of requests to my application?
  - Which microservice is causing a bottleneck?
  - Has latency to my application increased or decreased over time?
  - What can I do to reduce application latency?

## Error Reporting

  - Real-time error monitoring and alerting of your application
  - Quickly understand errors
  - Write to stackdriver logging or error reporting API (beta)
  - Automatic and real-time analysis
    - Alerts and dashboards
  - Built into App Engine standard and Cloud Functions - automatically enabled
  - Beta for Flexible, GCE, GKE and EC2
  - Stackdriver logging agent required for GCE, GKE, EC2 and flex
  - Java, Python, Node, Go libraries 

## Debug

  - Debug application
  - Used in close conjunction with Error Reporting
  - Inspect application state without slowing or stopping the app
  - Does not require adding log statements
  - Automatically enabled in GAE standard
  - Available in Flex, GCE and GKE with additional config
  - Java, Python, Node, Go libraries 
  - Can be installed on non-GCP resources

## Profiler (beta)

  - Profile resources intensive applications
  - Collect CPU/RAM usage data
    - Associate this data with source code to identify high usage componenets