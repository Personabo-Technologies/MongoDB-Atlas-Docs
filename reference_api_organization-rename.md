Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Rename an Organization

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example
  * Example Request
  * Example Response

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

    
    
    PATCH /orgs/{ORG-ID}  
      
  
### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`ORG-ID`

|

string

|

The id of the organization that you want to rename.  
  
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
  
||  
  
`name`

|

string

|

The new name for the organization.  
  
## Response

Name

|

Type

|

Description  
  
||  
  
`id`

|

ObjectId

|

Unique identifier for the organization.  
  
`links`

|

document array

|

One or more links to sub-resources and/related resources. The relations
between URLs are explained in the Web Linking Specification.  
  
`name`

|

string

|

New name of the organization.  
  
## Example

### Example Request

    
    
    curl -X PATCH --include --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --header "Content-Type: application/json" \  
      
         "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1?pretty=true" \  
         --data '{"name":"MyAtlasCluster"}'  
  
### Example Response

    
    
    {  
      
      "id" : "6001f2c580eef55aedbc6bb1",  
      "links" : [ {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1",  
        "rel" : "self"  
      }, {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1/groups",  
        "rel" : "http://mms.mongodb.com/groups"  
      }, {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1/teams",  
        "rel" : "http://mms.mongodb.com/teams"  
      }, {  
        "href" : "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6001f2c580eef55aedbc6bb1/users",  
        "rel" : "http://mms.mongodb.com/users"  
      } ],  
      "name" : "MyAtlasCluster"  
    }  
  
What is MongoDB Atlas? →

