Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Auditing

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The following resources provide access to project auditing settings. Each
resource requires at minimum your Project ID.

Process and audit logs are updated from the cluster backend infrastructure
every five minutes and contain log data from the previous five minutes. If you
are polling the API for log files, polling every five minutes is recommended.

## Example

If the logs are updated at 4:00 UTC and then you poll the API, the API returns
log data from the interval between 3:55 UTC and 4:00 UTC.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/auditLog

|

Get audit configuration for the project associated with `{GROUP-ID}`  
  
`PATCH`

|

/groups/{GROUP-ID}/auditLog

|

Modify the audit configuration for the project associated with `{GROUP-ID}`  
  
What is MongoDB Atlas? →

