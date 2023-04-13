Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Advanced Configuration Options for One Cluster

Share Feedback

On this page

  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/processArgs  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier for the project containing the cluster you want to retrieve.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the cluster to retrieve.  
  
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
  
defaultReadConcern

|

string

|

Default level of acknowledgment requested from MongoDB for read operations set
for this cluster.

MongoDB 4.4 clusters default to available.  
  
defaultWriteConcern

|

string

|

Default level of acknowledgment requested from MongoDB for write operations
set for this cluster.

MongoDB 4.4 clusters default to 1.  
  
failIndexKeyTooLong

|

boolean

|

Flag that indicates whether you can insert or update documents where all
indexed entries don't exceed 1024 bytes. If you set this to `false`, `mongod`
writes documents that exceed this limit but _doesn't_ index them.

This option corresponds to the `failIndexKeyTooLong` `mongod` parameter.  
  
javascriptEnabled

|

boolean

|

Flag that indicates whether the cluster allows execution of operations that
perform server-side executions of JavaScript.

  * If your cluster runs a MongoDB version less than 4.4, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` in the cluster.

  * If your cluster runs MongoDB version 4.4 or greater, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` and `mongos` in the cluster.

  
  
minimumEnabledTlsProtocol

|

string

|

Minimum Transport Layer Security (TLS) version that the cluster accepts for
incoming connections. Clusters using TLS 1.0 or 1.1 should consider setting
TLS 1.2 as the minimum TLS protocol version.

To learn more, see What versions of TLS does Atlas support?.

This option corresponds to the `net.ssl.disabledProtocols` `mongod`
configuration file option.  
  
noTableScan

|

boolean

|

Flag that indicates whether the cluster disables executing any query that
requires a collection scan to return results.

This option corresponds to the `notablescan` `mongod` parameter.  
  
oplogSizeMB

|

integer

|

Storage limit of cluster's oplog expressed in megabytes. A value of `null`
indicates that the cluster uses the default oplog size that Atlas calculates.

To check the oplog size:

  1. Connect to your cluster via `mongosh`.

  2. Authenticate as a user with the `Atlas admin` role.

  3. Run the `rs.printReplicationInfo()` method to view the current oplog size and time.

This option corresponds to the `replication.oplogSizeMB` `mongod`
configuration file option.  
  
sampleSizeBIConnector

|

integer

|

Number of documents per database to sample when gathering schema information.

This parameter corresponds to the sampleSize mongosqld option.  
  
sampleRefreshIntervalBIConnector

|

integer

|

Interval in seconds at which the mongosqld process re-samples data to create
its relational schema.

This parameter corresponds to the sampleRefreshIntervalSecs mongosqld option.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
         --include --digest \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/LogData/processArgs"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "defaultReadConcern": "available",  
    3|   "defaultWriteConcern": "1",  
    4|   "failIndexKeyTooLong": true,  
    5|   "javascriptEnabled": true,  
    6|   "minimumEnabledTlsProtocol": "TLS1_1",  
    7|   "noTableScan": false,  
    8|   "oplogSizeMB": 1000  
    9| }  
  
What is MongoDB Atlas? →

