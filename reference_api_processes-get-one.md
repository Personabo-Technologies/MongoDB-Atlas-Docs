Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get MongoDB Process by ID

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
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

Get information for the specified Atlas MongoDB process in the specified
project. An Atlas MongoDB process can be either a `mongod` or a `mongos`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project whose MongoDB processes you want to
retrieve.  
  
`HOST`

|

Required.

|

The hostname of the machine running the Atlas MongoDB process.  
  
`PORT`

|

Required.

|

The port to which the Atlas MongoDB process listens.  
  
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

### Response Elements

If you set the query element envelope to `true`, the response is wrapped by a
`content` object.

Name

|

Type

|

Description  
  
||  
  
`created`

|

DateTime

|

Date this Atlas MongoDB process was created by Atlas.  
  
`groupId`

|

string

|

ID of the project that owns the Atlas MongoDB process.  
  
`hostname`

|

string

|

The hostname of the machine running the Atlas MongoDB process.  
  
`id`

|

string

|

The hostname and port of the Atlas MongoDB process in `hostname`:`port`
format.  
  
`lastPing`

|

DateTime

|

When the last ping for this Atlas MongoDB process was received.  
  
`links`

|

array of objects

|

One or more links to sub-resources and/or related resources.  
  
`port`

|

number

|

The port to which the Atlas MongoDB process listens.  
  
`shardName`

|

string

|

Name of the shard this process belongs to. Only present if this process is
part of a sharded cluster.  
  
`replicaSetName`

|

string

|

Name of the replica set this process belongs to. Only present if this process
is part of a replica set.  
  
`typeName`

|

string

|

Type for this Atlas MongoDB process. Possible values are:

  * `REPLICA_PRIMARY`

  * `REPLICA_SECONDARY`

  * `RECOVERING`

  * `SHARD_MONGOS`

  * `SHARD_CONFIG`

  * `SHARD_STANDALONE`

  * `SHARD_PRIMARY`

  * `SHARD_SECONDARY`

  * `NO_DATA`

The type for new processes added to Atlas will be `NO_DATA` until Atlas
completes deployment of the process.  
  
`userAlias`

|

string

|

User-friendly hostname of the cluster node. The user-friendly hostname is
typically the standard hostname for a cluster node and it appears in the
connection string for a cluster instead of the value of the `hostname` field.  
  
`version`

|

string

|

Version of MongoDB running for this process.  
  
## Example Request

## Important

You must modify the following code block with the appropriate credentials,
project ID, host, and port.

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}?pretty=true"  
      
  
## Example Response

    
    
    HTTP/1.1 200 OK  
      
    Content-Type: application/json  
    Date: Wed, 23 Aug 2017 15:41:26 GMT  
    Strict-Transport-Security: max-age=300  
    Content-Length: 948  
    Connection: keep-alive  
      
    {  
      "created" : "2020-08-25T18:44:13Z",  
      "groupId" : "12345678",  
      "hostname" : "atlas-abcdef-shard-00-00.nta8e.mongodb.net",  
      "id" : "atlas-abcdef-shard-00-00.nta8e.mongodb.net:27017",  
      "lastPing" : "2020-09-01T18:40:06Z",  
      "links" : [ ... ],  
      "port" : 27017,  
      "replicaSetName" : "atlas-abcdef-shard-0",  
      "typeName" : "REPLICA_PRIMARY",  
      "userAlias" : "testcluster-shard-00-00.nta8e.mongodb.net"  
      "version" : "4.4.0"  
    }  
  
What is MongoDB Atlas? →

