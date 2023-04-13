Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Alerts

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

The `alerts` resource allows you to retrieve and acknowledge alerts.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/alerts

|

Get all alerts for the project associated to `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/alerts/{ALERT-ID}

|

Get the specified alert for the project associated to `{GROUP-ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/alerts/{ALERT-ID}

|

Acknowledge or unacknowledge the alert specified to `{ALERT-ID}` for the
project associated to `{GROUP-ID}`.  
  
What is MongoDB Atlas? →

