Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete an Online Archive

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Response Elements
  * Examples
  * Example Request
  * Error Codes

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can delete an online archive from the API or the Atlas UI. You must have
the `GROUP_DATA_ACCESS_ADMIN` (`Project Data Access Admin`) role to delete an
online archive.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique identifier of the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

Required

|

Name of the cluster that contains the collection.  
  
`ARCHIVE-ID`

|

Required

|

Unique identifier of the online archive to delete.  
  
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
  
## Response Elements

The HTTP response returns an empty JSON document.

## Examples

The following example request deletes the online archive by its ID.

### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
    --header "Content-Type: application/json" \  
    --include \  
    --request DELETE "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}"  
  
## Error Codes

If the request fails, it returns the following error:

Error Code

|

Description  
  
|  
  
`RESOURCE_NOT_FOUND`

|

The specified archive ID is not valid.  
  
What is MongoDB Atlas? →

