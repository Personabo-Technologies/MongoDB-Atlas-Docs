Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Checkpoints

Share Feedback

On this page

  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Get all checkpoints for a sharded cluster.

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

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backupCheckpoints  
      
  
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
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

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
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

### Response Document

The response JSON document includes an array of **result** objects, an array
of **link** objects and a count of the total number of **result** objects
retrieved.

Name

|

Type

|

Description  
  
||  
  
results

|

array of objects

|

One object for each item detailed in the results Embedded Document section.  
  
links

|

array of objects

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
totalCount

|

integer

|

Count of the total number of items in the result set. It may be greater than
the number of objects in the **results** array if the entire result set is
paginated.  
  
### results Embedded Document

Each `result` is one cluster checkpoint.

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
       -X GET  "https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints"  
  
## Example Response

    
    
    {  
      
      "links":[  
        {  
          "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints?pageNum=1&itemsPerPage=100",  
          "rel":"self"  
        }  
      ],  
      "results":[  
        {  
          "clusterId":"6b8cd61180eef547110159d9",  
          "completed":"2018-02-08T23:20:25Z",  
          "groupId":"6b8cd3c380eef5349ef77gf7",  
          "id":"5a7cdb3980eef53de5bffdcf",  
          "links":[  
            {  
              "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints",  
              "rel":"self"  
            }  
          ],  
          "parts":[  
            {  
              "replicaSetName":"Cluster0-shard-1",  
              "shardName":"Cluster0-shard-1",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-08T23:20:25Z",  
                "increment":1  
              },  
              "typeName":"REPLICA_SET"  
            },  
            {  
              "replicaSetName":"Cluster0-shard-0",  
              "shardName":"Cluster0-shard-0",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-08T23:20:25Z",  
                "increment":1  
              },  
              "typeName":"REPLICA_SET"  
            },  
            {  
              "replicaSetName":"Cluster0-config-0",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-08T23:20:25Z",  
                "increment":2  
              },  
              "typeName":"CONFIG_SERVER_REPLICA_SET"  
            }  
          ],  
          "restorable":true,  
          "started":"2018-02-08T23:20:25Z",  
          "timestamp":"2018-02-08T23:19:37Z"  
        },  
        {  
          "clusterId":"6b8cd61180eef547110159d9",  
          "completed":"2018-02-09T14:50:33Z",  
          "groupId":"6b8cd3c380eef5349ef77gf7",  
          "id":"5a7db53987d9d64fe298ff46",  
          "links":[  
            {  
              "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/6b8cd3c380eef5349ef77gf7/clusters/Cluster0/backupCheckpoints?pretty=true",  
              "rel":"self"  
            }  
          ],  
          "parts":[  
            {  
              "replicaSetName":"Cluster0-shard-1",  
              "shardName":"Cluster0-shard-1",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-09T14:50:33Z",  
                "increment":1  
              },  
              "typeName":"REPLICA_SET"  
            },  
            {  
              "replicaSetName":"Cluster0-shard-0",  
              "shardName":"Cluster0-shard-0",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-09T14:50:33Z",  
                "increment":2  
              },  
              "typeName":"REPLICA_SET"  
            },  
            {  
              "replicaSetName":"Cluster0-config-0",  
              "tokenDiscovered":true,  
              "tokenTimestamp":{  
                "date":"2018-02-09T14:50:33Z",  
                "increment":4  
              },  
              "typeName":"CONFIG_SERVER_REPLICA_SET"  
            }  
          ],  
          "restorable":true,  
          "started":"2018-02-09T14:50:33Z",  
          "timestamp":"2018-02-09T14:50:18Z"  
        },  
        {  
          ...  
        }  
      ],  
      "totalCount":61  
    }  
  
What is MongoDB Atlas? →

