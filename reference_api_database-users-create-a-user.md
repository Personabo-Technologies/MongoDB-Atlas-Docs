Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Database User

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

The Atlas Administration API uses HTTP Digest Authentication. Provide your
Atlas username as the username and Atlas Administration API key as the
password as part of the HTTP request.

This endpoint requires that the Atlas user has the `Owner` role. To view the
available Atlas users, click on Users & Teams in the left-hand navigation.

For complete documentation on configuring API access for an Atlas project, see
Get Started with the Atlas Administration API.

Atlas supports a maximum of 100 database users per Atlas project. If you
require more than 100 database users on a project, contact Atlas support.

The parameters that this resource requires depend upon the authentication
mechanism the database uses. Select from one of the following authentication
mechanisms:

SCRAM-SHA

X.509

LDAP

AWS IAM

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/databaseUsers  
      
  
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

Unique 24-hexadecimal string that identifies the project.  
  
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

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
databaseName

|

string

|

Required

|

Database against which the database user authenticates. Database users must
provide both a username and authentication database to log into MongoDB.

You may set this parameter value as:

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

Optional

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas deletes
the database user. The specified date must be in the future and within one
week of the time you make the API request.

## Note

You may include an ISO 8601 time zone designator to ensure that the expiration
date occurs with respect to the local time in the specified time zone.  
  
labels

|

array

|

Optional

|

List that contains key-value pairs that tag and categorize the database user.

Each key and value has a maximum length of 255 characters.

    
    
    | "labels": [  
      
       {  
         "key": "example key",  
         "value": "example value"  
       }  
     ]  
  
## Note

The **labels** you define are not visible in the Atlas console. They are
returned in the response body when you use the Atlas Administration API to get
one, get all, or update one database user.  
  
groupId

|

string

|

Required

|

Unique 24-hexadecimal string that identifies the project to which the database
user belongs.  
  
roles

|

array

|

Required

|

Array of this user's roles and the databases / collections on which the roles
apply. A role allows the user to perform particular actions on the specified
database. A role on the `admin` database can include privileges that apply to
the other databases as well.

## Note

The available privilege actions for custom roles support a subset of MongoDB
commands. See Unsupported Commands in `M10+` Clusters for more information.  
  
roles.collectionName

|

string

|

Optional

|

Collection on which the database user has the specified role.

You can specify a collection for the `read` and `readWrite` roles. If you do
not specify a collection for `read` and `readWrite`, the role applies to all
collections in the database (excluding some collections in the `system.`
database).

## Note

The following table describes the Atlas specific privileges, the database it
applies to, and the privilege actions they represent.

|

Atlas Specific Privilege

|

Database

|

Privilege Actions  
  
||  
  
`backup`

|

`admin`

|

  * `listDatabases`

  * `listCollections`

  * `listIndexes`

  * `appendOplogNote`

  * `getParameter`

  * `serverStatus`

  
  
`clusterMonitor`

|

`admin`

|

  * `checkFreeMonitoringStatus`

  * `connPoolStats`

  * `getCmdLineOpts`

  * `getDefaultRWConcern`

  * `getLog`

  * `getParameter`

  * `getShardMap`

  * `hostInfo`

  * `inprog`

  * `listDatabases`

  * `listSessions`

  * `listShards`

  * `netstat`

  * `replSetGetConfig`

  * `replSetGetStatus`

  * `serverStatus`

  * `setFreeMonitoring`

  * `shardingState`

  * `top`

  
  
`dbAdmin`

|

User configured

|

  * `bypassDocumentValidation`

  * `changeStream`

  * `collMod`

  * `collStats`

  * `compact`

  * `convertToCapped`

  * `createCollection`

  * `createIndex`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `dropDatabase`

  * `dropIndex`

  * `enableProfiler`

  * `find`

  * `killCursors`

  * `listCollections`

  * `listIndexes`

  * `planCacheIndexFilter`

  * `planCacheRead`

  * `planCacheWrite`

  * `reIndex`

  * `renameCollectionSameDB`

  * `storageDetails`

  * `validate`

  
  
`dbAdminAnyDatabase`

|

User configured except `local` and `config`

|

  * `dbAdminAnyDatabase`

  
  
`enableSharding`

|

|

  * `enableSharding`

  
  
`read`

|

User configured

