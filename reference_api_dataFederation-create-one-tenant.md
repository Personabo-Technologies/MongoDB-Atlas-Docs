Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create One Federated Database Instance

Share Feedback

On this page

  * Usage
  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Example

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

`https://cloud.mongodb.com/api/atlas/v1.0`

## Usage

Use this endpoint to create a specific federated database instance associated
to an Atlas project. To create an federated database instance, specify a name
for your federated database instance, the unique identifier of the role that
federated database instance can use to access your AWS data store, and the S3
bucket where data is stored.

## Syntax

    
    
    POST /groups/{GROUP-ID}/dataLakes  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

The unique identifier for the project.  
  
### Request Query Parameters

The following query parameters are optional:

Query Parameter

|

Type

|

Description

|

Default  
  
|||  
  
`pretty`

|

boolean

|

Displays response in a prettyprint format.

|

`false`  
  
`envelope`

|

boolean

|

Specifies whether or not to wrap the response in an envelope.

|

`false`  
  
### Request Body Parameters

Field

|

Required/Optional

|

Description  
  
||  
  
`name`

|

Required

|

Name of the federated database instance.  
  
`cloudProviderConfig`

|

Optional

|

Configuration information related to the cloud service where federated
database instance source data is stored.  
  
`cloudProviderConfig.<provider>`

|

Required

|

Name of the provider of the cloud service where the federated database
instance can access the S3 Bucket.

Data Federation supports only `aws`.

Required if specifying `cloudProviderConfig`.  
  
`cloudProviderConfig.aws.roleId`

|

Required

|

Unique identifier of the role that the federated database instance can use to
access S3 Buckets. If necessary, use the Atlas API to retrieve the role ID.
You must also specify the `testS3Bucket`.

Required if specifying `cloudProviderConfig`.  
  
`cloudProviderConfig.aws. testS3Bucket`

|

Required

|

Name of the S3 data bucket that the provided role ID is authorized to access.
You must also specify the `roleId`.

Required if specifying `cloudProviderConfig`.  
  
## Response

Name

|

Type

|

Description  
  
||  
  
`cloudProviderConfig`

|

object

|

Configuration information related to the cloud service where federated
database instance source data is stored.  
  
`cloudProviderConfig.<provider>`

|

object

|

Name of the provider of the cloud service where the federated database
instance can access the S3 Bucket data stores.

Data Federation only supports `aws`.  
  
`cloudProviderConfig.externalId`

|

string

|

Unique identifier associated with the IAM Role that the federated database
instance assumes when accessing the AWS S3 buckets.  
  
`cloudProviderConfig.aws. iamAssumedRoleARN`

|

string

|

Amazon Resource Name (ARN) of the IAM Role that the federated database
instance assumes when accessing the S3 Buckets.

The IAM Role must support the following actions against each S3 bucket:

  * `s3:GetObject`

  * `s3:ListBucket`

  * `s3:GetObjectVersion`

## Note

`s3:PutObject` is optional. This action is required only if you want to use
$out to S3.

For more information on S3 actions, see Actions, Resources, and Condition Keys
for Amazon S3.  
  
`cloudProviderConfig.aws. iamUserARN`

|

string

|

Amazon Resource Name (ARN) of the user that the federated database instance
uses when accessing the S3 Buckets.  
  
`cloudProviderConfig.aws.roleId`

|

string

|

Unique identifier of the role that the federated database instance uses to
access the S3 Buckets.  
  
`dataProcessRegion`

|

Optional

|

The cloud provider region to which Data Federation routes client connections
for data processing.

If `null`, Data Federation routes client connections to the region nearest to
the client based on DNS resolution.  
  
`dataProcessRegion.cloudProvider`

|

Required

|

Name of the cloud service provider.

Data Federation only supports `AWS`.  
  
`dataProcessRegion.region`

|

Required

|

Name of the region to which Data Federation routes client connections for data
processing.

Data Federation only supports the following regions:

  * `SYDNEY_AUS` (ap-southeast-2)

  * `MUMBAI_IND` (ap-south-1)

  * `FRANKFURT_DEU` (eu-central-1)

  * `DUBLIN_IRL` (eu-west-1)

  * `LONDON_GBR` (eu-west-2)

  * `VIRGINIA_USA` (us-east-1)

  * `OREGON_USA` (us-west-2)

  
  
`groupId`

|

string

|

The unique identifier for the project.  
  
`hostnames`

|

array

|

The list of hostnames assigned to the federated database instance. Each string
in the array is a hostname assigned to the federated database instance.  
  
`name`

|

string

|

Name of the federated database instance.  
  
`state`

|

string

|

Current state of the federated database instance:

  * `ACTIVE` \- The federated database instance is active and verified. You can query it.

  
  
`storage`

|

object

|

Configuration details for each federated database instance and its mapping to
MongoDB database(s) and collection(s).  
  
`storage.databases`

|

object

|

Configuration details for mapping each federated database instance to
queryable databases and collections. For complete documentation on this object
and its nested fields, see Define Data Stores for a Federated Database
Instance.

An empty object indicates that the federated database instance has no mapping
configuration for any federated database instance.  
  
`storage.stores`

|

array

|

Each object in the array represents a federated database instance. Data
Federation uses the `storage.databases` configuration details to map data in
each federated database instance to queryable databases and collections. For
complete documentation on this object and its nested fields, see Define Data
Stores for a Federated Database Instance.

An empty object indicates that the federated database instance has no
configured sources.  
  
## Example

## Example

### Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
     --header "Accept: application/json" \  
     --header "Content-Type: application/json" \  
     --request POST "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/dataLakes?pretty=true" \  
     --data '{ \  
       "name" : "UserMetricData", \  
       "cloudProviderConfig" : {  
         "aws" : {  
           "roleId" : "1a234bcd5e67f89a12b345c6",  
           "testS3Bucket" : "user-metric-data-bucket"  
         }  
       }  
     }'  
  
The preceding request returns the following:

## Example

### Response

    
    
    {  
      
      "cloudProviderConfig": {  
        "aws": {  
          "externalId" : "12a3bc45-de6f-7890-12gh-3i45jklm6n7o",  
          "iamAssumedRoleARN": "arn:aws:iam::123456789012:role/ReadS3BucketRole",  
          "iamUserARN": "arn:aws:iam::1234567890123:root",  
          "roleId": "1a234bcd5e67f89a12b345c6"  
        }  
      },  
      "dataProcessRegion": null,  
      "groupId": "1ab23c4567def890gh12ij34",  
      "hostnames": [  
        "hardwaremetricdata.mongodb.example.net"  
      ],  
      "name": "UserMetricData",  
      "state": "ACTIVE",  
      "storage": {  
        "databases": [],  
        "stores": []  
      }  
    }  
  
What is MongoDB Atlas? →

