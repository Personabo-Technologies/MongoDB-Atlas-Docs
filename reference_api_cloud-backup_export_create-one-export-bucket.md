Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Snapshot Export Bucket

Share Feedback

On this page

  * Resource
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

The `exportBuckets` resource allows you to grant Atlas access to the specified
bucket for exporting backup snapshots.

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

    
    
    POST /groups/{GROUP-ID}/backup/exportBuckets  
      
  
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

Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
`bucketName`

|

string

|

Required

|

Name of the bucket that the provided role ID is authorized to access. You must
also specify the `iamRoleId`.  
  
`cloudProvider`

|

string

|

Required

|

Name of the provider of the cloud service where Atlas can access the S3
bucket. Atlas only supports `AWS`.  
  
`iamRoleId`

|

string

|

Required

|

Unique identifier of the role that Atlas can use to access the bucket. If
necessary, use the UI or API to retrieve the role ID. You must also specify
the `bucketName`.  
  
## Response

The HTTP document contains the following elements:

Parameter

|

Type

|

Description  
  
||  
  
`id`

|

string

|

Unique identifier of the S3 bucket.  
  
`bucketName`

|

string

|

Name of the bucket that the role ID is authorized to access.  
  
`cloudProvider`

|

string

|

Name of the provider of the cloud service where Atlas can access the S3
bucket. Atlas only supports `AWS`.  
  
`iamRoleId`

|

string

|

Unique identifier of the role that Atlas uses to access the bucket.  
  
`projectId`

|

string

|

Unique 24-hexadecimal digit string identifying the project.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" -X POST --digest \  
      
         --header "Accept: application/json" \  
         --header "Content-Type: application/json" \  
         "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/backup/exportBuckets?pretty=true" \  
         --data '{  
           "iamRoleId": "12345678f901a234dbdb00ca",  
           "bucketName": "example-bucket",  
           "cloudProvider": "AWS"  
         }'  
  
## Example Response

    
    
    {  
      
      "_id": "{BUCKET-ID}",  
      "bucketName": "example-bucket",  
      "cloudProvider": "AWS",  
      "iamRoleId": "12345678f901a234dbdb00ca",  
      "projectId": "{PROJECT-ID}"  
    }  
  
What is MongoDB Atlas? →

