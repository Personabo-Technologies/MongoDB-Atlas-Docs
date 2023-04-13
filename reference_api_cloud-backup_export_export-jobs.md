Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Snapshot Export Jobs

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

The `/backup/exports` resource enables you to export backup snapshots to an
AWS bucket and retrieve information on export jobs.

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

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/exports

|

Get all Cloud Backup snasphot export jobs for the specified cluster.  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs/{JOB-ID}

|

Get one Cloud Backup snasphot export job specified by the export job ID.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/restoreJobs

|

Export one Cloud Backup snapshot specified by the snapshot ID to the bucket
specified by the bucket ID.  
  
What is MongoDB Atlas? →

