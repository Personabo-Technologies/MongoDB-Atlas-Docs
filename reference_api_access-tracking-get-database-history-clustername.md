Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Database Access History by Cluster Name

Share Feedback

On this page

  * Resource
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

Retrieve the access logs of a cluster by cluster name.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET /groups/{GROUP-ID}/dbAccessHistory/clusters/{CLUSTER-NAME}  
      
  
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

The unique identifier for the project.  
  
`CLUSTER-NAME`

|

Required.

|

The name of the cluster.  
  
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
  
|

|

|

|  
  
||||  
  
start

|

number

|

Optional

|

Timestamp in the number of milliseconds that have elapsed since the UNIX epoch
for the first entry that Atlas returns from the database access logs.

|

Current timestamp minus 7 days  
  
end

|

number

|

Optional

|

Timestamp in the number of milliseconds that have elapsed since the UNIX epoch
for the last entry that Atlas returns from the database access logs.

|

Current timestamp  
  
nLogs

|

number

|

Optional

|

Maximum number of log entries to return. Atlas accepts values between `0` and
`20000`, inclusive.

|

`20000`  
  
ipAddress

|

string

|

Optional

|

Single IP address that attempted to authenticate with the database. Atlas
filters the returned logs to include documents with only this IP address.

|  
  
authResult

|

Boolean

|

Optional

|

Flag that indicates whether to return either successful or failed
authentication attempts. When set to `true`, Atlas filters the log to return
only successful authentication attempts. When set to `false`, Atlas filters
the log to return only failed authentication attempts.

|  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`accessLogs`

|

object array

|

The authentication attempts made against the cluster. Each object is a
separate attempt.  
  
`authResult`

|

boolean

|

The result of the authentication attempt. Returns `true` if the authentication
request was successful. Returns `false` if the authentication request resulted
in failure.  
  
`authSource`

|

string

|

The database that the request attempted to authenticate against. Returns
`admin` if the authentication source for the user is `SCRAM-SHA`. Returns
`$external` if the authentication source for the user is LDAP.  
  
`failureReason`

|

string

|

The reason that the request failed to authenticate. Returns `null` if the
authentication request was successful.  
  
`groupId`

|

string

|

The unique identifier for the project.  
  
`hostname`

|

string

|

The hostname of the target node that received the authentication attempt.  
  
`clusterName`

|

string

|

The name associated with the cluster.  
  
`ipAddress`

|

string

|

The IP address that the authentication attempt originated from.  
  
`logLine`

|

string

|

The text of the server log concerning the authentication attempt.  
  
`timestamp`

|

string

|

The UTC timestamp of the authentication attempt.  
  
`username`

|

string

|

The username that attempted to authenticate.  
  
## Example Request

    
    
    curl --user "username:apiKey" --digest \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/571c390a7cea7e4dbf32b625/dbAccessHistory/clusters/cluster0?start=1564064082000&end=1564064082000&nLogs=2"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    {  
      
      "accessLogs": [  
        {  
          "authResult": true,  
          "authSource": "admin",  
          "failureReason": null,  
          "groupId": "571c390a7cea7e4dbf32b625",  
          "hostname": "cluster0-shard-00-00-c01ab.mongodb.net:27017",  
          "clusterName": "cluster0",  
          "ipAddress": "123.45.0.1",  
          "logLine": "2019-07-25T19:14:42.484+0000 I  ACCESS   [conn2167] Successfully authenticated as principal jon-snow on admin from client 123.45.0.1:8080",  
          "timestamp": "Sun Jul 25 9:14:42 EDT 2019",  
          "username": "jon-snow"  
        },  
        {  
          "authResult": false,  
          "authSource": "admin",  
          "failureReason": "UserNotFound: Could not find user \"jane-doe\" for db \"admin\"",  
          "groupId": "571c390a7cea7e4dbf32b625",  
          "hostname": "cluster0-shard-00-00-c01ab.mongodb.net:27017",  
          "clusterName": "cluster0",  
          "ipAddress": "123.45.2.2",  
          "logLine": "2019-07-25T19:13:39.316+0000 I  ACCESS   [conn1893] SASL SCRAM-SHA-1 authentication failed for jane-doe on admin from client 123.45.2.2:51842 ; UserNotFound: Could not find user \"jane-doe\" for db \"admin\"",  
          "timestamp": "Sun Jul 25 9:14:42 EDT 2019",  
          "username": "jane-doe"  
        }  
    ]}  
  
What is MongoDB Atlas? →

