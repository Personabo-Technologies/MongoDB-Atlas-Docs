Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update Team Roles in One Project

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

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    PATCH /groups/{GROUP-ID}/teams/{TEAM-ID}  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Unique identifier of the project associated with this team.  
  
`TEAM-ID`

|

string

|

Required

|

Unique identifier of the team for which you want to update roles.  
  
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

Specify an array of strings, where each string represents one role you want to
add to the team. You must specify an array even if you are only associating a
single role to the team.

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`roleNames`

|

array

|

Required

|

Project roles you want to assign the given team.  
  
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

Response Parameter

|

Type

|

Description  
  
||  
  
`roleNames`

|

array

|

Project roles assigned to the team for the specified `teamsId`.  
  
`teamsId`

|

string

|

Unique identifier of the team assigned the listed roles.  
  
## Example

### Request

    
    
    curl --user '{PUBLIC-KEY}:{PRIVATE-KEY}' --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID3}?pretty=true" \  
     --data '{  
         "roleNames": ["GROUP_OWNER"]  
       }'  
  
### Response

    
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
      
    
    {  
      
      "links": [{  
        "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID3}?pretty=true&pageNum=1&itemsPerPage=100",  
        "rel": "self"  
      }],  
      "results": [{  
        "links": [{  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID1}",  
          "rel": "self"  
        }],  
        "roleNames": ["GROUP_OWNER", "GROUP_DATA_ACCESS_READ_ONLY", "GROUP_DATA_ACCESS_ADMIN", "GROUP_DATA_ACCESS_READ_WRITE", "GROUP_READ_ONLY"],  
        "teamId": "{TEAM-ID1}"  
      }, {  
        "links": [{  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID2}",  
          "rel": "self"  
        }],  
        "roleNames": ["GROUP_DATA_ACCESS_ADMIN", "GROUP_READ_ONLY"],  
        "teamId": "{TEAM-ID2}"  
      }, {  
        "links": [{  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/teams/{TEAM-ID3}",  
          "rel": "self"  
        }],  
        "roleNames": ["GROUP_OWNER"],  
        "teamId": "{TEAM-ID3}"  
      }],  
      "totalCount": 3  
    }  
  
What is MongoDB Atlas? →

