Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Snapshot Export Buckets

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The `/backup/exportBuckets` resource enables you to grant Atlas access to your
AWS buckets for exporting Cloud Backup snapshots, retrieve buckets that Atlas
can access, and remove access to buckets for Atlas.

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

/groups/{GROUP-ID}/backup/exportBuckets

|

Get all the AWS buckets that Atlas can access for the specified project.  
  
`GET`

|

/groups/{GROUP-ID}/backup/exportBuckets/{BUCKET-ID}

|

Get the AWS bucket associated with `{BUCKET-ID}`  
  
`POST`

|

/groups/{GROUP-ID}/backup/exportBuckets

|

Grant Atlas access to one AWS bucket for exporting backup snapshot.  
  
`DELETE`

|

/groups/{GROUP-ID}/backup/exportBuckets/{BUCKET-ID}

|

Remove Atlas access to the bucket specified by `{BUCKET-ID}`  
  
What is MongoDB Atlas? →

