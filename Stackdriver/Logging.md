 # Logging
 
 Stackdriver logging acts as a single central repository for different types of log data and events from multiple sources such as GCP and AWS. It allows you to store and analyze logging data.
It collects platform, system and application logs with the help of an installed agent.
Stackdriver logging has intergration with stackdriver monitoring, the 2 products work together to track events and display alterts when errors occur. It provides realtime and batched logging.

It allows you to export logs out of stackdriver logging into other sources for different types of long term storage and analysis.

Logs in stackdriver logging are displayed per project.

#### Concepts and Terminology

- **Log entry** - records status or event
  - Includes log name
 - **Log** - named collection of log entries
   - Only exist of there are log entries
 - **Retention period**
   - Depends on log type

##### Log Types

 - "Who did what, where and when?"
 - **Audit logs**
   - Admin Activity, System Event, Access Transparency, Data access
- **Agent logs**
  - Agent installed on VM's
  - Records VM system and third-party app logs


##### Admin Activity/System Event Logs

  - Always on, immutable, no charge
  - Admin activity = administrative actions and API calls (e.g. James created an instance)
  - System events = GCE system event (e.g. live migration)

##### Data Access Logs

  - Logs API calls that create, modify, or read user-provided data
  - **Not on by default**, can become large
  - Charge if beyond free limits


##### Agent Logs

  - Installed on a supported VM
  - Logs data from third-party apps
  - Also incurs charge beyond free limits


##### Other Types

  - Access Transparency - Access logs when GCP support staff access data (enterprise support package)



### Retention

| <h4>Log Type: </h4>| <h4>Retention Period</h4>
|:-------------------------------|:-----------------|
| Admin Activity |400 days |
| Data Access |30 days|
|System Event|400 days|
|Access Transparency|400 days|
|All other logs|30 days|

#### Exporting Logs
  - After retention period, logs are deleted and **cannot be recovered**
  - Export logs for long term retention
  - Log term storage (Cloud Storage), big data analysis (BigQuery), stream to other sources (Pub/Sub)

  - Requires a project and destination service
  - Create a **filter** - select log entries to export
  - Choose a **destination** - Cloud Storage, BigQuery, Pub/Sub
  - Filter and destination held in **sink** - direct what entries to copy to which destination
  - Only new entries are exported after sink creation


#### IAM Roles

  - Logging Admin - full control plus add other to Logging IAM
  - Logs Viewer - View logs
  - Logs Writer - Grant to service account so can generate and write logs
  - Logs Configuration Writer - Create metrics and export sinks
