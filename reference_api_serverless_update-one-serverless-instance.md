Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Serverless Instance

Share Feedback

On this page

  * Required Roles
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

Serverless instances don't support some Atlas features at this time.

To learn more, see Serverless Instance Limitations.

Updates one serverless instance in the specified project.

## Required Roles

Your API Key must have the `Organization Owner` or `Project Owner` role to
successfully call this resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /groups/{groupId}/serverless/{instanceName}  
      
  
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

String

|

Required

|

Unique 24-hexadecimal digit string that identifies the target project for your
new serverless instance.  
  
instanceName

|

String

|

Required

|

Human-readable label that identifies your serverless instance.  
  
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
  
## Response

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
      
         --header 'Accept: application/json' \  
         --header 'Content-Type: application/json' \  
         --include \  
         --request PATCH 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/si0?pretty=true' \  
         --data '{  
             "serverlessBackupOptions" : {  
               "serverlessContinuousBackupEnabled" : true  
             }  
           }'  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "connectionStrings" : {  
    3|     "standardSrv" : "mongodb+srv://instanceName1.example.com"  
    4|   },  
    5|   "createDate" : "2021-06-25T21:31:10Z",  
    6|   "groupId" : "{groupId}",  
    7|   "id" : "{instance1}",  
    8|   "links" : [ {  
    9|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}",  
    10|     "rel" : "self"  
    11|   }, {  
    12|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}/backup/restoreJobs",  
    13|     "rel" : "http://cloud.mongodb.com/restoreJobs"  
    14|   }, {  
    15|     "href" : "http://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/serverless/{instanceName1}/backup/snapshots",  
    16|     "rel" : "http://cloud.mongodb.com/snapshots"  
    17|   } ],  
    18|   "mongoDBVersion" : "5.0.0",  
    19|   "name" : "{instanceName1}",  
    20|   "providerSettings" : {  
    21|     "providerName" : "SERVERLESS",  
    22|     "backingProviderName" : "AWS",  
    23|     "regionName" : "US_EAST_1"  
    24|   },  
    25|   "serverlessBackupOptions" : {  
    26|     "serverlessContinuousBackupEnabled" : true  
    27|   },  
    28|   "stateName" : "IDLE"  
    29| }  
  
What is MongoDB Atlas? →

