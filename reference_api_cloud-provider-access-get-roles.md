Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Cloud Provider Access Roles

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

    
    
    GET api/atlas/v1.0/groups/{GROUP-ID}/cloudProviderAccess  
      
  
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

The unique identifier for the project whose cloud provider roles you want to
retrieve.  
  
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

The HTTP document contains an array of `awsIamRoles` objects, each of which
contains the following elements:

Name

|

Type

|

Description  
  
||  
  
`atlasAWSAccountArn`

|

string

|

ARN associated with the Atlas AWS account used to assume IAM roles in your AWS
account.  
  
`atlasAssumedRoleExternalId`

|

string

|

Unique external ID Atlas uses when assuming the IAM role in your AWS account.  
  
`authorizedDate`

|

date

|

Date on which this role was authorized.  
  
`createdDate`

|

date

|

Date on which this role was created.  
  
`featureUsages`

|

array

|

Atlas features this AWS IAM role is linked to.  
  
`iamAssumedRoleArn`

|

string

|

ARN of the IAM Role that Atlas assumes when accessing resources in your AWS
account.  
  
`providerName`

|

string

|

Name of the cloud provider. Currently limited to `AWS`.  
  
`roleId`

|

string

|

Unique ID of this role.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" -X GET --digest \  
      
         --header "Accept: application/json" \  
         "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/cloudProviderAccess/?pretty=true"  
  
## Example Response

    
    
    {  
      
      "awsIamRoles" : [ {  
        "atlasAWSAccountArn" : "arn:aws:iam::123456789012:root",  
        "atlasAssumedRoleExternalId" : "3192be49-6e76-4b7d-a7b8-b486a8fc4483",  
        "authorizedDate" : "2020-08-03T20:42:49Z",  
        "createdDate" : "2020-07-30T20:20:36Z",  
        "featureUsages" : [ ],  
        "iamAssumedRoleArn" : "arn:aws:iam::772401394250:role/my-test-aws-role",  
        "providerName" : "AWS",  
        "roleId" : "5f232b94af0a6b41747bcc2d"  
      } ]  
    }  
  
What is MongoDB Atlas? →

