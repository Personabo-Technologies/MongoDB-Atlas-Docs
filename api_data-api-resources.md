Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data API Resources

Share Feedback

On this page

  * Base URL
  * Find a Single Document
  * Find Multiple Documents
  * Insert a Single Document
  * Insert Multiple Documents
  * Update a Single Document
  * Update Multiple Documents
  * Replace a Single Document
  * Delete a Single Document
  * Delete Multiple Documents
  * Run an Aggregation Pipeline
  * Error Codes

## Important

Each Atlas API has its own resources and requires initial setup. The Data API
also uses different access keys from the Atlas Administration API and the App
Services Admin API.

To learn more, see APIs.

## Base URL

All Data API endpoints have the following base URL, where `<Data API App ID>`
is a unique ID specific to each cluster:

    
    
    https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1  
      
  
### Regional Requests

If you deploy your data API to a local region, the base URL must include the
region name and cloud provider:

    
    
    https://<Region>.<Cloud>.data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1  
      
  
For a list of supported regions, see Deployment Models & Regions in the App
Services docs.

## Find a Single Document

### Endpoint

    
    
    POST /action/findOne  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/findOne' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": {  
            "text": "Do the dishes"  
          }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": <query filter>,  
      "projection": <projection>  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Optional

|

A MongoDB Query Filter. The `findOne` action returns the first document in the
collection that matches this filter.

If you do not specify a `filter`, the action matches all document in the
collection.

|

`{}`  
  
projection

|

object

|

Optional

|

A MongoDB Query Projection. Depending on the projection, the returned document
will either omit specific fields or include only specified fields or values

|

`{}`  
  
### Response

The `findOne` action returns the matched document in the `document` field:

    
    
    { "document": { "_id": "6193504e1be4ab27791c8133", "test": "foo" } }  
      
  
If the action does not match any documents, the `document` field is `null`:

    
    
    { "document": null }  
      
  
## Find Multiple Documents

### Endpoint

    
    
    POST /action/find  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/find' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": {  
            "status": "complete"  
          },  
          "sort": { "completedAt": 1 },  
          "limit": 10  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": <query filter>,  
      "projection": <projection>,  
      "sort": <sort expression>,  
      "limit": <number>,  
      "skip": <number>  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Optional

|

A MongoDB Query Filter. The `find` action returns documents in the collection
that match this filter.

If you do not specify a `filter`, the action matches all document in the
collection.

If the filter matches more documents than the specified `limit`, the action
only returns a subset of them. You can use `skip` in subsequent queries to
return later documents in the result set.

|

`{}`  
  
projection

|

object

|

Optional

|

A MongoDB Query Projection. Depending on the projection, the returned
documents either omit specific fields or include only specified fields and
values.

|

`{}`  
  
sort

|

object

|

Optional

|

A MongoDB Sort Expression. Matched documents are returned in ascending or
descending order of the fields specified in the expression.

|

`{}`  
  
limit

|

number

|

Optional

|

The maximum number of matched documents to include in the returned result set.
Each request may return up to 50,000 documents.

|

1000  
  
skip

|

number

|

Optional

|

The number of matched documents to skip before adding matched documents to the
result set.

|

0  
  
### Response

The `find` action returns an array of matched document in the `documents`
field:

    
    
    {  
      
      "documents": [  
        { "_id": "6193504e1be4ab27791c8133", ... },  
        { "_id": "6194604e1d38dc33792d8257", ... }  
      ]  
    }  
  
If the action does not match any documents, the `documents` field is an empty
array:

    
    
    { "documents": [] }  
      
  
## Insert a Single Document

### Endpoint

    
    
    POST /action/insertOne  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertOne' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "document": {  
            "status": "open",  
            "text": "Do the dishes"  
          }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "document": { ... },  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
document

|

object

|

Required

|

An EJSON document to insert into the collection.

|  
  
### Response

