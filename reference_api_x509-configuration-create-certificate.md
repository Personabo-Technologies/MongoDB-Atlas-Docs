Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create an X.509 Certificate for a User

Share Feedback

On this page

  * Prerequisites
  * Required Roles
  * Resource
  * Request
  * Path Parameters
  * Query Parameters
  * Body Parameters
  * Response
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Create a new Atlas-managed X.509 certificate for the specified database user.

## Important

If you are managing your own Certificate Authority (CA) in Self-Managed X.509
mode, you must generate certificates for database users using your own CA.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Prerequisites

To generate an Atlas-managed certificate for a database user, that user must
have an `x509Type` set to `MANAGED`.

## Required Roles

You must have the `Atlas admin` role to use this endpoint.

## Resource

`https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    POST /groups/{GROUP-ID}/databaseUsers/{USERNAME}/certs  
      
  
## Request

### Path Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`GROUP-ID`

|

string

|

Required

|

Identifier for the Atlas project associated with the X.509 configuration.  
  
`USERNAME`

|

string

|

Required

|

Username of the database user to create a certificate for.  
  
### Query Parameters

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
  
### Body Parameters

Name

|

Type

|

Description

|

Default  
  
|||  
  
`monthsUntilExpiration`

|

number

|

A number of months that the created certificate is valid for before expiry, up
to 24 months.

|

3  
  
## Response

The response is a concatenated X.509 certificate and private key.

## Example

### Request

The following example creates and returns an X.509 certificate.

    
    
    curl --request POST \  
      
     --user "{publicApiKey}:{privateApiKey}" \  
     --header "Content-Type: application/json" \  
     --digest "https://cloud.mongodb.com/api/atlas/v1.0/groups/{groupId}/databaseUsers/{username}/certs?pretty=true" \  
     --data '{"monthsUntilExpiration":12}'  
  
### Response

The following partial example shows an X.509 certificate and private key
returned:

    
    
    1| --BEGIN CERTIFICATE--  
    |  
    2| MIIFCTCCAvGgAwIBAgIIbbbwIuB41jMwDQYJKoZIhvcNAQELBQAwSTEhMB8GA1UE  
    3| ...  
    4| RU6XlZVzscjSFPjuXfGcprc+cXH2bXQ4tfH3KFOPETdHfWtxe7F1nq4zPwgQ  
    5| --END CERTIFICATE--  
    6| --BEGIN PRIVATE KEY--  
    7| MIIJQgIBADANBgkqhkiG9w0BAQEFAASCCSwwggkoAgEAAoICAQC8kbepjB1PB62e  
    8| ...  
    9| q0cjL/n1kRCfS5lJTsu7XkYDy6reEQ==  
    10| --END PRIVATE KEY--  
  
What is MongoDB Atlas? →

