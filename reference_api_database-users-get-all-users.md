Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Database Users

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/databaseUsers  
      
  
### Request Path Parameters

Parameter

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

Unique 24-hexadecimal string that identifies the project.  
  
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

### Response Elements

If you set the query element `"envelope" : true`, this resource wraps the
response in a `content` object.

#### Response Document

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
  
#### results Embedded Document

Response Element

|

Type

|

Description  
  
||  
  
databaseName

|

string

|

Database against which the database user authenticates. Database users must
provide both a username and authentication database to log into MongoDB.

This resource returns:

SCRAM-SHA

X.509

LDAP

AWS IAM

 **admin** if the database user authenticates with SCRAM-SHA.

If you don't set an authentication mechanism, Atlas defaults to **SCRAM-SHA**.  
  
deleteAfterDate

|

string

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas deletes
the database user. This resource returns this parameter if you set an
expiration date when creating the entry.  
  
groupId

|

string

|

Unique 24-hexadecimal string that identifies the project to which the database
user belongs.  
  
labels

|

array

|

List that contains key-value pairs that tag and categorize the database user.  
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
roles

|

array

|

Array of this user's roles and the databases / collections on which the roles
apply. A role allows the user to perform particular actions on the specified
database. A role on the `admin` database can include privileges that apply to
the other databases as well.  
  
roles.collectionName

|

string

|

Collection on which the database user has the specified role.  
  
roles.databaseName

|

string

|

Database on which the database user has the specified role. A role on the
**admin** database can include privileges that apply to the other databases.  
  
roles.roleName

|

string

|

Label given to a group of privileges assigned to a database user. This value
can either be a built-in role or a custom role.

The **admin** database accepts these values for the **role** parameter:

  * `atlasAdmin`

  * `readWriteAnyDatabase`

  * `readAnyDatabase`

  * `clusterMonitor`

  * `backup`

  * `dbAdminAnyDatabase`

  * `enableSharding`

Atlas limits this role to MongoDB databases that it manages. The role allows
the user to enable sharding on a database and to shard a collection.

Specific databases accept these values for the **role** parameter:

  * `dbAdmin`

  * `read`

  * `readWrite`

Specific collections accept these values for the **role** parameter:

  * `read`

  * `readWrite`

If you don't specify a collection for the `read` and `readWrite` roles, Atlas
applies the roles to all collections (excluding some `system.` collections) in
the database.

## Note

You can only set a custom role when you set `"roles.databaseName" : "admin"`.  
  
scopes

|

array

|

List of clusters and Atlas Data Lakes that this user can access. Returns an
empty array if the database user has access to all the clusters and Atlas Data
Lakes in the project. Atlas grants database users access to all resources by
default.  
  
scopes.name

|

string

|

Name of the cluster or Atlas Data Lake that the database user can access.  
  
scopes.type

|

string

|

Type of resource that the database user can access. This parameter returns one
of the following values:

  * `CLUSTER`

  * `DATA_LAKE`

  
  
username

|

string

|

Username needed to authenticate to the MongoDB database or collection. This
resource returns:

SCRAM-SHA

X.509

LDAP

AWS IAM

An alphanumeric string  
  
SCRAM-SHA

X.509

LDAP

AWS IAM

## Example Request

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794dee37132bb7b/databaseUsers?pretty=true"  
  
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
    2|   "links" : [ ],  
    3|   "results" : [  
    4|     {  
    5|       "databaseName" : "admin",  
    6|       "groupId" : "5356823b3794dee37132bb7b",  
    7|       "labels" : [],  
    8|       "links" : [ ],  
    9|       "roles" : [ {  
    10|         "databaseName" : "staging",  
    11|         "roleName" : "readWrite"  
    12|       }, {  
    13|         "databaseName" : "production",  
    14|         "roleName" : "read"  
    15|       } ],  
    16|       "scopes": [],  
    17|       "username" : "susan"  
    18|     }  
    19|   ],  
    20|   "totalCount" : 1  
    21| }  
  
What is MongoDB Atlas? →

