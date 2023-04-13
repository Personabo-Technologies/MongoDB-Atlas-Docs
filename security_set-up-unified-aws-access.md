Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up Unified AWS Access

Share Feedback

On this page

  * Overview
  * Prerequisites
  * Procedure
  * Manage AWS IAM Roles

## Overview

Some Atlas features, including Data Federation and Encryption at Rest,
authenticate with AWS IAM roles. When Atlas accesses AWS services, assumes an
IAM role.

You can set up an assumed IAM role for your Atlas account to use with the
Atlas Administration API or Atlas UI if you have the `Project Owner` role.
Atlas supports unified access only for AWS.

## Note

If you have Encryption at Rest enabled for your cluster and you want to set up
a new IAM role, be sure the new role has access to the existing KMS.

## Prerequisites

  * An Atlas account.

  * The AWS Command Line Interface (CLI).

## Procedure

Atlas CLI

Atlas Administration API

Atlas UI

1

### Create a new AWS IAM role in Atlas.

To create an AWS IAM role using the Atlas CLI, run the following command:

    
    
    atlas cloudProviders accessRoles aws create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas cloudProviders accessRoles aws create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

Save the `AtlasAWSAccountArn` and `AtlasAssumedRoleExternalId` field values
returned by the command for use in the next step.

2

### Modify your AWS IAM role trust policy.

  1. Log in to your AWS Management Console.

  2. Navigate to the Identity and Access Management (IAM) service.

  3. Select Roles from the left-side navigation.

  4. Click on the existing IAM role you wish to use for Atlas access from the list of roles.

  5. Select the Trust Relationships tab.

  6. Click the Edit trust relationship button.

  7. Edit the Policy Document. Add a new `Statement` object with the following content.

## Note

Replace the highlighted lines with values returned from the previous step.

    
        {  
      
       "Version":"2012-10-17",  
       "Statement":[  
          {  
             "Effect":"Allow",  
             "Principal":{  
                "AWS":"<atlasAWSAccountArn>"  
             },  
             "Action":"sts:AssumeRole",  
             "Condition":{  
                "StringEquals":{  
                   "sts:ExternalId":"<atlasAssumedRoleExternalId>"  
                }  
             }  
          }  
       ]  
    }  
  
  8. Click the Update Trust Policy button.

3

### Authorize the new IAM role.

To authorize an AWS IAM role using the Atlas CLI, run the following command:

    
    
    atlas cloudProviders accessRoles aws authorize <roleId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas cloudProviders accessRoles aws authorize.

If the command succeeds, you can use the `RoleID` value when configuring Atlas
services that use AWS.

### Resume an Authorization Procedure

If you cancel a procedure to authorize an AWS IAM role for use with Atlas, you
can resume it where you left off.

  1. Expand the Options menu next to your project name in the Atlas UI upper left corner. Select Integrations.

  2. Click the Configure button in the AWS IAM Role Access panel.

Note: if you already have one or more roles configured, the button reads Edit.

  3. Any roles with an ongoing authorization procedure are listed with an `in progress` status. Click the Resume button to resume the authorization process.

To cancel an in-progress role authorization completely, click the Delete icon
next to the in-progress role.

### Deauthorize an Assumed IAM Role

You can deauthorize an existing AWS IAM role from your Atlas account with the
Atlas Administration API or the Atlas UI.

## Note

Be sure to remove any associated Atlas services from the IAM role before you
deauthorize it.

Atlas CLI

Atlas Administration API

Atlas UI

To deauthorize an AWS IAM role using the Atlas CLI, run the following command:

    
    
    atlas cloudProviders accessRoles aws deauthorize <roleId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas cloudProviders accessRoles aws deauthorize.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Manage AWS IAM Roles

Atlas CLI

Atlas Administration API

Atlas UI

To authorize an AWS IAM role using the Atlas CLI, run the following command:

    
    
    atlas cloudProviders accessRoles aws authorize <roleId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas cloudProviders accessRoles aws authorize.

← Set Up a Private Endpoint for a Serverless InstanceConfigure Database
Deployment Authentication and Authorization →

