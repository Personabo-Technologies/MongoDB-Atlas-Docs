Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Rolling Index

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `index` resource lets you create a rolling index for a cluster. Rolling
indexes are created on one cluster node at a time, reducing system stress.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

You cannot create a rolling index on an `M0` free cluster or `M2/M5` shared
cluster. To upgrade a free cluster or shared cluster, see Modify a Cluster.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/index

|

Create a rolling index on the specified cluster.  
  
What is MongoDB Atlas? →

