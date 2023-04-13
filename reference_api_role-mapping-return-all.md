Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return All Role Mappings

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * `links` Array
  * `results` Array
  * `totalCount` Field
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `federationSettings` resource allows you to return all the role mappings
from the specified organization in the specified federation.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint. This
resource doesn't require the API Key to have an Access List.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings  
      
  
## Request

### Request Path Parameters

Name

|

Type

|

Description  
  
||  
  
`FEDERATION-SETTINGS-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the federated
authentication configuration.  
  
`ORG-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the connected organization.  
  
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

## Response

### `links` Array

The `links` array includes one or more links to sub-resources or related
resources. The relations between URLs are explained in the Web Linking
Specification.

Relation

|

Description  
  
|  
  
`self`

|

The URL endpoint for this resource.  
  
### `results` Array

Each element in the `result` array is one role mapping.

Name

|

Type

|

Description  
  
||  
  
`externalGroupName`

|

string

|

Unique human-readable label that identifies the identity provider group
associated with the role mapping.  
  
`id`

|

string

|

Unique 24-hexadecimal digit string that identifies the role mapping.  
  
`roleAssignments`

|

array

|

List that contains the unique identifiers for the projects and organizations
associated with each role.  
  
`roleAssignments.groupId`

|

string

|

Unique 24-hexadecimal digit string that identifies the project in which the
role applies.  
  
`roleAssignments.orgId`

|

string

|

Unique 24-hexadecimal digit string that identifies the organization in which
the role applies.  
  
`roleAssignments.role`

|

string

|

Human readable label that identifies the role.  
  
### `totalCount` Field

This value is the count of the total number of items in the result set.
`totalCount` may be greater than the number of objects in the `results` array
if the entire result set is paginated.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings"  
  
## Example Response

    
    
    {  
      
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings?pageNum=1&itemsPerPage=100",  
          "rel": "self"  
        }  
      ],  
      "results": [  
        {  
         "externalGroupName": "example",  
         "id": "61e89721b827b56c845ff44c",  
         "roleAssignments": [  
           {  
             "groupId": null,  
             "orgId": "{ORG-ID}",  
             "role": "ORG_MEMBER"  
           }  
         ]  
        }  
      ],  
      "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

