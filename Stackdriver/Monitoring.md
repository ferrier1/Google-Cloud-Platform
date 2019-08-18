# Monitoring

Full-Stack monitoring powered by Google.

  - What is up? What is down? What is overloaded?
  - Native monitoring of GCP, AWS and third-party applications due to stackdriver agent
  - Monitor system and 3rd party application metrics
  - Interacts with Stackdriver Logging
  - Easy to view insights with dashboards and alerts
  - Uptime checks on external applications
    - Must be public and allow firewall traffic from uptime source IP addresses


### Concepts

  - Troubleshoot reachability with external sources (e.g. uptime checks)
  - Familiar with the logging/monitoring agent
  - Know how to use the monitoring tool in conjunction with other stackdriver products to troubleshoot problems
    - Work with alerts


### Stackdriver Agent

  - Software installed on a VM
    - Recommended but not required
  - Without the agent, can still get machine specific info such as:
    - CPU
    - disk/network traffic
    - uptime info
  - Agent accesses additional resource and application service info
  - Monitors many third party applications



### General Best Practices

  - Creates single project for Stackdriver monitoring
    - **Single pane of glass** - Monitor all GCP/AWS resources across all projects
    - IAM controls - Seperate Stackdriver accounts for data and control isolation 
  -  Determine monitoring needs in advance