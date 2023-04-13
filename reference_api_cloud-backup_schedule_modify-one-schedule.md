Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Modify Cloud Backup Backup Policy

Share Feedback

On this page

  * Resource
  * Request Parameters
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

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    PATCH /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule  
      
  
## Request Parameters

### Request Path Parameters

Parameter

|

Type

|

Description  
  
||  
  
`GROUP-ID`

|

string

|

Unique identifier of the project for the Atlas cluster.  
  
`CLUSTER-NAME`

|

string

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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`autoExportEnabled`

|

boolean

|

Optional

|

Specify `true` to enable automatic export of cloud backup snapshots to the AWS
bucket. You must also define the export policy using `export`. Specify `false`
to disable automatic export.  
  
`export`

|

document

|

Optional

|

Export policy for automatically exporting cloud backup snapshots to AWS
bucket.  
  
`export.exportBucketId`

|

string

|

Required

|

Unique identifier of the AWS bucket to export the cloud backup snapshot to. If
necessary, use the Get All Snapshot Export Buckets API to retrieve the IDs of
all available export buckets for a project.  
  
`export.frequencyType`

|

string

|

Required

|

Frequency associated with the export policy. Value can be `daily`, `weekly`,
or `monthly`.  
  
`policies[]`

|

array

|

Required

|

Array containing a document for each backup policy item in the desired updated
backup policy.  
  
`policies[i]`

`.id`

|

string

|

Required

|

Unique identifier of the backup policy that you want to update.  
  
`policies[i]`

`.policyItems[]`

|

array

|

Required

|

Array of backup policy items. Array can be empty, but not null.  
  
`policies[i]`

`.policyItems[n]`

`.frequencyInterval`

|

number

|

Required

|

Desired frequency of the new backup policy item specified by `frequencyType`.
A value of `1` specifies the first instance of the corresponding
`frequencyType`.

## Example

  * In a monthly policy item, `1` indicates that the monthly snapshot occurs on the first day of the month.

  * In a weekly policy item, `1` indicates that the weekly snapshot occurs on Monday.

The following frequency values are valid:

  * Hourly: `1`, `2,`, `4`, `6`, `8`, and `12`.

## Note

The only accepted value you can set for frequency interval with NVMe clusters
is `12`.

  * Daily: `1`

  * Weekly: `1` through `7`, where `1` is Monday and `7` is Sunday.

  * Monthly: `1` through `28` and `40`, where `1` is the first day of the month and `40` is the last day of the month.

  
  
`policies[i]`

`.policyItems[n]`

`.frequencyType`

|

string

|

Required

|

Frequency associated with the backup policy item. One of the following values:
`hourly`, `daily`, `weekly` or `monthly`.

## Note

You cannot specify multiple `hourly` and `daily` backup policy items.  
  
`policies[i]`

`.policyItems[n]`

`.id`

|

string

|

Required

|

Unique identifier of the backup policy item.  
  
`policies[i]`

`.policyItems[n]`

`.retentionUnit`

|

string

|

Required

|

Scope of the backup policy item: `days`, `weeks`, or `months`.  
  
`policies[i]`

`.policyItems[n]`

`.retentionValue`

|

string

|

Required

|

Value to associate with `retentionUnit`.

## Note

Atlas requires that the value specified for `retentionValue` for less frequent
policy items be equal to or larger than the value specified for more frequent
policy items. For example, if the hourly policy item specifies a retention of
two days, the retention for the weekly policy item must be two days or
greater.  
  
`referenceHourOfDay`

|

number

|

Optional

|

UTC Hour of day between `0` and `23`, inclusive, representing which hour of
the day that Atlas takes snapshots for backup policy items.  
  
`referenceMinuteOfHour`

|

number

|

Optional

|

UTC Minutes after `referenceHourOfDay` that Atlas takes snapshots for backup
policy items. Must be between `0` and `59`, inclusive.  
  
`restoreWindowDays`

|

number

|

Optional

|

Number of days back in time you can restore to with Continuous Cloud Backup
accuracy. Must be a positive, non-zero integer.

Applies to continuous cloud backups only.  
  
`updateSnapshots`

|

boolean

|

Optional

|

Specify `true` to apply the retention changes in the updated backup policy to
snapshots that Atlas took previously.  
  
`useOrgAndGroupNamesInExportPrefix`

|

boolean

|

Optional

|

Specify `true` to use organization and project names instead of organization
and project UUIDs in the path for the metadata files that Atlas uploads to
your S3 bucket after it finishes exporting the snapshots. To learn more about
the metadata files that Atlas uploads, see Export Cloud Backup Snapshot.  
  
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

Frequency associated with the export policy. Value can be `daily`, `weekly`,
or `monthly`.  
  
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

Timestamp in the number of seconds that have elapsed since the UNIX epoch when
Atlas takes the next snapshot.  
  
