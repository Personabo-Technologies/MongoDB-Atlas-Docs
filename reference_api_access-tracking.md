Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Access Tracking

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

To view database access history, you must have either the `Project Owner` or
`Organization Owner` role.

Use the following resources to view the database access history settings. Each
resource requires at minimum your Group ID.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/dbAccessHistory/clusters/{CLUSTER-NAME}

|

Retrieve the access logs of a cluster by cluster name  
  
`GET`

|

/groups/{GROUP-ID}/dbAccessHistory/processes/{HOSTNAME}

|

Retrieve the access logs of a process by hostname  
  
What is MongoDB Atlas? →

