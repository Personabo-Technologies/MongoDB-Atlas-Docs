Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update Snapshot Schedule

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

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

    
    
    PATCH /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/snapshotSchedule  
      
  
## Request Parameters

### Request Path Parameters

Parameter

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique identifier for the project.  
  
`CLUSTER-NAME`

|

Required

|

Name of the cluster.  
  
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

Description  
  
||  
  
`groupId`

|

string

|

Unique identifier of the project.  
  
`clusterId`

|

string

|

Unique identifier of the cluster.  
  
`snapshotIntervalHours`

|

number

|

Number of hours between snapshots. Valid values are: `6`, `8`, `12`, `24`.  
  
`snapshotRetentionDays`

|

number

|

Number of days to keep recent snapshots. Valid values are: `2`, `3`, `4`, `5`.  
  
`dailySnapshotRetentionDays`

|

number

|

Number of days to retain daily snapshots. Valid values are: `0`, `3`, `4`,
`5`, `6`, `7`, `15`, `30`, `60`, `90`, `120`, `180`, `360`.  
  
`pointInTimeWindowHours`

|

number

|

Number of hours in the past for which a Continuous Cloud Backup snapshot can
be created.  
  
`clusterCheckpointIntervalMin`

|

number

|

Number of minutes between successive cluster checkpoints. This only applies to
sharded clusters. This number determines the granularity of continuous cloud
backups for sharded clusters. Valid values are: `15`, `30`, and `60`.  
  
`weeklySnapshotRetentionWeeks`

|

number

|

Number of weeks to retain weekly snapshots. Valid values are: `0`\- `8`, `12`,
`16`, `20`, `24`, `52`.  
  
`monthlySnapshotRetentionMonths`

|

number

|

Number of months to retain monthly snapshots. Valid values are: `0`\- `13`,
`18`, `24`, `36`  
  
## Response Elements

Name

|

Type

|

Description  
  
||  
  
`groupId`

|

string

|

Unique identifier of the project.  
  
`clusterId`

|

string

|

Unique identifier of the cluster.  
  
`snapshotIntervalHours`

|

number

|

Number of hours between snapshots.  
  
`snapshotRetentionDays`

|

number

|

Number of days to keep recent snapshots.  
  
`dailySnapshotRetentionDays`

|

number

|

Number of days to retain daily snapshots.  
  
`pointInTimeWindowHours`

|

number

|

Number of hours in the past for which a Continuous Cloud Backup snapshot can
be created.  
  
`clusterCheckpointIntervalMin`

|

number

|

Number of minutes between successive cluster checkpoints. This only applies to
sharded clusters. This number determines the granularity of continuous cloud
backups for sharded clusters.  
  
`weeklySnapshotRetentionWeeks`

|

number

|

Number of weeks to retain weekly snapshots.  
  
`monthlySnapshotRetentionMonths`

|

number

|

Number of months to retain monthly snapshots.  
  
`links`

|

array

|

Array of related resources. See Linking for details.  
  
## Example Request

### Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl -X PATCH -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
       -H "Content-Type: application/json" "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c7498dg87d9e6526801572b/clusters/Cluster0/snapshotSchedule" \  
       --data '  
       {  
          "snapshotRetentionDays": 3,  
          "monthlySnapshotRetentionMonths" : 2  
       }'  
  
### Example Response

    
    
    {  
      
       "clusterId" : "7c2487d833e9e75286093696",  
       "dailySnapshotRetentionDays" : 7,  
       "groupId" : "6c7498dg87d9e6526801572b",  
       "links" : [ ... ],  
       "monthlySnapshotRetentionMonths" : 2,  
       "pointInTimeWindowHours" : 24,  
       "snapshotIntervalHours" : 6,  
       "snapshotRetentionDays" : 3,  
       "weeklySnapshotRetentionWeeks" : 4  
    }  
  
What is MongoDB Atlas? →

