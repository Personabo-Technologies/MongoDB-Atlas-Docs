Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Backup Restore Jobs

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

### Cloud Backups Only

This resource only applies to clusters using Back Up Your Database Deployment.

The `/backup/restoreJobs` resource enables you to create or view restore jobs
for an Atlas cluster with Back Up Your Database Deployment enabled.

## Endpoints

`https://cloud.mongodb.com/api/atlas/v1.0`

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs

|

Get all Cloud Backup restore jobs for the specified cluster.  
  
`GET`

|

/groups/{groupId}/serverless/{instanceName}/backup/restoreJobs

|

Return all restore jobs of one serverless instance.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{JOB-ID}

|

Get one Cloud Backup restore jobs for the specified cluster.  
  
`GET`

|

/groups/{groupId}/serverless/{instanceName}/backup/restoreJobs/{restoreJobId}

|

Return one restore job of one serverless instance.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs

|

Restore one snapshot for the specified cluster.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
`POST`

|

/groups/{groupId}/serverless/{instanceName}/backup/restoreJobs

|

Restore one snapshot for the specified serverless instance.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{JOB-ID}

|

Cancels the Cloud Backup manual download restore job associated to `{JOB-ID}`.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists  
  
What is MongoDB Atlas? →

