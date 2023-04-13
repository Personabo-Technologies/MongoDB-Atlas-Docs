Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Search

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `fts` resource allows you to retrieve and edit Atlas Search analyzers and
index configurations for the specified cluster.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{DATABASE-
NAME}/{COLLECTION-NAME}

|

Get all Atlas Search indexes for a specified collection.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}

|

Get one Atlas Search index by its `indexId`.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/analyzers

|

Get all Atlas Search user-defined analyzers for a specified cluster.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/

|

Create an Atlas Search index.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}

|

Update an Atlas Search index by its `indexId`.  
  
`PUT`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/analyzers

|

Update the Atlas Search user-defined analyzers for a specified cluster.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}

|

Delete one Atlas Search index by its `indexId`.  
  
`GET`

|

/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics

|

Get all Atlas Search metric types for one process in the specified project.  
  
`GET`

|

/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/measurements

|

Get all Atlas Search hardware and status metrics for one process in the
specified project.  
  
`GET`

|

/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/indexes/{INDEX-
ID}/measurements

|

Get all Atlas Search index metrics for one Atlas Search index on the specified
process.  
  
`GET`

|

/groups/{GROUP-ID}/hosts/{PROCESS-ID}/fts/metrics/indexes/{DATABASE-
NAME}/{COLLECTION-NAME}/measurements

|

Get all Atlas Search index metrics for a namespace on the specified process.  
  
What is MongoDB Atlas? →