`policies[]`

|

array

|

Unique identifier for the snapshot and an array of backup policy items.  
  
`policies[i]`

`.id`

|

string

|

Unique identifier of the backup policy.  
  
`policies[i]`

`.policyItems[]`

|

array

|

Array of backup policy items.  
  
`policies[i]`

`.policyItems[n]`

`.frequencyInterval`

|

number

|

Desired frequency of the new backup policy item specified by `frequencyType`.  
  
`policies[i]`

`.policyItems[n]`

`.frequencyType`

|

string

|

Frequency associated with the backup policy item. One of the following values:
`hourly`, `daily`, `weekly` or `monthly`.  
  
`policies[i]`

`.policyItems[n]`

`.id`

|

string

|

Unique identifier of the backup policy item.  
  
`policies[i]`

`.policyItems[n]`

`.retentionUnit`

|

string

|

Metric of duration of the backup policy item: `days`, `weeks`, or `months`.  
  
`policies[i]`

`.policyItems[n]`

`.retentionValue`

|

number

|

Duration for which the backup is kept. Associated with `retentionUnit`.  
  
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
  
`restoreWindowDays`

|

number

|

Number of days back in time you can restore to with Continuous Cloud Backup
accuracy. Must be a positive, non-zero integer.

Applies to continuous cloud backups only.  
  
`updateSnapshots`

|

boolean

|

Flag indicating if updates to retention in the backup policy were applied to
snapshots that Atlas took earlier. If set to `true`, the retention changes
were applied to earlier snapshots.  
  
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

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
    |  
    2|   --header "Accept: application/json" \  
    3|   --header "Content-Type: application/json" \  
    4|   --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b6212af90dc76637950a2c6/clusters/MyCluster/backup/schedule" \  
    5|   --data '  
    6|     {  
    7|       "referenceHourOfDay": 12,  
    8|       "referenceMinuteOfHour": 30,  
    9|       "policies": [  
    10|       {  
    11|          "id": "5c95242c87d9d636e70c28ef",  
    12|          "policyItems": [  
    13|            {  
    14|              "id": "5c95242c87d9d636e70c28f0",  
    15|              "frequencyType": "hourly",  
    16|              "frequencyInterval": 6,  
    17|              "retentionValue": 2,  
    18|              "retentionUnit": "days"  
    19|            },  
    20|            {  
    21|              "id": "5c95242c87d9d636e70c28f2",  
    22|              "frequencyType": "weekly",  
    23|              "frequencyInterval": 1,  
    24|              "retentionValue": 3,  
    25|              "retentionUnit": "weeks"  
    26|            }  
    27|          ]  
    28|        }  
    29|       ],  
    30|       "updateSnapshots": true,  
    31|       "autoExportEnabled" : true,  
    32|       "export": {  
    33|         "frequencyType": "monthly",  
    34|         "exportBucketId": "604f6322dc786a5341d4f7fb"  
    35|       }  
    36|     }'  
  
## Example Response

    
    
    1| {  
    |  
    2|   "autoExportEnabled": true,  
    3|   "clusterId" : "5c94f6ea80eef5617167224d",  
    4|   "clusterName" : "MyCluster",  
    5|   "export": {  
    6|     "exportBucketId": "604f6322dc786a5341d4f7fb",  
    7|     "frequencyType": "monthly"  
    8|   },  
    9|   "links" : [ {  
    10|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b6212af90dc76637950a2c6/clusters/MyCluster/backup/schedule",  
    11|     "rel" : "self"  
    12|   }, {  
    13|     "href" : "https://cloud.mongodb.com/api/atlas/v1.0/groups/5b6212af90dc76637950a2c6",  
    14|     "rel" : "http://mms.mongodb.com/group"  
    15|   } ],  
    16|   "nextSnapshot" : "2019-04-03T18:30:08Z",  
    17|   "policies" : [ {  
    18|     "id" : "5c95242c87d9d636e70c28ef",  
    19|     "policyItems" : [ {  
    20|       "frequencyInterval" : 6,  
    21|       "frequencyType" : "hourly",  
    22|       "id" : "5c95242c87d9d636e70c28f0",  
    23|       "retentionUnit" : "days",  
    24|       "retentionValue" : 2  
    25|     }, {  
    26|       "frequencyInterval" : 1,  
    27|       "frequencyType" : "weekly",  
    28|       "id" : "5c95242c87d9d636e70c28f2",  
    29|       "retentionUnit" : "weeks",  
    30|       "retentionValue" : 3  
    31|     } ]  
    32|   } ],  
    33|   "referenceHourOfDay" : 12,  
    34|   "referenceMinuteOfHour" : 30,  
    35|   "useOrgAndGroupNamesInExportPrefix" : false  
    36| }  
  
What is MongoDB Atlas? →

