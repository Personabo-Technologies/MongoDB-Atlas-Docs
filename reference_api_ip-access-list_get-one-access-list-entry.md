Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Single Project IP Access List Entry

Share Feedback

On this page

  * Syntax
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

## Important

### Access List Replaces Whitelist

This resource replaces the whitelist resource. Atlas removed whitelists in
July 2021. Update your applications to use this new resource.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

This endpoint (`/groups/{GROUP-ID}/accessList`) manages the Project IP Access
List.

It doesn't manage the access list for Atlas organizations. The Programmatic
API Keys endpoint (`/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accesslist`) manages
those access lists.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/accessList/{ACCESS-LIST-ENTRY}  
      
  
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

Unique identifier for the project from which you want to retrieve an access
list entry.  
  
ACCESS-LIST-ENTRY

|

string

|

Required

|

Can be either the:

  * AWS security group ID,

  * IP address, or

  * CIDR address

of the access list entry to retrieve. If the entry includes a subnet mask, use
the URL-encoded value `%2F` for the forward slash `/`.  
  
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
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/accessList/203.0.113.0%2F24?pretty=true"  
  
## Example Response

    
    
    {  
      
      "cidrBlock": "203.0.113.0/24",  
      "comment": "CIDR block for Application Server B - D",  
      "groupId": "{GROUP-ID}",  
      "links": []  
    }  
  
What is MongoDB Atlas? →