|

  * `changeStream`

  * `collStats`

  * `dbHash`

  * `dbStats`

  * `find`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  
  
`readWrite`

|

User configured

|

  * `changeStream`

  * `collStats`

  * `convertToCapped`

  * `createCollection`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `createIndex`

  * `dropIndex`

  * `find`

  * `insert`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `remove`

  * `renameCollectionSameDB`

  * `update`

  
  
`killOpSession`

|

User configured

|

  * `inprog`

  * `killop`

  * `killAnySession`

  * `listSessions`

  
  
`readWriteAnyDatabase`

|

User configured except `local` and `config`

|

  * `readWriteAnyDatabase`

  * `changeStream`

  * `collStats`

  * `convertToCapped`

  * `createCollection`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `createIndex`

  * `dropIndex`

  * `find`

  * `insert`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `listDatabases`

  * `remove`

  * `renameCollectionSameDB`

  * `update`

  
  
`readAnyDatabase`

|

User configured except `local` and `config`

|

  * `readAnyDatabase`

  * `changeStream`

  * `collStats`

  * `dbHash`

  * `dbStats`

  * `find`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `listDatabases`

  
  
roles.databaseName

|

string

|

Optional

|

Database on which the database user has the specified role. A role on the
`admin` database can include privileges that apply to the other databases.  
  
roles.roleName

|

string

|

Required

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

Optional

|

List of clusters and Atlas Data Lakes that this user can access. Returns an
empty array if the database user has access to all the clusters and Atlas Data
Lakes in the project. Atlas grants database users access to all resources by
default.

    
    
    | "scopes": [  
      
      {  
        "name": <resource-name>,  
        "type": "CLUSTER"|"DATA_LAKE"  
      }  
    ]  
  
scopes.name

|

string

|

Required

|

Name of the cluster or Atlas Data Lake that the database user can access.  
  
scopes.type

|

string

|

Required

|

Type of resource that the database user can access. This parameter returns one
of the following values:

  * `CLUSTER`

  * `DATA_LAKE`

  
  
username

|

string

|

Required

|

Username needed to authenticate to the MongoDB database or collection.

SCRAM-SHA

X.509

LDAP

AWS IAM

An alphanumeric string  
  
SCRAM-SHA

X.509

LDAP

AWS IAM

|

|

|  
  
|||  
  
password

|

string

|

Conditional

|

Alphanumeric string that authenticates the database user against the database
specified in **databaseName**.  
  
### Response Elements

If you set the query element `"envelope" : true`, this resource wraps the
response in a `content` object.

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

SCRAM-SHA

X.509

LDAP

AWS IAM

Create a database user that Atlas authenticates using SCRAM-SHA and the
`admin` database.

## Important

You must modify the following code block with the appropriate credentials and
project ID.

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --include \  
    5|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/databaseUsers" \  
    6|      --data '  
    7|        {  
    8|          "databaseName": "admin",  
    9|          "password": "changeme123",  
    10|          "roles": [{  
    11|            "databaseName": "sales",  
    12|            "roleName": "readWrite"  
    13|          }, {  
    14|            "databaseName": "marketing",  
    15|            "roleName": "read"  
    16|          }],  
    17|          "scopes": [{  
    18|            "name": "myCluster",   
    19|            "type": "CLUSTER"  
    20|          }],  
    21|          "username": "david"  
    22|        }'  
  
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

SCRAM-SHA

X.509

LDAP

AWS-IAM

    
    
    1| {  
    |  
    2|   "databaseName": "admin",  
    3|   "groupId": "{GROUP-ID}",  
    4|   "labels": [],  
    5|   "ldapAuthType": "NONE",  
    6|   "links": [  
    7|     {  
    8|       "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/databaseUsers/admin/david",  
    9|       "rel": "self"  
    10|     }  
    11|   ],  
    12|   "roles": [  
    13|     {  
    14|       "databaseName": "sales",  
    15|       "roleName": "readWrite"  
    16|     },  
    17|     {  
    18|       "databaseName": "marketing",  
    19|       "roleName": "read"  
    20|     }  
    21|   ],  
    22|   "scopes": [  
    23|     {  
    24|       "name": "myCluster",  
    25|       "type": "CLUSTER"  
    26|     }  
    27|   ],  
    28|   "username": "david",  
    29|   "x509Type": "NONE"  
    30| }  
  
What is MongoDB Atlas? →

