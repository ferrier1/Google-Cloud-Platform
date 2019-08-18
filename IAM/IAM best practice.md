# IAM Best Practices

## Principle of least privilege

- Giving People just enough access to do what they need
- Use predefined roles over primitave roles
- Grant roles at the smallest scope necessary
    - e.g. Compute Instance Admin vs Compute Admin
    - Compute Admin gives access to almost all of the compute API
    - Compute Instance Admin gives access to GCE related API calls
        - Much more narrow in scope
- Treat each app component as a seperate trust boundary
    - Create seperate service accounts for each service
- Restrict service account access
- Restrict who can create and manage service accounts (Serivce Account Admin)
- Be careful with Owner roles
    - Owner can change IAM policy and Billing
    - Editor might be a better choice

## Service Accounts

- Rotate service account keys
    - Careful not to delete keys being used by running resources
- Dont put service account keys in source code, dont push to git etc..
- Name service keys to reflect user and permissions

## Auditing

- Use Cloud Audit logs to regularly audit IAM policy changes
- Export audit logs to Cloud Storage for long term retention
- Restrict log access with cloud logging roles

## Other best practices

- Use groups
- Have more than one Org admin
- Seperate production and dev envs into seperate projects
