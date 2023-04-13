Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return the Federation Configuration for One Organization

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

The `federationSettings` resource allows you to return the federated
authentication configuration for one organization.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint.

## Resource

    
    
    GET /orgs/{ORG-ID}/federationSettings  
      
  
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

Unique 24-hexadecimal digit string that identifies the organization.  
  
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
  
`federatedDomains`

|

array of strings

|

List that contains the domains associated with the organization's identity
provider.  
  
`hasRoleMappings`

|

boolean

|

Flag that indicates whether this organization has role mappings configured.  
  
`id`

|

string

|

Unique 24-hexadecimal digit string that identifies this federation.  
  
`identityProviderId`

|

string

|

Unique 20-hexadecimal digit string that identifies the identity provider
connected to this organization.  
  
`identityProviderStatus`

|

string

|

Value that indicates whether the identity provider is active. Atlas returns
`ACTIVE` if the identity provider is active and `INACTIVE` if the identity
provider is inactive.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/federationSettings"  
  
## Example Response

    
    
    {  
      
      "federatedDomains": [  
        "example.com"  
      ],  
      "hasRoleMappings": false,  
      "id": "5e8cc670a16506712e0b1e95",  
      "identityProviderId": "0oa8i0grsgbwDiIyw453",  
      "identityProviderStatus": "INACTIVE"  
    }  
  
What is MongoDB Atlas? →

