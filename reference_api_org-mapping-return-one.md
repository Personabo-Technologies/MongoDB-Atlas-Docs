Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return One Connected Organization

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

The `federationSettings` resource allows you to return one connected
organization for a federated authentication configuration.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role to call this endpoint.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}/  
      
  
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

Name

|

Type

|

Description  
  
||  
  
`domainAllowList`

|

array

|

List that contains the approved domains from which organization users can log
in.

## Note

If the organization uses an identity provider, `domainAllowList` includes:

  * Any SSO domains associated with organization's identity provider.

  * Any custom domains associated with the specific organization.

To update SSO domains, you must update the identity provider.  
  
`domainRestrictionEnabled`

|

boolean

|

Flag that indicates whether domain restriction is enabled for the connected
organization.

## Note

`userConflicts` returns `null` when `"domainRestrictionEnabled": false`.  
  
`identityProviderId`

|

string

|

Unique 20-hexadecimal digit string that identifies the identity provider
associated with the connected organization.  
  
`orgId`

|

string

|

Unique 24-hexadecimal digit string that identifies the connected organization.  
  
`postAuthRoleGrants`

|

array

|

List that contains the default roles granted to users who authenticate through
the IdP in a connected organization.  
  
`roleMappings`

|

array

|

List that contains the role mappings configured in this organization.  
  
`userConflicts`

|

array

|

List that contains the usernames that don't match any domain on the allowed
list.

## Note

`userConflicts` returns `null` when `"domainRestrictionEnabled": false`.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/{ORG-ID}"  
  
## Example Response

    
    
    {  
      
     "domainAllowList": [],  
     "domainRestrictionEnabled": false,  
     "identityProviderId": null,  
     "orgId": "5f86fb11e0079069c9ec3132",  
     "postAuthRoleGrants": [],  
     "roleMappings": [],  
     "userConflicts": null  
    }  
  
What is MongoDB Atlas? →

