Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Atlas Search Index

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `fts` resource allows you to retrieve and edit Atlas Search analyzers and
index configurations for the specified cluster.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Required Roles

The following table shows the modes of access each role supports.

Role

|

Action

|

Atlas UI

|

Atlas API

|

Atlas Search API

|

Atlas CLI  
  
|||||  
  
`Project Data Access Read Only` or higher role

|

To view Atlas Search analyzers and indexes.

|

✓

|

✓

|

|  
  
`Project Data Access Admin` or higher role

|

To create and manage Atlas Search analyzers and indexes, and assign the role
to your API Key.

|

✓

|

✓

|

✓

|

✓  
  
`Project Owner` role

|

To create and assign project access to API Keys.

|

|

|

✓

|

✓  
  
`Organization Owner` role

|

To create access list entries for your API Key and send the request from a
client that appears in the access list for your API Key.

|

|

|

✓

|

✓  
  
`Project Search Index Editor`

|

To create, view, edit, and delete Atlas Search indexes using the Atlas UI or
API.

|

✓

|

✓

|

✓

|  
  
## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

The unique identifier for the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

string

|

Required

|

The name of the cluster containing the collection with one or more Atlas
Search indexes.  
  
`INDEX-ID`

|

string

|

Required

|

The unique identifier of the Atlas Search index. Use the Get All Atlas Search
Indexes for a Collection API endpoint to find the IDs of all Atlas Search
indexes.  
  
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

## Response Elements

The HTTP response returns a JSON document with an index definition for the
specified index. An index definition contains the following elements:

Name

|

Type

|

Description  
  
||  
  
`analyzer`

|

Optional

|

Analyzer used when creating the index.  
  
`analyzers`

|

Optional

|

Custom analyzers used in this index.  
  
`collectionName`

|

string

|

Name of the collection the index is on.  
  
`database`

|

string

|

Name of the database the collection is in.  
  
`indexID`

|

string

|

Unique identifier for the index.  
  
`mappings`

|

object

|

Object containing index specifications for the collection fields.  
  
`mappings`

`.dynamic`

|

boolean

|

Flag indicating whether the index uses dynamic or static mappings.  
  
`mappings`

`.fields`

|

object

|

Object containing one or more field specifications.  
  
`name`

|

string

|

Name of the index.  
  
`searchAnalyzer`

|

string

|

Analyzer to use when searching the index.  
  
`status`

|

string

|

Status of the index. Value can be one of the following statuses:

  * `IN_PROGRESS` \- Atlas is building or re-building the index after an edit.

  * `STEADY` \- Index is ready to use.

  * `FAILED` \- Atlas could not build the index.

  * `MIGRATING` \- Atlas cluster tier is being upgraded and indexes are migrating.

  
  
`synonyms`

|

array of documents

|

Synonyms mapping definition used in this index.  
  
`synonyms[i]`

`.analyzer`

|

string

|

Name of the analyzer used in this synonym mapping. If `mappings.dynamic` is
`true`, Atlas Search uses the default analyzer, lucene.standard, for synonym
mapping.  
  
`synonyms[i]`

`.name`

|

string

|

Name of the synonym mapping.  
  
`synonyms[i]`

`.source`

|

document

|

Collection details for this synonym mapping definition.  
  
`synonyms[i]`

`.source`

`.collection`

|

string

|

Name of the source MongoDB collection for the synonyms.  
  
## Example

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes/{INDEX-ID}?pretty=true"  
  
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

The following example response contains an index definition for an index named
`SearchIndex1`. It is a custom definition with static mappings for two fields
named `genres` and `plot`.

    
    
    1| {  
    |  
    2|   "collectionName" : "movies",  
    3|   "database" : "sample_mflix",  
    4|   "indexID" : "5d1268a980eef518dac0cf41",  
    5|   "mappings" : {  
    6|     "dynamic" : false,  
    7|     "fields" : {  
    8|       "genres" : {  
    9|         "analyzer" : "lucene.standard",  
    10|         "type" : "string"  
    11|       },  
    12|       "plot" : {  
    13|         "analyzer" : "lucene.standard",  
    14|         "type" : "string"  
    15|       }  
    16|     }  
    17|   },  
    18|  "name" : "SearchIndex1",  
    19|  "status" : "STEADY"  
    20| }  
  
What is MongoDB Atlas? →

