Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create From the UI

Share Feedback

On this page

  * Prerequisites
  * Procedure

This page describes how to deploy a federated database instance for accessing
data in your AWS S3 buckets.

## Prerequisites

Before you begin, you will need to:

  * Create a MongoDB Atlas account, if you do not have one already.

  * Install the AWS CLI.

  * Configure the AWS CLI to access your AWS account. Alternatively, you must have access to the AWS Management Console with permission to create IAM roles.

  *  _Optional._ Set Up Unified AWS Access.

## Procedure

1

### Log in to MongoDB Atlas.

2

### Select the Data Federation option on the left-hand navigation.

3

### Create a federated database instance.

  * For your first federated database instance, click Create a Federated Database.

  * For subsequent federated database instances, click Create Federated Database.

4

### Select the configuration method.

  * For a guided experience, click Visual Editor.

  * To edit the raw JSON, click JSON Editor.

5

### Specify your AWS S3 data store and configure federated databases and
virtual collections that map to your data store.

Visual Editor

JSON Editor

1

#### Select the dataset for you federated database instance from the Data
Sources section.

Click Add Data Sources to select your data store.

2

#### Specify your data store.

Choose Amazon S3 to configure a federated database instance for data in AWS S3
buckets.

Corresponds to `stores.[n].provider` JSON configuration setting.

3

#### Select an AWS IAM role for Atlas.

You can select an existing AWS IAM role that Atlas is authorized for from the
role selection dropdown list or choose Authorize an AWS IAM Role to authorize
a new role.

If you selected an existing role that Atlas is authorized for, proceed to the
next step to list your AWS S3 buckets.

If you are authorizing Atlas for an existing role or are creating a new role,
complete the following steps before proceeding to the next step:

  1. Select Authorize an AWS IAM Role to authorize a new role or select an existing role from the dropdown and click Next.

  2. Use the AWS ARN and unique External ID in the Add Atlas to the trust relationships of your AWS IAM role section to add Atlas to the trust relationships of an existing or new AWS IAM role.

In the Atlas UI, click and expand one of the following:

    * The Create New Role with the AWS CLI shows how to use the ARN and the unique External ID to add Atlas to the trust relationships of a new AWS IAM role. Follow the steps in the Atlas UI for creating a new role. To learn more, see Create New Role with the AWS CLI.

When authorizing a new role, if you quit the `Configure a New Data Lake`
workflow:

      * Before validating the role, Atlas will not create the federated database instance. You can go to the Atlas Integrations page to authorize a new role. You can resume the workflow when you have the AWS IAM role ARN.

      * After validating the role, Atlas will not create the federated database instance. However, the role is available in the role selection dropdown and can be used to create a federated database instance. You do not need to authorize the role again.

    * The Add Trust Relationships to an Existing Role shows how to use the ARN and the unique External ID to add Atlas to the trust relationships of an existing AWS IAM role. Follow the steps in the Atlas UI for adding Atlas to the trust relationship to an existing role. To learn more, see Add Trust Relationships to an Existing Role .

## Important

If you modify your custom AWS role ARN in the future, ensure that the access
policy of the role includes the appropriate access to the S3 resources for the
federated database instance.

## Tip

### See also:

    * Set Up Unified AWS Access

    * Create a Cloud Provider Access Role

  3. Click Next.

4

#### Enter the S3 bucket information.

  1. Enter the name of your S3 bucket.

Corresponds to `stores.[n].bucket` JSON configuration setting.

  2. Specify whether the bucket is Read-only or both Read and write.

Atlas can only query Read-only buckets; if you wish to query and save query
results to your S3 bucket, choose Read and write. To save query results to
your S3 bucket, the role policy that grants Atlas access to your AWS resources
must include the `s3:PutObject` and `s3:DeleteObject` permissions in addition
to the `s3:ListBucket`, `s3:GetObject`, `s3:GetObjectVersion`, and
`s3:GetBucketLocation` permissions, which grant read access. See step 4 below
to learn more about assigning access policy to your AWS IAM role.

  3. Select the region of the S3 bucket.

Corresponds to `stores.[n].region` JSON configuration setting.

## Note

You can't create a federated database instance if Atlas Data Federation is
unable to retrieve the region of the specified S3 bucket.

  4.  **Optional**. Specify a prefix that Data Federation should use when searching the files in the S3 bucket. If omitted, Data Federation does a recursive search for all files from the root of the S3 bucket.

Corresponds to `stores.[n].prefix` JSON configuration setting.

  5. Click Next.

5

#### Assign an access policy to your AWS IAM role.

  1. Follow the steps in the Atlas user interface to assign an access policy to your AWS IAM role.

Your role policy for read-only or read and write access should look similar to
the following:

Read-Only Access

Read-Write Access

    
        {  
      
      "Version": "2012-10-17",  
      "Statement": [  
        {  
          "Effect": "Allow",  
          "Action": [  
            "s3:ListBucket",  
            "s3:GetObject",  
            "s3:GetObjectVersion",  
            "s3:GetBucketLocation"  
          ],  
          "Resource": [  
            <role arn>  
          ]  
        }  
      ]  
    }  
  
  2. Click Next.

6

#### Define the path structure for your files in the S3 bucket and click Next.

For example:

    
    
    s3://<bucket-name>/<path>/<to>/<files>/<filename>.<file-extension>  
      
  
To add additional paths to data on your S3 bucket, click Add Data Source and
enter the path. To learn more about paths, see Define Path for S3 Data.

Corresponds to `databases.[n].collections.[n].dataSources.[n].path` JSON
configuration setting.

7

#### Create the virtual databases, collections, and views and map the
databases, collections, and views to your data store.

  1. (Optional) Click the __for the:

    * Data Lake to specify a name for your federated database instance. Defaults to `Data Lake[n]`.

    * Database to edit the database name. Defaults to `Database[n]`.

Corresponds to `databases.[n].name` JSON configuration setting.

    * Collection to edit the collection name. Defaults to `Collection[n]`.

Corresponds to `databases.[n].collections.[n].name` JSON configuration
setting.

    * View to edit the view name.

You can click:

    * Create Database to add databases and collections.

    *  __associated with the database to add collections to the database.

    *  __associated with the collection to add views on the collection. To create a view, you must specify:

      * The name of the view.

      * The pipeline to apply to the view.

## Note

The view definition pipeline cannot include the `$out` or the `$merge` stage.
If the view definition includes nested pipeline stages such as `$lookup` or
`$facet`, this restriction applies to those nested pipelines as well.

To learn more about views, see:

      * Views

      * db.createView

    *  __associated with the database, collection, or view to remove it.

  2. Select External from the dropdown in the Datasets section.

  3. Drag and drop the data store to map with the collection.

Corresponds to `databases.[n].collections.[n].dataSources` JSON configuration
setting.

8

#### Optional: Repeat steps 1 through 6 in the Visual Editor tab above to
define additional AWS S3 data stores.

To add Atlas or HTTP data stores for federated queries, see:

  * Configure Atlas Data Source from the UI

  * Configure HTTP Data Source from the UI

## Tip

### See also:

  * Running Federated Queries

9

#### Click Save to create the federated database instance.

## Note

If Atlas Data Federation is unable to read the specified S3 bucket, it
displays a modal to:

  * Cancel this operation and specify a different IAM role to retrieve the object metadata from the specified S3 bucket.

  * Use Role Anyway to create the federated database instance for the specified bucket using the specified IAM role.

← AWS S3 BucketGenerate Wildcard Collections →

