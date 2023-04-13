Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update All User-Defined Analyzers for a Cluster

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Parameters
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

This API request creates new user-defined Atlas Search analyzers and replaces
existing ones. If you have any user-defined analyzers for your Atlas Search
index, they will be replaced by the new analyzer or analyzers specified in
this request.

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

    
    
    PUT /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/analyzers  
      
  
To delete all existing user-defined analyzers from your cluster, send a `PUT`
request to this endpoint with an empty array as the payload.

## Warning

Issuing a `PUT` request to this API endpoint overwrites any existing user-
definied Atlas Search analyzers.

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

Name of the cluster containing the collection with one or more Atlas Search
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

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`baseAnalyzer`

|

string

|

Required

|

Analyzer on which the user-defined analyzer is based.  
  
`ignoreCase`

|

boolean

|

Optional

|

Specify whether the index is case-sensitive.  
  
`maxTokenLength`

|

integer

|

Optional

|

Longest text unit to analyze. Atlas Search excludes anything longer from the
index.  
  
`name`

|

string

|

Required

|

Name of the user-defined analyzer.  
  
`stemExclusionSet`

|

array of strings

|

Optional

|

Words to exclude from stemming by the language analyzer.  
  
`stopwords`

|

array of strings

|

Optional

|

Strings to ignore when creating the index.  
  
## Response Elements

The HTTP response returns a JSON document that includes an array of analyzer
definitions. An analyzer definition contains some or all of the following
elements:

Name

|

Type

|

Description  
  
||  
  
`baseAnalyzer`

|

string

|

Analyzer on which the user-defined analyzer is based.  
  
`ignoreCase`

|

boolean

|

Specify whether the index is case-sensitive.  
  
`maxTokenLength`

|

integer

|

Longest text unit to analyze. Atlas Search excludes anything longer from the
index.  
  
`name`

|

string

|

Name of the user-defined analyzer.  
  
`stemExclusionSet`

|

array of strings

|

Words to exclude from stemming by the language analyzer.  
  
`stopwords`

|

array of strings

|

Strings to ignore when creating the index.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
    |  
    2|       --digest  \  
    3|       --header "Accept: application/json"  \  
    4|       --header "Content-Type: application/json"  \  
    5|       --request PUT "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/fts/analyzers" \  
    6|       --data '[  
    7|          {  
    8|            "name": "my_new_analyzer",  
    9|            "baseAnalyzer": "lucene.standard",  
    10|            "maxTokenLength": 48  
    11|          },  
    12|          {  
    13|            "name": "my_other_new_analyzer",  
    14|            "baseAnalyzer": "lucene.english",  
    15|            "stopwords": [  
    16|              "foo",  
    17|              "bar",  
    18|              "baz"  
    19|            ]  
    20|          }  
    21|        ]'  
  
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

The following example response contains an array of two analyzer definitions.

    
    
    1| [  
    |  
    2|   {  
    3|     "name": "my_new_analyzer",  
    4|     "baseAnalyzer": "lucene.standard",  
    5|     "maxTokenLength": 48  
    6|    },  
    7|    {  
    8|      "name": "my_other_new_analyzer",  
    9|      "baseAnalyzer": "lucene.english",  
    10|      "stopwords": [  
    11|        "foo",  
    12|        "bar",  
    13|        "baz"  
    14|      ]  
    15|    }  
    16|  ]  
  
What is MongoDB Atlas? →

