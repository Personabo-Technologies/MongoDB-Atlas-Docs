Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create an Atlas Search Index

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Examples
  * Example Request
  * Example Response
  * Example Request
  * Example Response

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

For more information about Atlas Search indexes, see What is MongoDB Atlas
Search? and Review Atlas Search Index Syntax.

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

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes  
      
  
## Note

You cannot create an Atlas Search index on any collection in the `admin`,
`local`, or `config` databases in any cluster.

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

Unique identifier for the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

string

|

Required

|

Name of the cluster that contains the collection on which you want to create
an Atlas Search index.  
  
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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`analyzer`

|

string

|

Optional

|

Analyzer to use when creating the index. Defaults to lucene.standard.  
  
`analyzers`

|

array of BSON objects

|

Optional

|

Custom analyzers to use in this index.  
  
`collectionName`

|

string

|

Required

|

Name of the collection the index is on.  
  
`database`

|

string

|

Required

|

Name of the database the collection is in.  
  
`mappings`

|

object

|

Required

|

Object containing index specifications for the collection fields.  
  
`mappings`

`.dynamic`

|

boolean

|

Conditional

|

Required if `mappings.fields` is omitted.

Indicates whether the index uses dynamic or static mappings. For dynamic
mapping, set the value to `true`. For static mapping, specify the fields to
index using `mappings.fields`.  
  
`mappings`

`.fields`

|

object

|

Conditional

|

Required if `mappings.dynamic` is `false` or is omitted.

Object containing one or more field specifications.  
  
`name`

|

string

|

Required

|

Name of the index.  
  
`searchAnalyzer`

|

string

|

Optional

|

Analyzer to use when searching the index. Defaults to lucene.standard.  
  
`synonyms`

|

array of documents

|

Optional

|

Synonyms mapping definition to use in this index.  
  
`synonyms[i]`

`.analyzer`

|

string

|

Required

|

Name of the analyzer to use with this synonym mapping. If you set
`mappings.dynamic` to `true`, you must use the default analyzer,
lucene.standard, here also. Atlas Search doesn't support these custom analyzer
tokenizers and token filters in the index definition for synonyms:

  * nGram tokenizer

  * edgeGram tokenizer

  * daitchMokotoffSoundex token filter

  * nGram token filter

  * edgeGram token filter

  * shingle token filter

  
  
`synonyms[i]`

`.name`

|

string

|

Required

|

Name of the synonym mapping definition. Name must be unique in this index
definition and it can't be an empty string.  
  
`synonyms[i]`

`.source`

|

document

|

Required

|

Collection details for this synonym mapping definition.  
  
`synonyms[i]`

`.source`

`.collection`

|

string

|

Required

|

Name of the source MongoDB collection for the synonyms. Documents in this
collection must be in the format described in the Synonyms Source Collection
Documents.  
  
## Response Elements

The HTTP response returns a JSON document with an index definition for the
newly created index. An index definition contains the following elements:

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
  
## Examples

Basic Example

Synonyms Example

The following example contains an index definition for an index named
`default`. This is the default definition with dynamic mappings for all fields
in the `fiscalYear2018.orders` collection.

### Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Content-Type: application/json" \  
    3|      --include \  
    4|      --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/indexes?pretty=true" \  
    5|      --data '{  
    6|          "collectionName": "orders",  
    7|          "database": "fiscalYear2018",  
    8|          "mappings": {  
    9|            "dynamic": true  
    10|          },  
    11|          "name": "default"  
    12|        }'  
  
### Example Response

#### Response Header

    
    
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
  
#### Response Body

    
    
    1| {  
    |  
    2|   "collectionName" : "orders",  
    3|   "database" : "fiscalYear2018",  
    4|   "indexID" : "5d12990380eef5303341accd",  
    5|   "mappings" : {  
    6|     "dynamic" : true  
    7|   },  
    8|   "name" : "default"  
    9| }  
  
What is MongoDB Atlas? →

