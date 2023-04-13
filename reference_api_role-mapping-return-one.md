Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return One Role Mapping

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `federationSettings` resource allows you to return one role mapping from
the specified organization in the specified federation.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings/{ROLE-MAPPING-ID}  
      
  
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
  
`ROLE-MAPPING-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the role mapping.  
  
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
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings/{ROLE-MAPPING-ID}"  
  
## Example Response

    
    
    {  
      
     "externalGroupName": "autocomplete-highlight",  
     "id": "61d88e15e6cc044270a36fce",  
     "roleAssignments": [  
         {  
             "groupId": null,  
             "orgId": "5f86fb11e0079069c9ec3132",  
             "role": "ORG_OWNER"  
         },  
         {  
             "groupId": "5f86fb2ff9c4e56d39502559",  
             "orgId": null,  
             "role": "GROUP_OWNER"  
         }  
     ]  
    }  
  
What is MongoDB Atlas? →

