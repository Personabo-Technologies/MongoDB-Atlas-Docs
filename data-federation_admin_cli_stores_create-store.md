Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `createStore`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Example
  * Troubleshoot Errors

The `createStore` command creates a store in the federated database instance
storage configuration. Click on the tab below to learn more about creating a
federated database instance store for the data source.

S3

Atlas Cluster

HTTP

Atlas Data Lake Datasets

This tab contains the syntax and parameters for creating a federated database
instance store for data in AWS S3 bucket.

## Syntax

S3 Configuration

Atlas Configuration

HTTP Configuration

Atlas Data Lake Configuration

    
    
    db.runCommand({ createStore: <store-name>, provider: <storage-provider>, region: <region-name>, bucket: <bucket-name>, additionalStorageClasses: [ <storage-classes> ], delimiter: <delimiter>, prefix: <prefix>, public: true|false })  
      
  
## Parameters

S3 Configuration

Atlas Configuration

HTTP Configuration

Atlas Data Lake Configuration

Parameter

|

Type

|

Description

|

Required?  
  
|||  
  
`createStore`

|

string

|

Name of the new federated database instance store. The federated database
instance store name must be unique.

|

yes  
  
`provider`

|

string

|

Name of the service where the data is stored. Value can be one of the
following:

  * `s3` for an AWS S3 bucket.

  * `atlas` for Atlas cluster.

  * `http` for files hosted at publicly accessible URLs.

  * `dls:aws` for Atlas Data Lake datasets.

|

yes  
  
|

|

|  
  
|||  
  
`region`

|

string

|

Region in which the `bucket` is hosted. For a list of valid region names, see
Amazon Web Services (AWS).

|

yes  
  
`bucket`

|

string

|

Name of the bucket in which data is stored. Must exactly match the name of an
S3 bucket which Data Federation can access given the configured AWS IAM
credentials.

|

yes  
  
`additionalStorageClasses`

|

array of strings

|

Array of AWS S3 storage classes. Atlas Data Federation will include the files
in these storage classes in the query results. Valid values are:

  * `INTELLIGENT_TIERING` to include files in the Intelligent Tiering storage class.

  * `STANDARD_IA` to include files in the Standard-Infrequent Access storage class.

## Note

Files in the Standard storage class are supported by default.

|

no  
  
`delimiter`

|

string

|

Character used to separate path segments in the federated database instance
store. If ommitted, defaults to `"/"`.

|

no  
  
`public`

|

boolean

|

Flag that indicates whether or not the bucket is public. Valid values are:

  * `true` to not use the AWS IAM role to access the bucket

  * `false` to require the AWS IAM role to access the bucket

If ommitted, defaults to `false`.

|

no  
  
`prefix`

|

string

|

Value prepended to the `path`. If ommitted, defaults to `""`.

|

no  
  
## Output

The command prints the following output if it succeeds. If the command fails,
see Troubleshoot Errors for recommended solutions.

S3 Configuration

Atlas Configuration

HTTP Configuration

Atlas Data Lake Configuration

    
    
    {  
      
      "ok": 1,  
      "store": {  
        "name": "<store-name>",  
        "region": "<region-name>",  
        "bucket": "<bucket-name>",  
        "additionalStorageClasses": ["<storage-classes>"]  
        "delimiter": "<delimiter>",  
        "prefix": "<prefix>",  
        "provider": "<storage-provider>"  
      }  
    }  
  
## Example

The following example uses the `createStore` command to create a new federated
database instance store called `myStore`.

S3 Configuration

Atlas Configuration

HTTP Configuration

Atlas Data Lake Configuration

    
    
    use sample  
      
    db.runCommand({ createStore: "myStore", provider: "s3", region: "us-east-1", bucket: "my-bucket", "additionalStorageClasses" : ["STANDARD_IA","INTELLIGENT_TIERING"], prefix: "/sample" })  
  
HIDE OUTPUT

    
    
    {  
      
      "ok": 1,  
      "store": {  
        "name": "myStore",  
        "region": "us-east-1",  
        "bucket": "my-bucket",  
        "additionalStorageClasses" : [  
                            "STANDARD_IA",  
                            "INTELLIGENT_TIERING"  
                    ],  
        "delimiter": "/",  
        "prefix": "/sample",  
        "provider": "s3"  
      }  
    }  
  
## Troubleshoot Errors

If the command fails, it returns one of the following errors.

 **Reason:** a federated database instance store with the name specified in
`createStore` already exists.

    
    
    {  
      
      "ok": 0,  
      "errmsg": "store <store-name> already exists",  
      "code": 2,  
      "codeName": "BadValue"  
    }  
  
 **Solution:** Specify a unique name for the federated database instance
store.

 **Reason:** The specified `provider` isn't recognized.

    
    
    {  
      
      "ok": 0,  
      "errmsg": "unrecognized store provider <storage-provider>",  
      "code": 2,  
      "codeName": "BadValue"  
    }  
  
 **Solution:** Ensure that you specify a valid storage provider.

S3 Configuration

Atlas Configuration

HTTP Configuration

Atlas Data Lake Configuration

← Manage a Federated Database Instance`listStores` →

