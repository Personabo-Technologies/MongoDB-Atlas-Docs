Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get Configuration for Encryption at Rest using Customer Key Management for
One Project

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

Retrieves the current configuration details for Encryption at Rest using
Customer Key Management for an Atlas project with one of the following
providers:

  * Amazon Web Services Key Management Service

  * Azure Key Vault

  * Google Cloud KMS

## Note

Atlas encrypts all storage whether or not you use your own key management.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/encryptionAtRest  
      
  
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

Unique identifier for the project.  
  
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

Name

|

Type

|

Description  
  
||  
  
`awsKms`

|

object

|

Specifies whether Encryption at Rest is enabled for an Atlas project and the
AWS KMS configuration details.  
  
`awsKms.accessKeyID`

|

string

|

The IAM access key ID with permissions to access the customer master key
specified by `customerMasterKeyID`.  
  
`awsKms.customerMasterKeyID`

|

string

|

The AWS customer master key used to encrypt and decrypt the MongoDB master
keys.  
  
`awsKms.enabled`

|

boolean

|

Specifies whether Encryption at Rest is enabled for an Atlas project.  
  
`awsKms.region`

|

string

|

The AWS region in which the AWS customer master key exists.  
  
`awsKms.valid`

|

boolean

|

Specifies whether the encryption key set for the provider is valid and may be
used to encrypt and decrypt data. This field is a system-controlled status
report and is read-only.  
  
`azureKeyVault`

|

object

|

Specifies Azure Key Vault configuration details and whether Encryption at Rest
is enabled for an Atlas project.  
  
`azureKeyVault.azureEnvironment`

|

string

|

The Azure environment where the Azure account credentials reside.  
  
`azureKeyVault.clientID`

|

string

|

The client ID, also known as the application ID, for an Azure application
associated with the Azure AD tenant.  
  
`azureKeyVault.enabled`

|

boolean

|

Specifies whether Encryption at Rest is enabled for an Atlas project and the
Azure Key Vault configuration details.  
  
`azureKeyVault.keyIdentifier`

|

string

|

The unique identifier of a key in an Azure Key Vault.  
  
`azureKeyVault.keyVaultName`

|

string

|

The name of an Azure Key Vault containing your key.  
  
`azureKeyVault.resourceGroupName`

|

string

|

The name of the Azure Resource group that contains an Azure Key Vault.  
  
`azureKeyVault.subscriptionID`

|

string

|

The unique identifier associated with an Azure subscription.  
  
`azureKeyVault.tenantID`

|

string

|

Unique identifier for an Azure AD tenant within an Azure subscription.  
  
`azureKeyVault.valid`

|

boolean

|

Specifies whether the encryption key set for the provider is valid and may be
used to encrypt and decrypt data. This field is a system-controlled status
report and is read-only.  
  
`googleCloudKms.enabled`

|

boolean

|

Specifies whether Encryption at Rest is enabled for an Atlas project using
Google Cloud KMS.  
  
`googleCloudKms.keyVersionResourceID`

|

string

|

Key Version Resource ID for your Google Cloud KMS.  
  
`googleCloudKms.valid`

|

boolean

|

Specifies whether the encryption key set for the provider is valid and may be
used to encrypt and decrypt data. This field is a system-controlled status
report and is read-only.  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --header "Accept: application/json" \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/encryptionAtRest?pretty=true"  
  
## Example Response

AWS

Azure

GCP

The following example response contains Encryption at Rest using Customer Key
Management configuration details for an Atlas project using AWS KMS:

    
    
    1| {  
    |  
    2|   "awsKms" : {  
    3|     "accessKeyID" : "AKIAIOSFODNN7EXAMPLE",  
    4|     "customerMasterKeyID" : "030gce02-586d-48d2-a966-05ea954fde0g",  
    5|     "enabled" : true,  
    6|     "region" : "US_EAST_1",  
    7|     "valid" : true  
    8|   },  
    9|   "azureKeyVault" : {  
    10|     "clientID" : null,  
    11|     "enabled" : false,  
    12|     "keyIdentifier" : null,  
    13|     "keyVaultName" : null,  
    14|     "resourceGroupName" : null,  
    15|     "subscriptionID" : null,  
    16|     "tenantID" : "null",  
    17|     "valid" : false  
    18|   },  
    19|   "googleCloudKms" : {  
    20|     "enabled" : false,  
    21|     "keyVersionResourceID" : null,  
    22|     "valid" : false  
    23|   }  
    24| }  
  
What is MongoDB Atlas? →

