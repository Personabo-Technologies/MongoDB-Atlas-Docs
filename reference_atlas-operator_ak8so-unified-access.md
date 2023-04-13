Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up Unified Cloud Provider Access

Share Feedback

On this page

  * Prerequisites
  * Procedure

Some Atlas features, including Data Federation and Encryption at Rest,
authenticate with AWS IAM roles. When Atlas accesses AWS services, assumes an
IAM role.

You can set up an assumed IAM role for your Atlas account to use with the
Atlas Administration API or Atlas UI if you have the `Project Owner` role.
Atlas supports unified access only for AWS.

You can use Atlas Kubernetes Operator to set up unified access for an AWS IAM
role in the `AtlasProject` Custom Resource.

## Prerequisites

You need the following public API key, private API key, and the organization
ID information to configure Atlas Kubernetes Operator access to Atlas.

  * If you want Atlas Kubernetes Operator to create a new Atlas project, Create an API Key in an Organization and configure the API Access List.

## Important

You must assign the API key the Organization Project Creator organization role
or higher.

  * If you want to work with an existing Atlas project, Create an API Key for a Project and configure the API Access List.

## Important

You must assign the API key the Project Owner project role.

To learn more, see Configure Access to Atlas.

## Procedure

1

### Add the `spec.cloudProviderAccessRoles` fields to the `AtlasProject`
custom resource.

  1. Specify an empty value placeholder within the `spec.cloudProviderAccessRoles.iamAssumedRoleArn` parameter of the `AtlasProject` Custom Resource.

  2. Specify `AWS` within the `spec.cloudProviderAccessRoles.providerName` parameter of the `AtlasProject` Custom Resource.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Project  
      projectIpAccessList:  
        - ipAddress: "192.0.2.15"  
          comment: "IP address for Application"  
      cloudProviderAccessRoles:  
      - providerName: "AWS"  
        iamAssumedRoleArn: ""  
    EOF  
  
## Important

Complete this entire procedure to configure the role for the empty value
placeholder before adding any additional access roles to your `AtlasProject`
custom resource.

2

### Retrieve the project's `atlasAWSAccountArn` and
`atlasAssumedRoleExternalId`.

  1. Run the command to retrieve the `atlasAWSAccountArn`, which you need for the next steps.
    
        kubectl get atlasprojects my-project -o=jsonpath='{.status.cloudProviderAccessRoles.atlasAWSAccountArn.type}'  
      
  
HIDE OUTPUT

    
        arn:aws:iam::198765432109:root  
      
  
  2. Run the command to retrieve the `atlasAssumedRoleExternalId`, which you need for the next steps.
    
        kubectl get atlasprojects my-project -o=jsonpath='{.status.cloudProviderAccessRoles.atlasAssumedRoleExternalId.type}'  
      
  
HIDE OUTPUT

    
        1a234b56-c789-0d12-345e-67f89012345a  
      
  

3

### Modify your AWS IAM role trust policy.

You can use an existing IAM role or create a new IAM role for unified access.

Use existing IAM role

Create new IAM role

Modify the trust policy for your AWS IAM role using the following custom trust
policy. Replace the highlighted lines with the values you retrieved in a
previous step.

    
    
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
  
4

### Find the IAM role's ARN in AWS.

In the Roles section of the AWS Management Console, click on the IAM role you
edited or created for Atlas access. AWS displays the ARN in the Summary
section.

5

### Authorize the IAM role's access using Atlas Kubernetes Operator.

Replace the empty value placeholder within the
`spec.cloudProviderAccessRoles.iamAssumedRoleArn` parameter of the
`AtlasProject` Custom Resource with the IAM role's AWS ARN from the previous
step.

 **Example:**

    
    
     cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Project  
      projectIpAccessList:  
        - ipAddress: "192.0.2.15"  
          comment: "IP address for Application"  
      cloudProviderAccessRoles:  
      - providerName: "AWS"  
        iamAssumedRoleArn: "arn:aws:iam::123456789012:role/aws-service-role/support.amazonaws.com/myRole"  
    EOF  
  
6

### Check the status of the `cloudProviderAccessRole`.

  1. Run the command to retrieve the status:
    
        kubectl get atlasprojects my-project -o=jsonpath='{.status.cloudProviderAccessRoles}'  
      
  
  2. Check for the `READY` status.

    * If the status is `CREATED`, Atlas created the role but you have not authorized it within AWS.

    * If the status is `EMPTY_ARN`, Atlas created the role but you have not specified the `spec.cloudProviderAccessRoles.iamAssumedRoleArn`.

    * If the status is `READY`, Atlas has created the role and you have authorized it within AWS.

← Configure Network PeeringConfigure Teams →

