Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Customer Keys with AWS KMS

Share Feedback

On this page

  * Enable Customer-Managed Keys with AWS KMS
  * Rotate your AWS Customer Master Key
  * Related Topics

## Note

Starting with the 26 January 2021 Release, you must use AWS IAM _roles_
instead of IAM _users_ to manage access to your AWS KMS encryption keys for
customer key management.

When you move from AWS IAM users to roles, ensure that your new role has
access to your old AWS customer master key.

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can configure your Atlas project to use an AWS IAM role for accessing your
AWS KMS keys for encryption at rest. You can either use an existing role or
create a new role when you enable encryption at rest for your project.

This page covers configuring customer key management on your Atlas project for
role-based access.

If you have not yet enabled encryption at rest for your new or existing Atlas
project, follow the Enable Role-Based Access to Your Encryption Key for a
Project procedure to enable encryption at rest for your Atlas project. If you
have an Atlas project for which you have already enabled encryption at rest
and configured credentials-based access to your encryption keys, follow the
Switch to Role-Based Access to Your Encryption Key for a Project procedure to
switch to role-based access to your encryption keys.

You must configure customer key management for the Atlas project before
enabling it on clusters in that project.

## Tip

### See also:

  * Set Up Unified AWS Access

## Enable Customer-Managed Keys with AWS KMS

### Prerequisites

To enable customer-managed keys with AWS KMS for a MongoDB project, you must:

  * Use an M10 or larger cluster.

  * Use Cloud Backups to encrypt your backup snapshots. Legacy Backups are not supported.

  * Have a symmetric AWS KMS key . To learn how to create a key, see Creating Keys in the AWS documentation.

  * Have an AWS IAM role with sufficient privileges. Atlas must have permission to perform the following actions with your key:

    * DescribeKey

    * Encrypt

    * Decrypt

## Note

If you wish to use the AWS KMS key with an AWS IAM role from a different AWS
account instead of that of the IAM role which created the AWS KMS key , ensure
you have sufficient privileges:

    * Add a key policy statement under the AWS KMS key to include the external AWS account.

    * Add an IAM inline policy for the IAM role in the external AWS account.

For a comprehensive discussion of IAM roles and customer master keys, see the
AWS documentation.

After confirming the above privileges, you can follow the usual steps to
configure the KMS settings in Atlas, with the following exception:

    * You must provide the full ARN for the AWS KMS key (e.g. `arn:aws:kms:eu-west-2:111122223333:key/12345678-1234-1234-1234-12345678`) instead of the master key ID (e.g. `12345678-1234-1234-1234-12345678`) in the AWS KMS key ID field.

To learn how to create an IAM role, see IAM Roles in the AWS documentation.

Atlas uses the same IAM role and AWS KMS key settings for all clusters in a
project for which Encryption at Rest is enabled.

  * If your AWS KMS configuration requires it, allow access from Atlas IP addresses and the public IP addresses or DNS hostnames of your cluster nodes so that Atlas can communicate with your KMS. If the node IP addresses change, you must update your configuration to avoid connectivity interruptions.

### Enable Role-Based Access to Your Encryption Key for a Project

UI

API

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Toggle the button next to Encryption at Rest using your Key Management to
On.

3

#### Click the Authorize a new IAM role link to authorize an AWS IAM role to
Atlas to access your AWS KMS keys for encryption at rest.

To create a new AWS IAM role for accessing your AWS KMS keys for encryption at
rest, follow the Create New Role with the AWS CLI procedure. If you have an
existing AWS IAM role that you want to authorize, follow the Add Trust
Relationships to an Existing Role procedure.

4

#### Add an access policy to your AWS IAM role via the AWS console or CLI. See
Managing IAM policies for more information.

The access policy for encryption at rest looks similar to the following:

    
    
    {  
      
      "Version": "2012-10-17",  
      "Statement": [  
        {  
          "Effect": "Allow",  
          "Action": [  
            "kms:Decrypt",  
            "kms:Encrypt",  
            "kms:DescribeKey"  
          ],  
          "Resource": [  
            "arn:aws:kms:us-east-1:123456789012:key/12x345y6-7z89-0a12-3456-xyz123456789"  
          ]  
        }  
      ]  
    }  
  
5

#### Repeat steps 1 and 2 to assign the role you authorized in step 3 to your
project for accessing your encryption key.

6

