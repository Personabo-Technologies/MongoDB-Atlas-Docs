Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Enable and Configure Encryption at Rest using Customer Key Management for
One Project

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example Request
  * Enable Encryption at Rest using Customer Key Management
  * Disable Encryption at Rest using Customer Key Management
  * Example Response
  * Disable Encryption at Rest using Customer Key Management

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Enables, disables, and configures Encryption at Rest using Customer Key
Management for an Atlas project with one of the following providers:

  * Amazon Web Services Key Management Service

  * Azure Key Vault

  * Google Cloud KMS

After configuring at least one Encryption at Rest using Customer Key
Management provider for the Atlas project, `Project Owners` can enable
Encryption at Rest using Customer Key Management for each Atlas cluster for
which they require encryption. The Encryption at Rest using Customer Key
Management provider does _not_ have to match the cluster cloud service
provider.

Atlas does not automatically rotate user-managed encryption keys. Defer to
your preferred Encryption at Rest using Customer Key Management provider's
documentation and guidance for best practices on key rotation. Atlas
automatically creates a 90-day key rotation alert when you configure
Encryption at Rest using Customer Key Management using your Key Management in
an Atlas project.

## Note

Atlas encrypts all storage whether or not you use your own key management.

## Tip

### See also:

To learn more about key management, see Encryption at Rest using Customer Key
Management, including prerequisites and restrictions.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    PATCH /groups/{GROUP-ID}/encryptionAtRest  
      
  
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

The required request body parameters depend on whether Encryption at Rest
using Customer Key Management is currently enabled:

  * If you have enabled Encryption at Rest using Customer Key Management, Atlas requires all of the parameters for the desired encryption provider.

    * If you want to use AWS KMS, Atlas requires all the fields in the `awsKms` document.

    * If you want to use Azure Key Vault, Atlas requires all the fields in the `azureKeyVault` document.

    * If you want to use Google Cloud KMS, Atlas requires all the fields in the `googleCloudKms` document.

  * If you have enabled Encryption at Rest using Customer Key Management, administrators can pass only the changed fields for the `awsKms`, `azureKeyVault`, or `googleCloudKms` document to update the configuration to this endpoint.

AWS

Azure

GCP

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`awsKms`

|

object

|

Required

|

AWS KMS configuration details and whether Encryption at Rest using Customer
Key Management is enabled for an Atlas project.  
  
`awsKms`

`.accessKeyID`

|

string

|

Optional

|

IAM access key ID with permissions to access the customer master key
(`awsKms.customerMasterKeyID`).  
  
`awsKms`

`.customerMasterKeyID`

|

string

|

Optional

|

AWS customer master key used to encrypt and decrypt the MongoDB master keys.  
  
`awsKms`

`.enabled`

|

boolean

|

Optional

|

Flag that indicates whether Encryption at Rest using Customer Key Management
is enabled for an Atlas project. To disable Encryption at Rest using Customer
Key Management, pass only this parameter with a value of `false`. When you
disable Encryption at Rest using Customer Key Management, Atlas removes the
configuration details.  
  
`awsKms`

`.region`

|

string

|

Optional

|

AWS region in which the AWS customer master key exists:

North America

Europe

South America

Asia

Australia

Middle East

Africa

|

Region Value

|

Corresponding Region in Console  
  
|  
  
US_EAST_1

|

  1. Virginia (us-east-1)

  
  
US_EAST_2

|

Ohio (us-east-2)  
  
US_WEST_1

|

  1. California (us-west-1)

  
  
US_WEST_2

|

Oregon (us-west-2)  
  
CA_CENTRAL_1

|

Montreal (ca-central-1)  
  
`awsKms`

`.roleId`

|

string

|

Optional

|

ID of an AWS IAM role authorized to manage an AWS customer master key. To find
the ID for an existing IAM role, send a GET request to the
`cloudProviderAccess` API endpoint.  
  
`awsKms`

`.secretAccessKey`

|

string

|

Optional

|

IAM secret access key with permissions to access the customer master key
(`awsKms.customerMasterKeyID`).  
  
### Response

AWS

Azure

GCP

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

Specifies whether Encryption at Rest using Customer Key Management is enabled
for an Atlas project and the AWS KMS configuration details.  
  
`awsKms`

`.accessKeyID`

|

string

|

IAM access key ID with permissions to access the customer master key
(`awsKms.customerMasterKeyID`).  
  
`awsKms`

`.customerMasterKeyID`

|

string

|

AWS customer master key used to encrypt and decrypt the MongoDB master keys.  
  
`awsKms`

`.enabled`

|

boolean

|

Flag that indicates whether Encryption at Rest using Customer Key Management
is enabled for an Atlas project.  
  
`awsKms`

`.region`

|

string

|

AWS region in which the AWS customer master key exists.  
  
`awsKms`

`.valid`

|

boolean

|

Specifies whether the encryption key set for the provider is valid and may be
used to encrypt and decrypt data. This field is a system-controlled status
report and is read-only.  
  
## Example Request

### Enable Encryption at Rest using Customer Key Management

AWS

Azure

GCP

The following example enables and configures Encryption at Rest using Customer
Key Management for an Atlas project using AWS KMS:

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/encryptionAtRest?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "awsKms": {  
    8|            "enabled": true,  
    9|            "accessKeyID" : "AKIAIOSFODNN7EXAMPLE",  
    10|            "secretAccessKey": "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",  
    11|            "customerMasterKeyID" : "030gce02-586d-48d2-a966-05ea954fde0g",  
    12|            "region" : "US_EAST_1"  
    13|          }  
    14|        }'  
  
### Disable Encryption at Rest using Customer Key Management

The following example disables Encryption at Rest using Customer Key
Management for an Atlas project:

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Accept: application/json" \  
    3|      --header "Content-Type: application/json" \  
    4|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/encryptionAtRest?pretty=true" \  
    5|      --data '  
    6|        {  
    7|          "awsKms": {  
    8|            "enabled" : false  
    9|          }  
    10|        }'  
  
## Example Response

AWS

Azure

GCP

    
    
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
    16|     "tenantID" : null,  
    17|     "valid" : false  
    18|   }  
    19| }  
  
### Disable Encryption at Rest using Customer Key Management

    
    
    1| {  
    |  
    2|   "awsKms" : {  
    3|     "accessKeyID" : null,  
    4|     "customerMasterKeyID" : null,  
    5|     "enabled" : false,  
    6|     "region" : null,  
    7|     "valid" : false  
    8|   },  
    9|   "azureKeyVault" : {  
    10|     "clientID" : null,  
    11|     "enabled" : false,  
    12|     "keyIdentifier" : null,  
    13|     "keyVaultName" : null,  
    14|     "resourceGroupName" : null,  
    15|     "subscriptionID" : null,  
    16|     "tenantID" : null,  
    17|     "valid" : false  
    18|   },  
    19|   "googleCloudKms" : {  
    20|     "enabled": false,  
    21|     "keyVersionResourceID" : null,  
    22|     "valid" : false  
    23|   }  
    24| }  
  
What is MongoDB Atlas? →

