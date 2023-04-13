Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Clusters (Advanced)

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `clusters` resource provides access to your cluster configurations. The
resource lets you create, edit and delete clusters. The resource requires your
Project ID.

## Important

Changes to cluster configurations can affect costs. Before making changes,
please see Manage Billing.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.5`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters

|

Return all clusters for the specified project.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Return one cluster in the specified project.  
  
`POST`

|

/groups/{GROUP-ID}/clusters

|

Create one cluster in the specified project.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Update one cluster in the specified project.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Remove one cluster in the specified project.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restartPrimaries

|

Test failure of a primary replica set member to verify your application
handles a replica set failover.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/tenantUpgrade

|

Upgrade a shared-tier cluster in the specified project.  
  
What is MongoDB Atlas? →

