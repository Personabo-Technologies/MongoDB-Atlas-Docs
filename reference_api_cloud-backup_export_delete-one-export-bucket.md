Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete One Snapshot Export Bucket

Share Feedback

On this page

  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `exportBuckets` resource allows you to remove one bucket specified by the
bucket ID.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    DELETE /groups/{GROUP-ID}/backup/exportBuckets/{BUCKET-ID}  
      
  
### Request Path Parameters

Parameter

|

Type

|

Description  
  
||  
  
`BUCKET-ID`

|

string

|

Unqiue identifier of the bucket to remove.  
  
`GROUP-ID`

|

string

|

Unique 24-hexadecimal digit string that identifies the project for which to
grant access to the S3 bucket.  
  
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

This endpoint does not have response elements.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" -X DELETE --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/backup/exportBuckets/{BUCKET-ID}?pretty=true"  
  
What is MongoDB Atlas? →

