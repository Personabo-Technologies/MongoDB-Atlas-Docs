Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Return All Connected Organizations

Share Feedback

On this page

  * Required Roles
  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `federationSettings` resource allows you to return all connected
organizations for a federated authentication configuration.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Organization Owner` role for at least one connected
organization in the federation configuration to call this endpoint.

## Resource

    
    
    GET /federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs/  
      
  
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

## Response

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

Each document in the `result` array contains the federated authentication
configuration for each connected organization.

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
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs"  
  
## Example Response

    
    
    {  
      
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/federationSettings/{FEDERATION-SETTINGS-ID}/connectedOrgConfigs?pageNum=1&itemsPerPage=100",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "domainAllowList": [],  
             "domainRestrictionEnabled": false,  
             "identityProviderId": null,  
             "orgId": "5f86fb11e0079069c9ec3132",  
             "postAuthRoleGrants": [],  
             "roleMappings": [],  
             "userConflicts": null  
         }  
     ],  
     "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

