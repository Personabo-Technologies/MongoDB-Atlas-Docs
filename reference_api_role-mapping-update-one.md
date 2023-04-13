Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update One Role Mapping

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

The `federationSettings` resource allows you to update one role mapping in the
specified organization in the specified federation.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint.

## Resource

    
    
    PUT /{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings/{ROLE-MAPPING-ID}  
      
  
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

Unique 24-hexadecimal digit string that identifies your federation.  
  
`ORG-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the organization that
contains your projects.  
  
`ROLE-MAPPING-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the role mapping to update.  
  
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
  
`externalGroupName`

|

string

|

Unique human-readable label that identifies the identity provider group to
which this role mapping applies.

|

Required  
  
`roleAssignments`

|

array

|

Atlas roles and the unique identifiers of the groups and organizations
associated with each role.

roleAssignments.groupId Example

    
    
    | 1| {  
    |  
    2|   "externalGroupName": "<someIdpGroupName>",  
    3|   "roleAssignments": [  
    4|     {  
    5|       "role": "GROUP_OWNER",  
    6|       "groupId": "<GROUP-ID>"  
    7|     }  
    8|   ]  
    9| }  
  
roleAssignments.orgId Example

    
    
    1| {  
    |  
    2|   "externalGroupName": "<someIdpGroupName>",  
    3|   "roleAssignments": [  
    4|     {  
    5|       "role": "ORG_OWNER",  
    6|       "orgId": "<ORG-ID>"  
    7|     }  
    8|   ]  
    9| }  
  
Required  
  
`id`

|

string

|

Unique 24-hexadecimal digit string that identifies this role mapping.

|

Required  
  
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

Unique human-readable label that identifies the identity provider group to
which this role mapping applies.  
  
`id`

|

string

|

Unique 24-hexadecimal digit string that identifies this role mapping.  
  
`roleAssignments`

|

array

|

Atlas roles and the unique identifiers of the groups and organizations
associated with each role.

roleAssignments.groupId Example

    
    
    | 1| {  
    |  
    2|   "externalGroupName": "<someIdpGroupName>",  
    3|   "roleAssignments": [  
    4|     {  
    5|       "role": "GROUP_OWNER",  
    6|       "groupId": "<GROUP-ID>"  
    7|     }  
    8|   ]  
    9| }  
  
roleAssignments.orgId Example

    
    
    1| {  
    |  
    2|   "externalGroupName": "<someIdpGroupName>",  
    3|   "roleAssignments": [  
    4|     {  
    5|       "role": "ORG_OWNER",  
    6|       "orgId": "<ORG-ID>"  
    7|     }  
    8|   ]  
    9| }  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request PUT "https://cloud.mongodb.com/api/atlas/v1.0/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/roleMappings/{ROLE-MAPPING-ID}"  
         --data {  
                 "externalGroupName": "myGroup",  
                 "id": "9b43a5b329223c3a1591a678",  
                 "roleAssignments": [  
                     {  
                      "groupId": null,  
                      "orgId": "5df7a168f10fab3a149357fb",  
                      "role": "ORG_OWNER"  
                     }  
                   ]  
                 }  
  
## Example Response

    
    
     {  
      
     "externalGroupName": "myGroup",  
     "id": "9b43a5b329223c3a1591a678",  
     "roleAssignments": [  
         {  
              "groupId": null,  
              "orgId": "5df7a168f10fab3a149357fb",  
              "role": "ORG_OWNER"  
         }  
       ]  
     }  
  
What is MongoDB Atlas? →

