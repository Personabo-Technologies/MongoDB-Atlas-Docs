Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up Passwordless Authentication with AWS IAM

Share Feedback

On this page

  * Set Up Passwordless Authentication with AWS IAM Roles
  * AWS Lambda
  * AWS ECS
  * AWS ECS Fargate
  * AWS EKS
  * Set Up Passwordless Authentication Using SAML

You can set up passwordless authentication for your AWS IAM users in the
following ways:

  * Configure AWS IAM roles to make username or password fields optional. In this scenario, each user presents the secret key for authentication. The user does not send the secret key over the wire to Atlas and the driver does not persist it. To learn more, see Set Up Passwordless Authentication with AWS IAM Roles.

  * Use temporary credentials obtained with the AssumeRoleWithSAML API operation. In this scenario, you must integrate with an SSO provider, and have an IAM role that specifies your SAML IdP provider in its trust policy. To learn more, see Set Up Passwordless Authentication Using SAML.

## Set Up Passwordless Authentication with AWS IAM Roles

You can set up a database user to use an AWS IAM user ARN for authentication.
You can connect to your database using `mongosh` and drivers and authenticate
using your AWS IAM user ARN. Using AWS IAM role reduces the number of
authentication mechanisms and number of secrets to manage. You can configure
AWS IAM to not require a username or password to authenticate, thus making it
a passwordless mechanism. The secret key that you use instead for
authentication is not sent over the wire to Atlas and is not persisted by the
driver, thus making AWS IAM suitable for even the most sensitive situations.

For AWS Lambda and HTTP (ECS and EC2), drivers automatically read from the
environment variables. For AWS EKS, you must manually assign the IAM role.
This page describes how AWS Lambda, AWS ECS, and AWS EKS can connect using an
AWS IAM role.

## Note

You must assign an IAM role to Lambda, EC2, ECS, or EKS in the AWS console.

### AWS Lambda

AWS Lambda passes information to functions through the following environment
variables if you assign an execution role to the lambda function:

  * `AWS_ACCESS_KEY_ID`

  * `AWS_SECRET_ACCESS_KEY`

  * `AWS_SESSION_TOKEN`

To learn more about these environment variables, see Using AWS Lambda
environment variables.

### AWS ECS

AWS ECS gets the credentials from the following URI:

    
    
    http://169.254.170.2 + AWS_CONTAINER_CREDENTIALS_RELATIVE_URI  
      
  
`AWS_CONTAINER_CREDENTIALS_RELATIVE_URI` is an environment variable. To learn
more, see IAM Roles for Tasks.

AWS EC2 gets the credentials from Instance Metadata Service V2 at the
following URL:

    
    
    http://169.254.169.254/latest/meta-data/iam/security-credentials/  
      
  
To learn more, see Launch an instance with an IAM role.

### AWS ECS Fargate

To learn how to configure an AWS IAM role for passwordless authentication with
AWS ECS Fargate, see the AWS documentation.

### AWS EKS

For AWS EKS, you must first assign the IAM role to your pod to set up the
following environment variables in that pod:

  * `AWS_WEB_IDENTITY_TOKEN_FILE` \- contains the path to the web identity token file.

  * `AWS_ROLE_ARN` \- contains the IAM role that you want to use to connect to your database deployment.

For information on assigning an IAM role to your pod, see the AWS
documentation.

After you assign the IAM role to your pod, you must manually assume the IAM
role to connect to your database deployment.

To assume the role manually:

  1. Use the AWS SDK to call AssumeRoleWithWebIdentity.

## Tip

    * Omit the `ProviderID` parameter.

    * Find the value of the `WebIdentityToken` parameter in the file described in your pod's `AWS_WEB_IDENTITY_TOKEN_FILE` environment variable.

  2. Pass the credentials that you received in the previous step to the MongoDB driver. See your driver's documentation for details.

## Tip

### See also:

IAM roles for service accounts

## Set Up Passwordless Authentication Using SAML

If you integrate your AWS IAM users with an IdP that relies on SAML
authentication, you can use your enterprise's corporate SSO provider to:

  * Access Atlas.

  * Establish passwordless authentication for your MongoDB database user to connect to Atlas. `mongosh` and MongoDB drivers may then use this database user to connect to Atlas.

For this MongoDB database user, you can use temporary security credentials
that you obtain with the AssumeRoleWithSAML API operation.

In this scenario, you must already have:

  * A SAML SSO provider configured.

  * An existing IdP role that specifies your SAML IdP provider in its trust policy.

The following steps show how to set up passwordless authentication for a
MongoDB database user. To learn more, use the links for each stage in the
workflow.

To set up passwordless authentication for your MongoDB database user when your
enterprise uses an SSO provider with SAML and integrates with AWS IAM:

  1. Create a role to delegate permissions to an IAM user.

  2. Request temporary security credentials from the delegated role. The AWS Security Token Service creates temporary security credentials when you call the AssumeRoleWithSAML API operation.

  3. Use your temporary API key, access key, and token to authenticate with Atlas database deployments.

← Configure Custom Database RolesSet Up User Authentication and Authorization
with LDAP →