The `insertOne` action returns the `_id` value of the inserted document as a
string in the `insertedId` field:

    
    
    { "insertedId": "6193504e1be4ab27791c8133" }  
      
  
## Insert Multiple Documents

### Endpoint

    
    
    POST /action/insertMany  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/insertMany' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "documents": [  
            { "status": "open", "text": "Mop the floor" },  
            { "status": "open", "text": "Clean the windows" }  
          ]  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "documents": [{ ... }, ...]  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
documents

|

array of objects

|

Required

|

An array of one or more EJSON documents to insert into the collection.

|  
  
### Response

The `insertMany` action returns the `_id` values of all inserted documents as
an array of strings in the `insertedIds` field:

    
    
    { "insertedIds": ["61935189ec53247016a623c9", "61935189ec53247016a623ca"] }  
      
  
## Update a Single Document

### Endpoint

    
    
    POST /action/updateOne  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/updateOne' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": { "_id": { "$oid": "6193ebd53821e5ec5b4f6c3b" } },  
          "update": {  
              "$set": {  
                  "status": "complete",  
                  "completedAt": { "$date": { "$numberLong": "1637083942954" } }  
              }  
          }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": { ... },  
      "update": { ... },  
      "upsert": true|false  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Required

|

A MongoDB Query Filter. The `updateOne` action modifies the first document in
the collection that matches this filter.

|  
  
update

|

object

|

Required

|

A MongoDB Update Expression that specifies how to modify the matched document.

|  
  
upsert

|

boolean

|

Optional

|

The `upsert` flag only applies if no documents match the specified `filter`.
If `true`, the `updateOne` action inserts a new document that matches the
filter with the specified `update` applied to it.

|

false  
  
### Response

The `updateOne` action returns:

  * the number of documents that the filter matched in the `matchedCount` field

  * the number of matching documents that were updated in the `modifiedCount` field

    
    
    { "matchedCount": 1, "modifiedCount": 1 }  
      
  
If `upsert` is set to `true` and no documents match the filter, the action
returns the `_id` value of the inserted document as a string in the
`upsertedId` field:

    
    
    { "matchedCount": 0, "modifiedCount": 0, "upsertedId": "619353593821e5ec5b0f8944" }  
      
  
## Update Multiple Documents

### Endpoint

    
    
    POST /action/updateMany  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/updateMany' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": { "status": "open" },  
          "update": {  
              "$set": {  
                  "status": "complete",  
                  "completedAt": { "$date": { "$numberLong": "1637083942954" } }  
              }  
          }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": { ... },  
      "update": { ... },  
      "upsert": true|false  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Required

|

A MongoDB Query Filter. The `updateMany` action modifies all documents in the
collection that match this filter.

|  
  
update

|

object

|

Required

|

A MongoDB Update Expression that specifies how to modify matched documents.

|  
  
upsert

|

boolean

|

Optional

|

The `upsert` flag only applies if no documents match the specified `filter`.
If `true`, the `updateMany` action inserts a new document that matches the
filter with the specified `update` applied to it.

|

false  
  
### Response

The `updateMany` action returns:

  * the number of documents that the filter matched in the `matchedCount` field

  * the number of matching documents that were updated in the `modifiedCount` field

    
    
    { "matchedCount": 12, "modifiedCount": 12 }  
      
  
If `upsert` is set to `true` and no documents match the filter, the action
returns the `_id` value of the inserted document as a string in the
`upsertedId` field:

    
    
    { "matchedCount": 0, "modifiedCount": 0, "upsertedId": "619353593821e5ec5b0f8944" }  
      
  
## Replace a Single Document

### Endpoint

    
    
    POST /action/replaceOne  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/replaceOne' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": { "text": "Call Jessica" },  
          "replacement": {  
            "status": "open",  
            "text": "Call Amy"  
          }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": { ... },  
      "replacement": { ... },  
      "upsert": true|false  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Required

|

A MongoDB Query Filter. The `replaceOne` action overwrites the first document
in the collection that matches this filter.

|  
  
