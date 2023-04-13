Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete All Cloud Backup Schedules

Share Feedback

On this page

  * Request
  * Request
  * Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

All requests to this endpoint must originate from an IP address in the
organization's API access list.

## Tip

### See also:

Required for Select Resources: API Resource Request Access Lists

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule  
      
  
## Request

### Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier of the project for the Atlas cluster.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the Atlas cluster that contains the schedule you want to delete.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
`clusterId`

|

string

|

Unique identifier of the Atlas cluster.  
  
`clusterName`

|

string

|

Name of the Atlas cluster.  
  
`links`

|

array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
`policies[]`

|

array

|

Unique identifier for the snapshot and an array of backup policy items.  
  
`policies[i]`

`.id`

|

string

|

Unique identifier of the backup policy.  
  
`policies[i]`

`.policyItems[]`

|

array

|

Array of backup policy items.  
  
`referenceHourOfDay`

|

number

|

UTC Hour of day between `0` and `23` representing which hour of the day that
Atlas takes a snapshot.  
  
`referenceMinuteOfHour`

|

number

|

UTC Minute of day between `0` and `59` representing which minute of the
`referenceHourOfDay` that Atlas takes the snapshot.  
  
`restoreWindowDays`

|

number

|

Number of days back in time you can restore to with Continuous Cloud Backup
accuracy. Must be a positive, non-zero integer.

Applies to continuous cloud backups only.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    {  
      
      "clusterId": "{GROUP-ID}",  
      "clusterName": "{CLUSTER-NAME}",  
      "links": [  
        {  
          "href": "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/backup/schedule",  
             "rel": "self"  
        },  
        {  
          "href": "https://cloud.mongodb.com/api/public/v1.0/groups/{GROUP-ID}",  
          "rel": "http://cloud.mongodb.com/group"  
        }  
      ],  
      "policies": [  
        {  
          "id": "6099955de495925c8b32592e",  
          "policyItems": []  
        }  
      ],  
      "referenceHourOfDay": 20,  
      "referenceMinuteOfHour": 19,  
      "restoreWindowDays": 7  
    }  
  
What is MongoDB Atlas? →

