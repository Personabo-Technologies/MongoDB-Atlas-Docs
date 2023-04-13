Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Online Archive

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `onlineArchives` resource provides access to create, edit, delete, pause,
and resume an online archive for a collection. You can also configure and
manage online archives from the Atlas UI.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives

|

Return all the online archives for a cluster.  
  
`GET`

|

/groups/{GROUP-ID}/privateNetworkSettings/endpointIds

|

Return all the private endpoints for the online archives.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}

|

Return the online archive specified by its ID.  
  
`GET`

|

/groups/{GROUP-ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}

|

Return one private endpoint for the online archives.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/queryLogs.gz

|

Download query logs for an online archive.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives

|

Create an online archive for a collection.  
  
`POST`

|

/groups/{GROUP-ID}/privateNetworkSettings/endpointIds

|

Add one AWS private endpoint for the online archives in the specified project.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}

|

Update, pause, or resume an online archive by its ID.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}

|

Delete an online archive by its ID.  
  
`DELETE`

|

/groups/{GROUP-ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}

|

Delete one AWS private endpoint for the online archives in the specified
project.  
  
What is MongoDB Atlas? →

