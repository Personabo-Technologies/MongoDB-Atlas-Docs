Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create a Team

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
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

Atlas limits the number of teams to a maximum of 250 teams per organization.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /orgs/{ORG-ID}/teams  
      
  
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

The name of the team you want to create.  
  
`usernames`

|

array of strings

|

Valid email addresses of users to add to the new team. Atlas checks whether
the user's email belongs to the organization, so that Atlas can properly
associate the users to the teams. The command fails and issues an error if you
provide invalid email addresses to it.  
  
## Response

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

The unique identifier for the team.  
  
`name`

|

string

|

The name of the organization associated with the team.  
  
`usernames`

|

array of strings

|

Usernames added to the new team.  
  
`links`

|

object array

|

One or more uniform resource locators that link to sub-resources and/or
related resources. The Web Linking Specification explains the relation-types
between URLs.  
  
## Example

### Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/teams/" \  
     --data '{ "name" : "myNewTeam", "usernames": ["jane.a.smith@example.com", "jane.b.smith@example.com", "jane.c.smith@example.com"] }'  
  
### Response

    
    
    {  
      
     "id": "{TEAM-ID}",  
     "links": [  
         {  
             "href": "https://cloud.mongodb.com/api/atlas/v1.0/orgs/{ORG-ID}/teams/{TEAM-ID}",  
             "rel": "self"  
         }  
     ],  
     "name": "myNewTeam",  
     "usernames": ["jane.a.smith@example.com", "jane.b.smith@example.com", "jane.c.smith@example.com"]  
    }  
  
What is MongoDB Atlas? →

