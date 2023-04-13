Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Rolling Index

Share Feedback

On this page

  * Syntax
  * Required Roles
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/index  
      
  
## Required Roles

You must have one of the following roles to successfully call this resource:

  * `Project Owner`

  * `Project Cluster Manager`

  * `Project Data Access Admin`

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

Unique identifier of the project which holds the cluster on which to create an
index.  
  
`CLUSTER-NAME`

|

Required.

|

The name of the cluster on which to create an index.  
  
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

|

Required  
  
|||  
  
`db`

|

string

|

The name of the database that holds the collection on which to create an
index.

|

Required  
  
`collection`

|

string

|

The name of the collection on which to create an index.

|

Required  
  
`keys`

|

array of objects

|

An array containing one or more objects in which the key is the field to be
indexed and the value is the type of the index. For more information on index
creation syntax, see the createIndex() shell method.

## Important

If you want to create a multikey index, you must list each field in its own
object within the `keys` object array. JSON does not guarantee item order, so
if you list multiple fields in the same object, the index may not build
correctly.

|

Required  
  
`options`

|

object

|

A document that contains a set of options that controls the creation of the
index. See Index Options for more information.

|

Optional  
  
`collation`

|

object

|

A document that contains a set of options to control index collation. See
Collation Options for more information.

|

Optional  
  
## Response

This endpoint returns an empty document.

## Example

### Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/index" \  
     --data '{  
               "db": "test",  
               "collection": "myCollection",  
               "keys": [{ "myField": 1 }],  
               "collation": { "locale": "en_US", "strength": 2 }  
             }'  
  
### Response

    
    
    {}  
      
  
What is MongoDB Atlas? →

