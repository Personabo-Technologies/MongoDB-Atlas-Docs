Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return All Serverless Instances

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Returns all serverless instances in the specified project.

## Required Roles

Your API Key must have the `Project Read Only` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{groupId}/serverless  
      
  
### Request Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the project that contains
your serverless instance.  
  
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

This endpoint doesn't use HTTP request body parameters.

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

Each element in the **result** array is one serverless instance.

Name

|

Type

|

Description  
  
||  
  
connectionStrings

|

object

|

Set of connection strings that your applications use to connect to this
serverless instance. This resource returns this object after the serverless
instance finishes deploying, not during the serverless instance deployment.  
  
connectionStrings.standardSrv

|

string

|

Public `mongodb+srv://` connection string that you can use to connect to this
serverless instance.  
  
createDate

|

string

|

Timestamp that indicates when MongoDB Cloud created the serverless instance.
The timestamp displays in the ISO 8601 date and time format in UTC.  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the project that contains
the serverless instance.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the serverless instance.  
  
mongoDBVersion

|

string

|

Version of MongoDB that the serverless instance runs, in `<major
version>.<minor version>` format.  
  
name

|

string

|

Human-readable label that identifies the serverless instance.  
  
providerSettings

|

object

|

Group of settings that configure the provisioned MongoDB database.  
  
providerSettings.backingProviderName

|

string

|

Cloud service provider on which MongoDB Cloud provisioned the serverless
instance.  
  
providerSettings.providerName

|

string

|

This value will always be the string literal `SERVERLESS`.  
  
providerSettings.regionName

|

string

|

Human-readable label that identifies the physical location of your MongoDB
serverless instance. The region you choose can affect network latency for
clients accessing your databases.  
  
serverlessBackupOptions.serverlessContinuousBackupEnabled

|

boolean

|

Flag that indicates whether the serverless instance uses Serverless Continuous
Backup. If this parameter is `false`, the serverless instance uses Basic
Backup.

|

Option

|

Description  
  
|  
  
Serverless Continuous Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and lets you restore the data from a selected point in time
within the last 72 hours. Atlas also takes daily snapshots and retains these
daily snapshots for 35 days. To learn more, see Serverless Instance Costs.  
  
Basic Backup

|

Atlas takes incremental snapshots of the data in your serverless instance
every six hours and retains only the two most recent snapshots. You can use
this option for free.  
  
stateName

|

string

|

Stage of deployment of this serverless instance when the resource made its
request.  
  
## Example Request

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
         --header 'Content-Type: application/json' \  
         --include \  
         --request GET 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless?pretty=true'  
  
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
    2|   "links" : [ {  
    3|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless?pretty=true&pageNum=1&itemsPerPage=100",  
    4|     "rel" : "self"  
    5|   } ],  
    6|   "results" : [ {  
    7|     "connectionStrings" : {  
    8|       "standardSrv" : "mongodb+srv://instance1.example.com"  
    9|     },  
    10|     "createDate" : "2021-06-25T21:32:06Z",  
    11|     "groupId" : "{groupId}",  
    12|     "id" : "{instance1}",  
    13|     "links" : [ {  
    14|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}",  
    15|       "rel" : "self"  
    16|     }, {  
    17|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}/backup/restoreJobs",  
    18|       "rel" : "http://cloud.mongodb.com/restoreJobs"  
    19|     }, {  
    20|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}/backup/snapshots",  
    21|       "rel" : "http://cloud.mongodb.com/snapshots"  
    22|     } ],  
    23|     "mongoDBVersion" : "5.0.0",  
    24|     "name" : "{instanceName1}",  
    25|     "providerSettings" : {  
    26|       "providerName" : "SERVERLESS",  
    27|       "backingProviderName" : "AWS",  
    28|       "regionName" : "US_EAST_1"  
    29|     },  
    30|     "stateName" : "IDLE"  
    31|   }, {  
    32|     "connectionStrings" : {  
    33|       "standardSrv" : "mongodb+srv://instance2.example.com"  
    34|     },  
    35|     "createDate" : "2021-06-25T21:31:10Z",  
    36|     "groupId" : "{groupId}",  
    37|     "id" : "{instance2}",  
    38|     "links" : [ {  
    39|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName2}",  
    40|       "rel" : "self"  
    41|     }, {  
    42|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName2}/backup/restoreJobs",  
    43|       "rel" : "http://cloud.mongodb.com/restoreJobs"  
    44|     }, {  
    45|       "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName2}/backup/snapshots",  
    46|       "rel" : "http://cloud.mongodb.com/snapshots"  
    47|     } ],  
    48|     "mongoDBVersion" : "5.0.0",  
    49|     "name" : "{instanceName2}",  
    50|     "providerSettings" : {  
    51|       "providerName" : "SERVERLESS",  
    52|       "backingProviderName" : "AWS",  
    53|       "regionName" : "US_EAST_1"  
    54|     },  
    55|     "serverlessBackupOptions" : {  
    56|       "serverlessContinuousBackupEnabled" : true  
    57|     },  
    58|     "stateName" : "IDLE"  
    59|   } ],  
    60|   "totalCount" : 2  
    61| }  
  
What is MongoDB Atlas? →