#### Specify the following for accessing your encryption key and click Save.

  1. Select the role to assign from the AWS IAM role dropdown list.

  2. Specify your encryption key in the Customer Master Key ID field.

  3. Select the AWS region for your encryption key.

### Switch to Role-Based Access to Your Encryption Key for a Project

## Important

If you switch your encryption keys to role-based access, you can't undo the
role-based access configuration and revert to credentials-based access for
encryption keys on that project.

UI

API

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Click Rotate Keys for the Encryption at Rest Section.

3

#### Read the information in the Grant Access to Keys with an AWS IAM Role
section and click Configure.

4

#### Authorize and assign an AWS IAM role to Atlas to access your AWS KMS keys
for encryption at rest.

To create a new AWS IAM role for accessing your AWS KMS keys for encryption at
rest, follow the Create New Role with the AWS CLI procedure. If you have an
existing AWS IAM role that you want to authorize, follow the Add Trust
Relationships to an Existing Role procedure.

### Enable Customer Key Management for an Atlas Cluster

After you Enable Role-Based Access to Your Encryption Key for a Project, you
must enable customer key management for each Atlas cluster that contains data
that you want to encrypt.

## Note

You must have the `Project Owner` role to enable customer key management for
clusters in that project.

For new clusters, toggle the Manage your own encryption keys setting to Yes
when you create the cluster.

For existing clusters:

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Modify the cluster's configuration.

For the cluster that contains data that you want to encrypt, click the
ellipses ..., then select Edit Configuration.

3

#### Enable cluster encryption.

  1. Expand the Additional Settings panel.

  2. Toggle the Manage your own encryption keys setting to Yes.

4

#### Review and apply your changes.

  1. Click Review Changes.

  2. Review your changes, then click Apply Changes to update your cluster.

## Rotate your AWS Customer Master Key

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

When you use your own cloud provider KMS, Atlas automatically rotates the
MongoDB master keys every 90 days. These keys are rotated on a rolling basis
and the process does not require the data to be rewritten.

Atlas does _not_ automatically rotate the AWS customer master key (CMK) used
for AWS-provided Encryption at Rest.

Atlas automatically creates an `alert` to remind you to rotate your CMK every
90 days by default when you enable Encryption at Rest for an Atlas project.

AWS KMS supports automatic CMK rotation. AWS automatic CMK rotation does not
require you to update the Atlas Encryption at Rest project settings, including
the CMK ID.

This page explains how to create a new key and update the CMK ID in Atlas to
rotate your Atlas project CMK. This method of key rotation supports more
granular control of the rotation period compared to AWS KMS automatic CMK
rotation.

## Important

### Cloud Backups with Encryption at Rest

For clusters using Encryption at Rest and Back Up Your Database Deployment,
Atlas uses the project's CMK and AWS IAM user credentials at the time of the
snapshot to automatically encrypt the snapshot data files. This is an
additional layer of encryption on the existing encryption applied to all Atlas
storage and snapshot volumes.

Atlas does _not_ re-encrypt snapshots with the new CMK after rotation. Do
_not_ delete the old CMK until you check _every_ backup-enabled cluster in the
project for any snapshots still using that CMK. Atlas deletes backups in
accordance to the Backup Scheduling, Retention, and On-Demand Snapshots. After
Atlas deletes all snapshots depending on a given CMK, you can delete that CMK
safely.

### Procedure

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Click Rotate Keys for the Encryption at Rest Section.

3

#### Update the AWS CMK details.

  1. Enter the following information:

Field

|

Action  
  
|  
  
AWS IAM role

|

Select an existing AWS IAM role that already has access to your KMS keys, or
authorize a new role and grant this role access to your KMS keys with the
following permissions:

    * DescribeKey

    * Encrypt

    * Decrypt

To learn more, see Role-Based Access to Your Encryption Key for a Project.  
  
Customer Master Key ID

|

Enter your AWS customer master key ID.  
  
Customer Master Key Region

|

Select the AWS region in which you created your AWS CMK.

## Note

Atlas only lists AWS regions that support AWS KMS.  
  
  2. Click Save.

Atlas displays a banner in the Atlas console during the CMK rotation process.
Do **not** delete or disable the CMK until your changes have deployed.

## Related Topics

  * To learn more about MongoDB Encryption at Rest, see Encryption at Rest in the MongoDB server documentation.

  * To learn more about Encryption at Rest with Cloud Backups, see Storage Engine and Cloud Backup Encryption.

← Encryption at Rest using Customer Key ManagementManage Customer Keys with
Azure Key Vault →

