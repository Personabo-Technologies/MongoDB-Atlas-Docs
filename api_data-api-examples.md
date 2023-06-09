Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data API Examples

Share Feedback

On this page

  * Specify BSON Types in Requests
  * Binary
  * Date
  * Decimal128
  * Double
  * Int32
  * Int64
  * ObjectId
  * Query Examples
  * Find All Documents
  * Find Document by ID
  * Find By Date
  * Data Access Permissions
  * Define Permissions for Specific API Keys
  * Define Permissions for a Specific Collection

The following examples demonstrate how to send requests to the Atlas Data API.

## Specify BSON Types in Requests

Data API requests can specify BSON types that don't exist in JSON by instead
using the EJSON data format in the request body. You can use EJSON to match
BSON types in query filters or write BSON types in insert and update
operations.

To specify that a request body uses EJSON, set the `Content-Type` header:

    
    
    Content-Type: application/ejson  
      
  
### Binary

To specify a binary value, use `$binary` with the value encoded in Base64 and
a BSON subtype encoded as a two-character hexadecimal string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "data": {  
              "$binary": {  
                "base64": "46d989eaf0bde5258029534bc2dc2089",  
                "subType": "05"  
              }  
            }  
          }  
      }'  
  
### Date

To specify a date, use `$date` with the UNIX timestamp in milliseconds as a
64-bit integer:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "createdAt": { "$date": { "$numberLong": "1638551310749" } }  
          }  
      }'  
  
### Decimal128

To specify a 128-bit decimal, use `$numberDecimal` with the decimal value as a
string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "accountBalance": { "$numberDecimal": "128452.420523" }  
          }  
      }'  
  
### Double

To specify a 64-bit signed floating point value (commonly referred to as a
"double"), use `$numberDouble` with the integer value as a string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "temperatureCelsius": { "$numberDouble": "23.847" }  
          }  
      }'  
  
### Int32

To specify a 32-bit signed integer value, use `$numberInt` with the integer
value as a string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "coins": { "$numberInt": "2147483647" }  
          }  
      }'  
  
### Int64

To specify a 64-bit signed integer value, use `$numberLong` with the integer
value as a string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "population": { "$numberLong": "8047923148" }  
          }  
      }'  
  
### ObjectId

To specify an ObjectId value, use `$oid` with the ID as a byte string:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "document": {  
            "_id": { "$oid": "61f02ea3af3561e283d06b91" }  
          }  
      }'  
  
## Query Examples

The code snippets in this section demonstrate common patterns you can use in
your read and write operations.

### Find All Documents

To match all documents in a collection, use an empty query object:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/find' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "filter": {}  
      }'  
  
### Find Document by ID

MongoDB stores each document with a unique identifier in the `_id` field. For
most apps, this is a BSON ObjectID value. You can match any ObjectID field,
including a document using an EJSON `$oid` object:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/find' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "filter": {  
            "_id": { "$oid": "630e51b3f4cd7d9e606caab6" }  
          }  
      }'  
  
### Find By Date

You can match documents on a specific date by matching an EJSON `$date` object
with a field that contains a date value:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/find' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "filter": {  
            "createdAt": { "$date": { "$numberLong": "1661881925033" } }  
          }  
      }'  
  
You can query a range of dates with `$gt`, `$gte`, `$lt`, and `$lte`:

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/find' \  
      --header 'Content-Type: application/ejson' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "<cluster name>",  
          "database": "<database name>",  
          "collection": "<collection name>",  
          "filter": {  
            "createdAt": {  
              "$gte": { "$date": { "$numberLong": "1640995200000" } },  
              "$lt": { "$date": { "$numberLong": "1672531200000" } }  
            }  
          }  
      }'  
  
## Data Access Permissions

You can secure Data API requests using the underlying Atlas App's built-in
role-based permissions. The examples in this section demonstrate how to set up
common permissions schemes. You can mix and match these and more complex
schemes to meet your API's needs. For more examples and information on how
permissions work, see Role-based Permissions in the Atlas App Services docs.

### Define Permissions for Specific API Keys