replacement

|

object

|

Required

|

An EJSON document that overwrites the matched document.

|  
  
upsert

|

boolean

|

Optional

|

The `upsert` flag only applies if no documents match the specified `filter`.
If `true`, the `replaceOne` action inserts the `replacement` document.

|

false  
  
### Response

The `replaceOne` action returns:

  * the number of documents that the filter matched in the `matchedCount` field

  * the number of matching documents that were replaced in the `modifiedCount` field

    
    
    { "matchedCount": 1, "modifiedCount": 1 }  
      
  
If `upsert` is set to `true` and no documents match the filter, the action
returns the `_id` value of the inserted document as a string in the
`upsertedId` field:

    
    
    { "matchedCount": 0, "modifiedCount": 0, "upsertedId": "619353593821e5ec5b0f8944" }  
      
  
## Delete a Single Document

### Endpoint

    
    
    POST /action/deleteOne  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/deleteOne' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": { "_id": { "$oid": "6193ebd53821e5ec5b4f6c3b" } }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": { ... }  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Required

|

A MongoDB Query Filter. The `deleteOne` action deletes the first document in
the collection that matches this filter.

|  
  
### Response

The `deleteOne` action returns the number of deleted documents in the
`deletedCount` field:

    
    
    { "deletedCount": 1 }  
      
  
## Delete Multiple Documents

### Endpoint

    
    
    POST /action/deleteMany  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/deleteMany' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "filter": { "status": "complete" }  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "filter": { ... }  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
filter

|

object

|

Required

|

A MongoDB Query Filter. The `deleteMany` action deletes all documents in the
collection that match this filter.

|  
  
### Response

The `deleteMany` action returns the number of deleted documents in the
`deletedCount` field:

    
    
    { "deletedCount": 42 }  
      
  
## Run an Aggregation Pipeline

### Endpoint

    
    
    POST /action/aggregate  
      
  
### Example

    
    
    curl --request POST \  
      
      'https://data.mongodb-api.com/app/<Data API App ID>/endpoint/data/v1/action/aggregate' \  
      --header 'Content-Type: application/json' \  
      --header 'api-key: <Data API Key>' \  
      --data-raw '{  
          "dataSource": "Cluster0",  
          "database": "todo",  
          "collection": "tasks",  
          "pipeline": [  
            {  
              "$group": {  
                "_id": "$status",  
                "count": { "$sum": 1 },  
                "text": { "$push": "$text" }  
              }  
            },  
            { "$sort": { "count": 1 } }  
          ]  
      }'  
  
### Request Body

    
    
    {  
      
      "dataSource": "<data source name>",  
      "database": "<database name>",  
      "collection": "<collection name>",  
      "pipeline": [<aggregation pipeline>]  
    }  
  
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
  
dataSource

|

string

|

Required

|

The name of the cluster.

|  
  
database

|

string

|

Required

|

The name of the database.

|  
  
collection

|

string

|

Required

|

The name of the collection.

|  
  
|

|

|

|  
  
||||  
  
pipeline

|

array of objects

|

Required

|

A MongoDB Aggregation Pipeline.

|  
  
### Response

The `aggregate` action returns the result set of the final stage of the
pipeline as an array of documents in the `documents` field:

    
    
    { "documents": [{ ... }, ...] }  
      
  
## Error Codes

Code

|

Description  
  
|  
  
400

|

Bad request

The request was invalid. This might mean:

  * A request header is missing.

  * The request body is malformed or improperly encoded.

  * A field has a value with an invalid type.

  * The specified data source is disabled or does not exist.

  * The specified database or collection does not exist.

  
  
401

|

Unauthorized

The request did not include an authorized and enabled Data API Key. Ensure
that your Data API Key is enabled for the cluster.  
  
404

|

Not found

The request was sent to an endpoint that does not exist.  
  
500s

|

Server errors

The Data API encountered an internal error and could not complete the request.  
  
← Read and Write with the Data APIData API Examples →

