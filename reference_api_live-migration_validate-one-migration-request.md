Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Validate One Migration Request

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

Create one new validation request for the push live migration job.

## Required Roles

Your API Key must have the `Organization Owner` role to successfully call this
resource.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{groupId}/liveMigrations/validate  
      
  
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

Unique 24-hexadecimal digit string that identifies your project.  
  
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
  
source

|

object

|

Required

|

Document that describes the Cloud Manager or Ops Manager source of the
migrating cluster.  
  
source.clusterName

|

string

|

Required

|

Human-readable label that identifies the source Cloud Manager or Ops Manager
cluster.  
  
source.groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the source project.  
  
source.username

|

string

|

Optional

|

Human-readable label that identifies the SCRAM-SHA user that connects to the
source Cloud Manager or Ops Manager cluster. Omit this value if
**"source.managedAuthentication" : true**.  
  
source.password

|

string

|

Optional

|

Password that authenticates the username to the source Cloud Manager or Ops
Manager cluster. Omit this value if **"source.managedAuthentication" : true**.  
  
source.ssl

|

boolean

|

Required

|

Flag that indicates whether you have TLS enabled.  
  
source.caCertificatePath

|

string

|

Optional

|

Path to the CA certificate that signed TLS certificates use to authenticate to
the source Cloud Manager or Ops Manager cluster. Omit this value if
**"source.ssl" : false**.  
  
source.managedAuthentication

|

boolean

|

Required

|

Flag that indicates whether MongoDB Automation manages authentication to the
source Cloud Manager or Ops Manager cluster. If you set this to **true** ,
don't provide values for **source.username** and **source.password**.  
  
destination

|

object

|

Required

|

Settings that describe the Atlas destination of the migrating Cloud Manager or
Ops Manager cluster.  
  
destination.groupId

|

string

|

Required

|

Unique 24-hexadecimal digit string that identifies the Atlas destination
project.  
  
destination.clusterName

|

string

|

Required

|

Human-readable label that identifies the Atlas destination cluster.  
  
migrationHosts

|

array

|

Required

|

List of hosts running the MongoDB Agent that can transfer your MongoDB data
from the source (Cloud Manager or Ops Manager) to destination (Atlas)
deployments. Each live migration process uses its own dedicated migration
host.  
  
dropEnabled

|

boolean

|

Required

|

Flag that indicates whether this process should drop existing collections from
the destination (Atlas) cluster given in **destination.clusterName** before
starting the migration of data from the source cluster.  
  
## Response

Name

|

Type

|

Description  
  
||  
  
_id

|

string

|

Unique 24-hexadecimal digit string that identifies this process validating the
live migration.  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the Atlas project to
validate.  
  
status

|

string

|

State of the validation job when you submitted this request. Returns
`"PENDING"`, `"SUCCESS"`, or `"FAILED"`.  
  
sourceGroupId

|

string

|

Unique 24-hexadecimal digit string that identifies the source (Cloud Manager
or Ops Manager) project.  
  
errorMessage

|

string

|

Reason why the validation job failed.  
  
## Example Request

    
    
    curl --user '{USERNAME}:{APIKEY}' --digest \  
      
         --header 'Accept: application/json' \  
         --header 'Content-Type: application/json' \  
         --include \  
         --request POST 'https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/liveMigrations/validate?pretty=true' \  
         --data '{  
             "source": {  
               "clusterName": "exampleClusterA",  
               "groupId": "9b43a5b329223c3a1591a678",  
               "username": "example",  
               "password": "string",  
               "ssl": true,  
               "caCertificatePath": "/path/to/ca",  
               "managedAuthentication" : false  
             },  
             "destination": {  
               "groupId": "e01c9427f054fe80745f3f6c",  
               "clusterName": "exampleClusterB"  
             },  
             "migrationHosts": [ "vm001.example.com" ],  
             "dropEnabled": true  
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

    
    
    {  
      
      "_id": "a659ce44c03ca1e348b1e992",  
      "groupId": "e01c9427f054fe80745f3f6c",  
      "sourceGroupId": "9b43a5b329223c3a1591a678",  
      "status": "PENDING"  
    }  
  
What is MongoDB Atlas? →

