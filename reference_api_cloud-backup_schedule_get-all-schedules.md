Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Cloud Backup Schedule

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

Unique identifier of the project for the Atlas cluster.  
  
`CLUSTER-NAME`

|

Name of the Atlas cluster that contains the snapshot you want to retrieve.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`autoExportEnabled`

|

boolean

|

Flag that indicates whether automatic export of cloud backup snapshots to the
AWS bucket is enabled. Value can be one of the following:

  * `true` \- enables automatic export of cloud backup snapshots to the AWS bucket

  * `false` \- disables automatic export of cloud backup snapshots to the AWS bucket (default)

  
  
`clusterId`

|

string

|

Unique identifier of the Atlas cluster.  
  
`clusterName`

|

string

|

Name of the Atlas cluster.  
  
`export`

|

document

|

Export policy for automatically exporting cloud backup snapshots to AWS
bucket.  
  
`export.exportBucketId`

|

string

|

Unique identifier of the AWS bucket to export the cloud backup snapshot to.  
  
`export.frequencyType`

|

string

|

Frequency associated with the export policy. Value must be `monthly`.  
  
`links`

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
`nextSnapshot`

|

string

|

UTC ISO 8601 formatted point in time when Atlas will take the next snapshot.  
  
`policies`

|

array of objects

|

A list of policy definitions for the cluster.  
  
`policies.id`

|

string

|

Unique identifier of the backup policy.  
  
`policies.policyItems`

|

array of objects

|

A list of specifications for a policy.  
  
`policies.policyItems.frequencyInterval`

|

number

|

The frequency interval for a set of snapshots.  
  
`policies.policyItems.frequencyType`

|

string

|

A type of frequency. Possible values are:

  * hourly

  * daily

  * weekly

  * monthly

  
  
`id`

|

string

|

Unique identifier for this policy item.  
  
`policies.policyItems.retentionUnit`

|

string

|

The unit of time in which snapshot retention is measured. Possible values are:

  * days

  * weeks

  * months

  
  
`policies.policyItems.retentionValue`

|

number

|

The number of days, weeks, or months the snapshot is retained.  
  
`restoreWindowDays`

|

number

|

Specifies a restore window in days for the cloud provider backup to maintain.  
  
`referenceHourOfDay`

|

number

|

UTC Hour of day between `0` and `23` representing which hour of the day that
Atlas takes a snapshot.  
  
`referenceMinuteOfHour`

|

number

|

UTC Minute of day between `0` and `59` representing which minute of the
`referenceHourOfDay` that Atlas takes the snapshot.  
  
`useOrgAndGroupNamesInExportPrefix`

|

boolean

|

Specifies whether to use organization and project names instead of
organization and project UUIDs in the path to the metadata files that Atlas
uploads to your S3 bucket after it finishes exporting the snapshots. Value can
be one of the following:

  * `true` \- to use organization and project names

  * `false` \- to use organization and project UUIDs (default)

  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/MyCluster/backup/schedule"  
  
## Example Response

    
    
    {  
      
      "autoExportEnabled": false,  
      "clusterId" : "5e2f1bcaf38990fab9227b8",  
      "clusterName" : "myCluster",  
      "links" : [ {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/myCluster/backup/schedule",  
        "rel" : "self"  
      }, {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}",  
        "rel" : "http://mms.mongodb.com/group"  
      } ],  
      "nextSnapshot" : "2020-01-28T05:24:25Z",  
      "policies" : [ {  
        "id" : "5e2f1bcaf38990fab9227b8",  
        "policyItems" : [ {  
          "frequencyInterval" : 6,  
          "frequencyType" : "hourly",  
          "id" : "5e2f1cc8105eef6d6bd9005b",  
          "retentionUnit" : "days",  
          "retentionValue" : 7  
        }, {  
          "frequencyInterval" : 1,  
          "frequencyType" : "daily",  
          "id" : "5e2f1cc8105eef6d6bd9005c",  
          "retentionUnit" : "days",  
          "retentionValue" : 7  
        }, {  
          "frequencyInterval" : 6,  
          "frequencyType" : "weekly",  
          "id" : "5e2f1cc8105eef6d6bd9005d",  
          "retentionUnit" : "weeks",  
          "retentionValue" : 4  
        }, {  
          "frequencyInterval" : 40,  
          "frequencyType" : "monthly",  
          "id" : "5e2f1cc8105eef6d6bd9005e",  
          "retentionUnit" : "months",  
          "retentionValue" : 12  
        } ]  
      } ],  
      "referenceHourOfDay" : 17,  
      "referenceMinuteOfHour" : 24,  
      "restoreWindowDays" : 7,  
      "useOrgAndGroupNamesInExportPrefix" : false  
    }  
  
What is MongoDB Atlas? →

