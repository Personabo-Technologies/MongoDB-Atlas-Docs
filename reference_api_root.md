Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Root

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The root resource is the starting point for the Atlas Administration API.

## Syntax

    
    
    GET https://cloud.mongodb.com/api/atlas/v1.0/  
      
  
### Request Path Parameters

This endpoint does not use HTTP request path parameters.

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

This endpoint does not use HTTP request body parameters.

## Response Elements

The response includes the following elements:

Field

|

Description  
  
|  
  
`links`

|

Array of links to related API resources. For more information on links, see
Linking.  
  
`results`

|

Array of documents, each representing one programmatic Api Key and the
organization roles associated with it.

|

Field

|

Description  
  
|  
  
`desc`

|

User-supplied description of the programmatic API Key.  
  
`id`

|

Unique identifier of the programmatic API Key.  
  
`links`

|

Links to resources associated with the programmatic API Key.  
  
`privateKey`

|

The private key of the programmatic API Key used to query this resource.  
  
`publicKey`

|

The public key for the programmatic API Key used to query this resource.  
  
`roles[]`

|

Array of organization roles. assigned to the programmatic API Key used to
query this resource.  
  
`roles[i].orgId`

|

The unique identifer of the project associated with the programmatic API Key.  
  
`roles[i].roleName`

|

The organization role associated with the programmatic API Key.  
  
`roles[i].groupId`

|

The Atlas project to which the organization role has privileges.  
  
`roles[i].roleName`

|

The organization role assigned to the programmatic API Key. The `users`
resource returns all roles assigned to the user in Atlas. Possible values are:

  * Organization Roles

    * `ORG_OWNER`

    * `ORG_MEMBER`

    * `ORG_GROUP_CREATOR`

    * `ORG_BILLING_ADMIN`

    * `ORG_READ_ONLY`

  
  
`totalCount`

|

Number of programmatic API Keys returned in the `results` array.  
  
## Example

### Example Request

    
    
    curl -X GET -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest -i "https://cloud.mongodb.com/api/atlas/v1.0"  
      
  
### Example Response

    
    
    {  
      
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6002f2c580eef55aedbc7bb1/apiKeys?pageNum=1&itemsPerPage=100",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "desc": "Programmatic Key 1",  
             "id": "6e1bac9587d9d62619dc45df",  
             "links": [  
                 {  
                     "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6002f2c580eef55aedbc7bb1/apiKeys/6e1bac9587d9d62619dc45df",  
                     "rel": "self"  
                 }  
             ],  
             "privateKey": "********-****-****-8e902de02aa0",  
             "publicKey": "cvlqyfeo",  
             "roles": [  
                 {  
                     "orgId": "5991f2c580eef55aedbc6aa0",  
                     "roleName": "ORG_MEMBER"  
                 },  
                 {  
                     "groupId": "5d0aa5fb80eef50e5e4caf7d",  
                     "roleName": "GROUP_OWNER"  
                 }  
             ]  
         },  
         {  
             "desc": "Programmatic API Key #2",  
             "id": "6df3f74980eef51f794938fe",  
             "links": [  
                 {  
                     "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/6002f2c580eef55aedbc7bb1/apiKeys/6df3f74980eef51f794938fe",  
                     "rel": "self"  
                 }  
             ],  
             "privateKey": "********-****-****-d54c11c7cce9",  
             "publicKey": "czqssgho",  
             "roles": [  
                 {  
                     "orgId": "5991f2c580eef55aedbc6aa0",  
                     "roleName": "ORG_MEMBER"  
                 },  
                 {  
                     "groupId": "5c6df63680eef54ad84bb90e",  
                     "roleName": "GROUP_READ_ONLY"  
                 }  
             ]  
         }  
     ],  
     "totalCount": 2  
    }  
  
What is MongoDB Atlas? →

