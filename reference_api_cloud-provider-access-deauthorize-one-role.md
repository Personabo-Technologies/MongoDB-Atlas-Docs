Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Deauthorize a Cloud Provider Access Role

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

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Resource

    
    
    DELETE api/atlas/v1.0/groups/{GROUP-ID}/cloudProviderAccess/{CLOUD-PROVIDER}/{ROLE-ID}  
      
  
### Request Path Parameters

Parameter

|

Type

|

Description  
  
||  
  
`GROUP-ID`

|

string

|

Unique identifier for the project with a cloud provider role you want to
deauthorize.  
  
`CLOUD-PROVIDER`

|

string

|

Cloud provider of the role you want to deauthorize. Currently only `AWS` is
supported.  
  
`ROLE-ID`

|

string

|

Unique identifier of the role to deauthorize.  
  
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

A successful request to this endpoint returns no content.

## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" -X DELETE --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/cloudProviderAccess/{CLOUD-PROVIDER}/{ROLE-ID}?pretty=true"  
  
What is MongoDB Atlas? →

