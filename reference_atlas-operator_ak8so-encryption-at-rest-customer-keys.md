Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Encrypt Data Using a Key Management Service

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Atlas encrypts all cluster storage and snapshot volumes at rest by default.
You can add another layer of security by using your cloud provider's KMS
together with the MongoDB encrypted storage engine.

You can use one or more of the following customer KMS providers for encryption
at rest in Atlas:

  * AWS KMS

  * Azure Key Vault

  * Google Cloud KMS

## Note

The key management provider doesn't need to match the cluster cloud service
provider.

To learn more about using your KMS with Atlas, see:

  * Encryption at Rest using Customer Key Management.

  * Manage Customer Keys with AWS KMS.

  * Manage Customer Keys with Azure Key Vault.

  * Manage Customer Keys with Google Cloud KMS.

To manage your KMS encryption with Atlas Kubernetes Operator, you can specify
and update the `spec.encryptionAtRest` parameter for the `AtlasProject` Custom
Resource. Each time you change the `spec` field in any of the supported custom
resources, Atlas Kubernetes Operator creates or updates the corresponding
Atlas configuration.

## Prerequisites

AWS KMS

Azure Key Vault

Google Cloud KMS

To configure encryption at rest using AWS KMS in Atlas Kubernetes Operator,
you require:

  * A running Kubernetes cluster with Atlas Kubernetes Operator deployed.

  * The `Project Owner` or `Organization Owner` role in Atlas.

  * Valid key management credentials and an encryption key for AWS KMS. To learn more, see Prerequisites to Enable Customer-Managed Keys with AWS.

  * An assumed IAM role for your Atlas account. To set up an assumed IAM role with the Atlas Kubernetes Operator, see Set Up Unified Cloud Provider Access. To learn more about role-based access for an AWS encryption key, see Manage Customer Keys with AWS KMS.

## Important

If you switch your encryption keys to role-based access, you can't undo the
role-based access configuration and revert to credentials-based access for
encryption keys on that project.

## Procedure

Encypt your Atlas data using a customer-managed key with the following
procedure:

AWS KMS

Azure Key Vault

Google Cloud KMS

1

### Specify the `spec.encryptionAtRest.awsKms` parameter.

  1. Add the `spec.encryptionAtRest.awsKms` object to the `spec.encryptionAtRest` array in the `AtlasProject` Custom Resource, including the following parameters:

Parameter

|

Description  
  
|  
  
`spec.encryptionAtRest.awsKms.` `customerMasterKeyID`

|

Unique alphanumeric string that identifies the AWS customer master key you use
to encrypt and decrypt the MongoDB master keys.  
  
`spec.encryptionAtRest.awsKms.enabled`

|

Flag that indicates whether this project uses AWS KMS to encrypt data at rest.
To enable encryption at rest using AWS KMS, set this parameter to `true`. To
disable encryption at rest using AWS KMS, set this parameter to `false`. If
you disable encryption at rest using AWS KMS, Atlas Kubernetes Operator
removes the configuration details.  
  
`spec.encryptionAtRest.awsKms.region`

|

Label that indicates the AWS region in which the customer master key exists.  
  
`spec.encryptionAtRest.awsKms.roleId`

|

Unique AWS ARN that identifies the AWS IAM role with permission to manage your
AWS customer master key. You can find this in the Roles section of the AWS
Management Console by clicking on the IAM role you edited or created for Atlas
access. AWS displays the ARN in the Summary section.  
  
  2. Run the following command:
    
        cat <<EOF | kubectl apply -f -  
      
    apiVersion: atlas.mongodb.com/v1  
    kind: AtlasProject  
    metadata:  
      name: my-project  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      name: Test Atlas Operator Project  
      encryptionAtRest:  
        awsKms:  
          customerMasterKeyID: "030gce02-586d-48d2-a966-05ea954fde0g"  
          enabled: true  
          region: "US_EAST_1"  
          roleId: "arn:aws:iam::123456789012:role/aws-service-role/support.amazonaws.com/myRole"  
    EOF  
  

2

### Check for successful enablement of encryption at rest on your project.

Run the following command to check whether Atlas Kubernetes Operator detects
the AWS KMS configuration for your project.

    
    
    kubectl get atlasprojects my-project -o=jsonpath='{.status.conditions[?(@.type=="EncryptionAtRestReadyType")].status}  
      
  
HIDE OUTPUT

    
    
    true  
      
  
3

### Enable encryption at rest using customer-managed keys for your cluster.

After you enable encryption at rest using customer-managed keys for your
project, you must enable it at the cluster level to encrypt data.

Run the following command to add the
`spec.deploymentSpec.encryptionAtRestProvider` to your `AtlasDeployment`
Custom Resource, which enables encryption at rest using your AWS key for this
cluster:

    
    
    cat <<EOF | kubectl apply -f -  
      
          apiVersion: atlas.mongodb.com/v1  
          kind: AtlasDeployment  
          metadata:  
            name: my-cluster  
          spec:  
            name: Test Atlas Operator Cluster  
            DeploymentSpec:  
              encryptionAtRestProvider: "AWS"  
          EOF  
  
← Configure Custom Database RolesConfigure Audit Logs →

