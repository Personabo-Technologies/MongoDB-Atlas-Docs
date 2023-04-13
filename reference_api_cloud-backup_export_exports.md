Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cloud Backup Snapshot Export

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

The following resources enable you to configure AWS buckets for exporting
Cloud Backup snasphots and create and retrieve information export jobs.

Endpoint

|

Description  
  
|  
  
/backup/exportBuckets

|

Create, retrieve, and delete Cloud Backup snasphot export buckets.  
  
/backup/exports

|

Create and retrieve Cloud Backup snasphot export jobs.  
  
What is MongoDB Atlas? →

