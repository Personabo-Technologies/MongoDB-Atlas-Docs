Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add Users to Team

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Important

Atlas limits Atlas user membership to a maximum of 250 Atlas users per team.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /orgs/{ORG-ID}/teams/{TEAM-ID}/users  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`ORG-ID`

|

Required.

|

The unique identifier for the organization you want to associate the team
with.  
  
`TEAM-ID`

|

Required

|

The name of the team you want to add users to.  
  
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

Specify an array of documents, where each document represents one user you
want to add to the team. You must specify an array even if you are only
associating a single user to the team.

Name

|

Type

|

Description  
  
||  
  
`id`

|

string

|

The unique ID of the user you want to add to the team  
  
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

Each element in the `result` array is one user added to the team.

Name

|

Type

|

Description  
  
||  
  
`country`

|

string

|

The ISO 3166 Alpha-2 country code associated to the user.  
  
`emailAddress`

|

string

|

The email address associated to the user.  
  
`firstName`

|

string

|

The first name of the user.  
  
`id`

|

string

|

The unique identifier for the team.  
  
`lastName`

|

string

|

The last name of the user.  
  
`links`

|

object array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
`mobileNumber`

|

string

|

The phone number associated to the user.  
  
`roles`

|

array

|

Each object in the `roles` array represents the Atlas organization role the
user has for the associated `org_id`  
  
`roles.orgId`

|

string

|

ID of the organization where the user has the assigned `roles.roleName`
organization role.  
  
`roles.roleName`

|

string

|

The organization role assigned to the user for the specified `roles.orgId`.  
  
`teamsId`

|

array

|

Array of string IDs for each team the user is a member of.  
  
`username`

|

string

|

Username associated to the user.  
  
## Example

### Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/teams/{TEAM-ID}/users?pretty=true" \  
     --data '[{ "id" : "{USER-ID}" }]'  
  
### Response

    
    
    {  
      
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/teams/{TEAM-ID}/users?pretty=true",  
             "rel": "self"  
         }  
     ],  
     "results": [  
         {  
             "country": "US",  
             "emailAddress": "atlasUser@example.com",  
             "firstName": "Atlas",  
             "id": "{USER-ID}",  
             "lastName": "user",  
             "links": [  
                 {  
                     "href": "https://cloud.mongodb.com/api/atlas/v1.0/users/{USER-ID}",  
                     "rel": "self"  
                 }  
             ],  
             "mobileNumber": "5555550100",  
             "roles": [  
                 {  
                     "orgId": "{ORG-ID}",  
                     "roleName": "ORG_MEMBER"  
                 },  
                 ...  
             ],  
             "teamIds": [  
                 "{TEAM-ID}"  
             ],  
             "username": "atlasUser@example.com"  
         }  
     ],  
     "totalCount": 1  
    }  
  
What is MongoDB Atlas? →

