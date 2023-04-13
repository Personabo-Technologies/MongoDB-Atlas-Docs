Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Test Failover

Share Feedback

On this page

  * Permissions Required
  * Resource
  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Example
  * Request
  * Response

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

To learn more about failover testing and the replica set election process, see
Test Failover.

## Permissions Required

You must have `Project Cluster Manager` or higher role to test failover.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/restartPrimaries  
      
  
### Request Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

String

|

Required

|

The unique identifier of the project containing the cluster you want to test.  
  
`CLUSTER-NAME`

|

String

|

Required

|

The name of the cluster to test.  
  
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

## Example

### Request

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794de37132bb7b/clusters/egCluster/restartPrimaries"  
      
  
### Response

    
    
    {}  
      
  
What is MongoDB Atlas? →

