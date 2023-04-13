Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Namespaces for a Host

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

Retrieve up to 20 namespaces for collections experiencing slow queries for a
specified host. Namespaces appear in the following format:
`{database}.{collection}`.

## Note

If you specify a secondary member of a replica set that has not received any
database read operations, the endpoint does not return any namespaces.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/processes/{PROCESS-ID}/performanceAdvisor/namespaces  
      
  
### Request Path Parameters

Path Element

|

Description  
  
|  
  
`GROUP-ID`

|

The unique identifier for the project where the the MongoDB host resides.  
  
`PROCESS-ID`

|

The unique identifier for the host of a MongoDB process in the following
format: `{hostname}:{port}`. For information about retrieving process ids, see
Get All MongoDB Processes in a Group.  
  
### Request Query Parameters

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
  
|

|

|

|  
  
||||  
  
since

|

number

|

Optional

|

Timestamp in the number of seconds that have elapsed since the UNIX epoch from
which to retrieve suggested indexes.

  * If you don't specify **duration** , the endpoint returns results between **since** and the current time.

  * If you specify neither **duration** nor **since** , the endpoint returns data for the previous 24 hours.

|  
  
duration

|

number

|

Optional

|

Length of time in milliseconds during which to find suggested indexes among
the managed namespaces in the cluster.

  * If you don't specify **since** , the endpoint returns results for the **duration** before the current time.

  * If you specify neither **duration** nor **since** , the endpoint returns data for the previous 24 hours.

|  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response Elements

Name

|

Type

|

Description  
  
||  
  
`namespaces`

|

array

|

Each element in the array represents one namespace on the specified host.
Namespaces appear in the following format: `{database}.{collection}`.  
  
`namespaces[i].namespace`

|

string

|

A namespace on the specified host.  
  
`namespaces[i].type`

|

string

|

The type of namespace.  
  
## Example Request

    
    
    curl --digest -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
       "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c381af480eef519ea5cdeb1/processes/cluster0-shard-00-00-mnswc.mongodb-dev.net:27017/performanceAdvisor/namespaces?namespace=data.zips&pretty=true"  
  
## Example Response

    
    
    {  
      
      "namespaces" : [ {  
        "namespace" : "data.zips",  
        "type" : "COLLECTION"  
      }, {  
        "namespace" : "data.stocks",  
        "type" : "COLLECTION"  
      } ]  
    }  
  
What is MongoDB Atlas? →

