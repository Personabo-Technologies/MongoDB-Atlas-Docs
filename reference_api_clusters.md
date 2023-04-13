Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Clusters

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

Get all clusters for the specified project.

For multi-cloud clusters, use Get All Advanced Clusters.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Get a cluster in the specified project.

For multi-cloud clusters, use Get One Advanced Cluster.  
  
`GET`

|

/clusters

|

Get details for all clusters in all projects available to the programmatic or
personal API key making the request.

## Important

### Multi-Cloud Clusters Unsupported

Atlas excludes multi-cloud clusters from this endpoint's response.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/processArgs

|

Get the advanced configuration options for the cluster in the specified
project.  
  
`POST`

|

/groups/{GROUP-ID}/clusters

|

Create a cluster in the specified project.

For multi-cloud clusters, use Create One Advanced Cluster.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Update a cluster in the specified project.

For multi-cloud clusters, use Modify One Advanced Cluster.  
  
`PATCH`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/processArgs

|

Set one or more advanced configuration options for the cluster in the
specified project.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}

|

Delete a cluster in the specified project.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restartPrimaries

|

Test failure of a primary replica set member to verify your application
handles a replica set failover.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/status

|

Check if Atlas has completed adding a user to, or removing a user from, your
cluster.  
  
`POST`

|

/groups/{GROUP-ID}/sampleDatasetLoad/{CLUSTER-NAME}

|

Load the sample dataset into your cluster.  
  
`GET`

|

/groups/{GROUP-ID}/sampleDatasetLoad/{SAMPLE-DATASET-ID}

|

Check the status of the dataset loading.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/provider/regions

|

Get the cloud providers and regions available for a cluster in the specified
project.  
  
What is MongoDB Atlas? →

