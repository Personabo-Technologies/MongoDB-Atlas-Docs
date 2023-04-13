Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update Regionalized Private Endpoint Status

Share Feedback

On this page

  * Required Roles
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Enable or disable the regionalized private endpoint setting for one Atlas
project.

## Warning

Your connection strings to existing multi-region and global sharded clusters
change when you enable this setting.

You must update your applications to use the new connection strings. This
might cause downtime.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Required Roles

You must have the `Project Owner` role for the project to successfully call
this resource.

## Request

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /groups/{GROUP-ID}/privateEndpoint/regionalMode  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
{GROUP-ID}

|

string

|

Required

|

Unique identifier for the project for which you want to enable or disable the
regionalized private endpoint setting.  
  
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

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
enabled

|

boolean

|

Required

|

Flag that indicates whether the regionalized private endpoint setting is
enabled for one Atlas project.

Set this value to **true** to create more than one private endpoint in a cloud
provider region to connect to multi-region and global Atlas sharded clusters.

## Warning

Your connection strings to existing multi-region and global sharded clusters
change when you enable this setting.

You must update your applications to use the new connection strings. This
might cause downtime.

You can enable this setting only if your Atlas project contains no replica
sets.

You can't disable this setting if you have:

  * More than one private endpoint in more than one region, or

  * More than one private endpoint in one region and one private endpoint in one or more regions.

You can create only sharded clusters when you enable the regionalized private
endpoint setting. You can't create replica sets.

Set this value is **false** to disable this setting.  
  
## Response Elements

Response Parameter

|

Type

|

Description  
  
||  
  
enabled

|

boolean

|

Flag that indicates whether the regionalized private endpoint setting is
enabled for one Atlas project.

If this value is **true** , you can create more than one private endpoint in a
cloud provider region to connect to multi-region and global Atlas sharded
clusters.

If this value is **false** , you can't create more than one private endpoint
in one cloud provider region if you have a private endpoint in a different
region.

The default value is **false**.  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Content-Type: application/json" \  
    3|      --include \  
    4|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/privateEndpoint/regionalMode" \  
    5|      --data '  
    6|        {  
    7|          "enabled" : true  
    8|        }'  
  
## Example Response

    
    
    1| {  
    |  
    2|   "enabled": true  
    3| }  
  
What is MongoDB Atlas? →