You can define multiple roles with different data access permissions and
assign specific API keys to each role. For example, you can create a `read-
only` role that allows users to read all data but not insert, delete, or
modify data.

You map each role to an API key in the role's `apply_when` expression.

Each API key corresponds to a separate user account with a unique account ID.
You can access the account ID and other data of the user making a request with
the `%%user` expansion.

To associate a role with a single API key, set the `apply_when` expression to
match the API key's account ID:

apply_when - One user per role

    
    
    {  
      
      "database": "<database>",  
      "collection": "<collection>",  
      "roles": [  
        {  
           "name": "SpecificUser",  
           "apply_when": {  
             "%%user.id": "61f9a5e69cd3c0199dc1bb88"  
           },  
           "insert": true,  
           "delete": true,  
           "read": true,  
           "write": true  
        }  
      ],  
      "filters": []  
    }  
  
To associate a role with multiple API keys, set the `apply_when` expression to
match an array of API key account IDs:

apply_when - Multiple users per role

    
    
    {  
      
      "database": "<database>",  
      "collection": "<collection>",  
      "roles": [  
        {  
           "name": "MultipleUsers",  
           "apply_when": {  
             "%%user.id": {  
                "$in": [  
                  "61f9a5e69cd3c0199dc1bb88",  
                  "61f9a5e69cd3c0199dc1bb89"  
                ]  
             }  
           },  
           "insert": true,  
           "delete": true,  
           "read": true,  
           "write": true  
        }  
      ],  
      "filters": []  
    }  
  
You can also use a custom system to determine if a user has a role. For
example, you can write a function that looks up a user's roles from an Atlas
cluster.

functions/hasRole.js

    
    
    exports = async function hasRole({  
      
      userId, // The user account ID, e.g. "60d0c1bdee9d3c23b677f929"  
      roleName, // The name of a role the user might have, e.g. "admin"  
    }) {  
      // 1. Get a reference to a custom user data collection  
      const users = context.services.get("mongodb-atlas").db("app").collection("users")  
      // 2. Query the user's document and make sure it exists  
      const user = await users.findOne({ userId })  
      if(!user) {  
        console.error(`User.id ${userId} not found in custom user data collection`)  
        return false  
      }  
      // 3. Decide if the user has the role we're checking  
      return user.roles.includes(roleName)  
    };  
  
And then call that function from the role's `apply_when` expression with the
`%function` operator:

apply_when - Custom function

    
    
    {  
      
      "database": "<database>",  
      "collection": "<collection>",  
      "roles": [  
        {  
           "name": "SomeCustomRole",  
           "apply_when": {  
             "%%true": {  
               "%function": {  
                 "name": "hasRole",  
                 "arguments": [{  
                   "userId": "%%user.id",  
                   "roleName": "SomeCustomRole"  
                 }]  
               }  
             }  
           },  
           "insert": true,  
           "delete": true,  
           "read": true,  
           "write": true  
        }  
      ],  
      "filters": []  
    }  
  
This example uses a custom user data collection, but you can use any external
service to determine if a user has a role. The function code and arguments you
pass are up to you.

### Define Permissions for a Specific Collection

You can define roles that control data access permissions for a specific
collection in your cluster. For example, you can create a `read-only` role
that allows users to read all data in a collection but not insert, delete, or
modify any data.

To define roles for a specific collection, update the collection's
configuration file with the collection-specific role configurations:

/data_sources/<data source>/<database>/<collection>/rules.json

    
    
    {  
      
      "database": "<database>",  
      "collection": "<collection>",  
      "roles": [  
        {  
           "name": "IsOwner",  
           "apply_when": { "owner_id": "%%user.id" },  
           "insert": false,  
           "delete": false,  
           "read": true,  
           "write": true  
        }  
      ],  
      "filters": []  
    }  
  
If no collection roles match, then the request is also evaluated against the
data source's default roles. If you don't want to apply default roles, remove
any roles and filters from the default rule configuration file.

/data_sources/<data source>/default_rule.json

    
    
    {  
      
      "roles": [],  
      "filters": []  
    }  
  
← Data API ResourcesData API Data Formats →

