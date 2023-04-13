Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add Entries to Project IP Access List

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Response Document
  * results Embedded Document
  * Example Request
  * Example Response
  * Example Header
  * Example Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Access List Replaces Whitelist

This resource replaces the whitelist resource. Atlas removed whitelists in
July 2021. Update your applications to use this new resource.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

The `/groups/{GROUP-ID}/accessList` endpoint manages the database IP access
list. This endpoint is distinct from the orgs/{ORG-ID}/apiKeys/{API-KEY-
ID}/accesslist endpoint, which manages the access list for Atlas
organizations.

This endpoint does not support concurrent `POST` requests. Multiple `POST`
requests must be submitted synchronously.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/accessList  
      
  
### Request Path Parameters

Parameter

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

Unique identifier for the project to which you want to add one or more Access
List entries.  
  
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

Specify an array of documents, where each document represents one Access List
entry you want to add to the project. You must specify an array even if you
add a single Access List entry to the project.

## Important

### How Access List Updates Work

The Access List might change depending upon what you submit in the `POST`
request. This request attempts to find an existing Access List entry that has
the same `awsSecurityGroup`, `ipAddress`, or `cidrBlock` value. If the Access
List entry:

Access List Entry Match

|

`comment` Value

|

Access List Update  
  
||  
  
Yes

|

Unchanged

|

Makes no change.  
  
No

|

Added

|

Appends request as new Access List entry.  
  
Yes

|

Changed

|

Updates **comment** value in Access List entry with matching
**awsSecurityGroup** , **ipAddress** , or **cidrBlock** value.  
  
Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
awsSecurityGroup

|

string

|

Conditional

|

Unique identifier of the AWS security group to add to the access list.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.

## Note

You must configure VPC peering for your project before you can add an AWS
security group to an access list.  
  
cidrBlock

|

string

|

Conditional

|

Range of IP addresses in CIDR notation to be added to the access list.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.  
  
comment

|

string

|

Optional

|

Comment associated with the access list entry.  
  
deleteAfterDate

|

date

|

Optional

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas removes
the entry from the access list. The specified date must be in the future and
within one week of the time you make the API request.

## Important

You cannot set AWS security groups as temporary access list entries.

## Note

You may include an ISO 8601 time zone designator to ensure that the expiration
date occurs with respect to the local time in the specified time zone.  
  
ipAddress

|

string

|

Conditional

|

Single IP address to be added to the access list. Mutually exclusive with
**awsSecurityGroup** and **cidrBlock**.

Your access list entry can include only one **awsSecurityGroup** , one
**cidrBlock** , or one **ipAddress**.  
  
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

Each element in the **result** array is one Access List entry associated to
the project IP Access List.

Name

|

Type

|

Description  
  
||  
  
awsSecurityGroup

|

string

|

Unique identifier of AWS security group in this access list entry.  
  
cidrBlock

|

string

|

Range of IP addresses in CIDR notation in this access list entry.  
  
comment

|

string

|

Comment associated with this access list entry.  
  
deleteAfterDate

|

date

|

Timestamp in ISO 8601 date and time format in UTC after which Atlas deletes
the temporary access list entry. Atlas returns this field if you specified an
expiration date when creating this access list entry.  
  
groupId

|

string

|

Unique identifier of the project to which this access list entry applies.  
  
ipAddress

|

string

|

Entry using an IP address in this access list entry.  
  
links

|

object array

|

One or more links to sub-resources and/or related resources. The relations
between URLs are explained in the Web Linking Specification  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --include \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/accessList?pretty=true" \  
         --data '  
           [  
             {  
               "ipAddress" : "192.0.2.15",  
               "comment" : "IP address for Application Server A"  
             },  
             {  
               "cidrBlock" : "203.0.113.0/24",  
               "comment" : "CIDR block for Application Server B - D"  
             },  
             {  
               "awsSecurityGroup" : "sg-0026348ec11780bd1",  
               "comment" : "Access Listed AWS Security Group"  
             }  
           ]'  
  
## Example Response

### Example Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Example Body

    
    
    {  
      
      "links": [],  
      "results": [  
        {  
          "cidrBlock": "192.0.2.0/24",  
          "comment": "IP address for Application Server A",  
          "groupId": "{GROUP-ID}",  
          "ipAddress": "192.0.2.15",  
          "links": []  
        },  
        {  
          "cidrBlock": "203.0.113.0/24",  
          "comment": "CIDR block for Application Server B - D",  
          "groupId": "{GROUP-ID}",  
          "links": []  
        },  
        {  
          "awsSecurityGroup": "sg-0026348ec11780bd1",  
          "comment": "Access Listed AWS Security Group",  
          "groupId": "{GROUP-ID}",  
          "links": []  
      ],  
      "totalCount": 3  
    }  
  
What is MongoDB Atlas? →

