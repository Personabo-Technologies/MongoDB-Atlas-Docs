Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Available Disks for a MongoDB Process

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Get all disks or partitions for the specified Atlas MongoDB process. A Atlas
MongoDB process can be either a `mongod` or `mongos`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Resource

    
    
    GET api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks  
      
  
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

Unique 24-hexadecimal digit string that identifies the project that owns this
Atlas MongoDB process.  
  
HOST

|

string

|

Required

|

Hostname, FQDN, IPv4 address, or IPv6 address of the machine running the Atlas
MongoDB process.  
  
PORT

|

number

|

Required

|

IANA port to which the Atlas MongoDB process listens.  
  
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

## Response Elements

### Response Document

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
  
### results Embedded Document

Name

|

Type

|

Description  
  
||  
  
partitionName

|

string

|

Name of the disk or partition. You can use this value to retrieve measurements
for the disk.  
  
links

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

Replace the information in brackets `{}` with your own Atlas information to
execute this example request:

    
    
    curl -u "<ATLAS-USERNAME>:<API-KEY>" --digest -i "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/processes/{HOST}:{PORT}/disks?pretty=true"  
      
  
## Example Response

    
    
    {  
      
       "links":[  
          {  
             "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/12345678/processes/shard-00-00.mongodb.net:27017/disks?pageNum=1&itemsPerPage=100",  
             "rel":"self"  
          }  
       ],  
       "results":[  
          {  
             "links":[  
                {  
                   "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/12345678/processes/shard-00-00.mongodb.net:27017/disks/xvdb",  
                   "rel":"self"  
                }  
             ],  
             "partitionName":"xvdb"  
          }  
       ],  
       "totalCount":1  
    }  
  
What is MongoDB Atlas? →

