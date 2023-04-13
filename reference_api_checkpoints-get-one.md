Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Checkpoint

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

Get the specified checkpoint for a sharded cluster.

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

## Resource

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backupCheckpoints/{CHECKPOINT-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`{GROUP-ID}`

|

Required.

|

The unique identifier of the project that owns the checkpoints.  
  
`{CLUSTER-NAME}`

|

Required

|

The name of the cluster that contains the checkpoints that you want to
retrieve.  
  
`{CHECKPOINT-ID}`

|

Required

|

The unique identifer for the checkpoint.  
  
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
  
`clusterId`

|

string

|

ID of the cluster containing the checkpoint.  
  
`completed`

|

BSON timestamp

|

The point in time the checkpoint completed and the balancer restarted.  
  
`groupId`

|

string

|

The unique identifier of the project that owns the checkpoint.  
  
`id`

|

string

|

The checkpoint ID.  
  
`links`

|

array of objects

|

This array includes one or more links to sub-resources and/or related
resources. The relations between URLs are explained in the Web Linking
Specification.  
  
`parts`

|

array of objects

|

The individual parts that comprise the complete checkpoint. There will be one
element for each shard plus one element for the config servers.  
  
`parts[i].replicaSetName`

|

string

|

Name of the replica set. Not present for config servers.  
  
`parts[i].shardName`

|

string

|

The name of the shard.  
  
`parts[i].tokenDiscovered`

|

Boolean

|

Indicates whether the token exists.  
  
`parts[i].tokenTimestamp`

|

document

|

The timestamp of the checkpoint token entry in the oplog, as specified by the
entry’s `ts` field. The `ts` field is a BSON timestamp and has two components:

  * timestamp: the value in seconds since the Unix epoch

  * increment: an incrementing ordinal for operations within a given second

  
  
`parts[i].typeName`

|

string

|

The type of server represented by the part. Possible values are:

  * `REPLICA_SET`, which indicates the part is a shard.

  * `CONFIG_SERVER`

  
  
`restorable`

|

Boolean

|

Indicates whether the checkpoint can be used for a restore.  
  
`started`

|

BSON timestamp

|

The point in time Atlas stopped the balancer and began the checkpoint.  
  
`timestamp`

|

BSON timestamp

|

The point in time the checkpoint restores to.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
       --header "Content-Type: application/json" \  
       --include \  
       -X GET  "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints/6b8cd61180eef547110159d9?pretty=true"  
  
## Example Response

    
    
    {  
      
      "clusterId":"6b8cd6d580eef54711017e89",  
      "completed":"2018-02-13T16:54:09Z",  
      "groupId":"6b8cd3c380eef5349ef77gf7",  
      "id":"6b94183187d9d64b6f2868b5",  
      "links":[  
        {  
          "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints",  
          "rel":"self"  
        },  
        {  
          "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0",  
          "rel":"http://mms.mongodb.com/cluster"  
        },  
        {  
          "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7",  
          "rel":"http://mms.mongodb.com/group"  
        }  
      ],  
      "parts":[  
        {  
          "replicaSetName":"Cluster0-shard-1",  
          "shardName":"Cluster0-shard-1",  
          "tokenDiscovered":true,  
          "tokenTimestamp":{  
            "date":"2018-02-13T16:54:09Z",  
            "increment":1  
          },  
          "typeName":"REPLICA_SET"  
        },  
        {  
          "replicaSetName":"Cluster0-shard-0",  
          "shardName":"Cluster0-shard-0",  
          "tokenDiscovered":true,  
          "tokenTimestamp":{  
            "date":"2018-02-13T16:54:09Z",  
            "increment":1  
          },  
          "typeName":"REPLICA_SET"  
        },  
        {  
          "replicaSetName":"Cluster0-config-0",  
          "tokenDiscovered":true,  
          "tokenTimestamp":{  
            "date":"2018-02-13T16:54:09Z",  
            "increment":2  
          },  
          "typeName":"CONFIG_SERVER_REPLICA_SET"  
        }  
      ],  
      "restorable":true,  
      "started":"2018-02-13T16:54:09Z",  
      "timestamp":"2018-02-13T16:54:09Z"  
    }  
  
What is MongoDB Atlas? →

