Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Organization Users

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Response Elements
  * Example Request
  * Request
  * Response

`https://cloud.mongodb.com/api/atlas/v1.0`

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

    
    
    GET /orgs/{ORG-ID}/users  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`ORG-ID`

|

Required.

|

The unique identifier for the organization whose user information you want to
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
  
### Response Elements

If you set the query element `envelope` to `true`, the response is wrapped by
the `content` object.

The HTTP response returns a JSON document that includes the following objects:

#### `results`

An array of documents, each representing one Organization user.

Name

|

Description  
  
|  
  
`country`

|

The country where the user lives.  
  
`emailAddress`

|

The user's email address.  
  
`firstName`

|

The user's first name.  
  
`lastName`

|

ID of the Atlas project the user belongs to.  
  
`id`

|

The user's id.  
  
`links`

|

One or more links to sub-resources and/or related resources.  
  
`mobileNumber`

|

The user's mobile phone number.  
  
`username`

|

The username for authenticating to MongoDB.  
  
`roles`

|

An array of the user's roles within the Organization and for each Project to
which the user belongs.  
  
`roles.{ENTITY-ID}`

|

The `{ENTITY-ID}` represents the Organization or Project to which this role
applies. Possible values are: `orgId` or `groupId`.  
  
`roles.roleName`

|

The name of the role. The `users` resource returns all the roles the user has
in Atlas. Possible values are:

  * Organization Roles

    * `ORG_OWNER`

    * `ORG_MEMBER`

    * `ORG_GROUP_CREATOR`

    * `ORG_BILLING_ADMIN`

    * `ORG_READ_ONLY`

  * Project Roles

## Note

Groups and projects are synonymous terms.

    * `GROUP_OWNER`

    * `GROUP_CLUSTER_MANAGER`

    * `GROUP_READ_ONLY`

    * `GROUP_DATA_ACCESS_ADMIN`

    * `GROUP_DATA_ACCESS_READ_WRITE`

    * `GROUP_DATA_ACCESS_READ_ONLY`

    * `GROUP_AUTOMATION_ADMIN` (Cloud Manager)

    * `GROUP_BACKUP_ADMIN` (Cloud Manager)

    * `GROUP_MONITORING_ADMIN` (Cloud Manager)

    * `GROUP_OWNER` (Cloud Manager)

    * `GROUP_USER_ADMIN` (Cloud Manager)

  
  
`teamIds`

|

An array of the team ids for the organization.  
  
##### `links`

An array of documents, representing a link to one or more sub-resources and/or
related resources such as list pagination. See Linking for more information.

##### `totalCount`

The total number of items in the result set. This value may be higher than the
number of objects in the `results` array if the entire result set is
paginated.

## Example Request

### Request

## Important

You must modify the following code block with the appropriate credentials and
organization ID.

    
    
    curl -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest "https://cloud.mongodb.com/api/atlas/v1.0/orgs/59db8d1d87d9d6420df0613f/users?pretty=true"  
      
  
### Response

    
    
    HTTP/1.1 200 OK  
      
      
    {  
      "links" : [ ... ],  
      "results" : [  
        {  
           "country": "US",  
           "emailAddress": "someone@example.com",  
           "firstName": "John",  
           "id": "59db8d1d87d9d6420df0613a",  
           "lastName": "Smith",  
           "links": [ ... ],  
           "mobileNumber": "123-456-7890",  
           "roles": [{  
             "groupId": "59ea02e087d9d636b587a967",  
             "roleName": "GROUP_OWNER"  
           }, {  
             "groupId": "59db8d1d87d9d6420df70902",  
             "roleName": "GROUP_OWNER"  
           }, {  
             "orgId": "59db8d1d87d9d6420df0613f",  
             "roleName": "ORG_OWNER"  
           }],  
           "teamIds" : [ "5aeeed020bd6ef9d00033291", "5ac2aeadcabceef96172be31" ],  
           "username": "someone@example.com"  
        },  
        ...  
      ],  
      "totalCount" : 2  
    }  
  
What is MongoDB Atlas? →

