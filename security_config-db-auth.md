Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Database Deployment Authentication and Authorization

Share Feedback

On this page

  * Database User Authentication or Authorization
  * Custom Database Roles
  * Passwordless Authentication with AWS IAM
  * User Authentication or Authorization with LDAP
  * User Authentication with X.509

Atlas offers the following security features for database deployment
authentication and authorization.

## Database User Authentication or Authorization

Atlas requires clients to authenticate to access database deployments. You
must create database users to access the database. To set up database users
for your database deployments, see Configure Database Users.

## Custom Database Roles

When the built-in Atlas database user privileges don't meet your desired set
of privileges, you can create custom roles.

## Passwordless Authentication with AWS IAM

You can set up passwordless authentication for your AWS IAM users in the
following ways:

  * Configure AWS IAM roles to make username or password fields optional. To learn more, see Set Up Passwordless Authentication with AWS IAM Roles.

  * Use temporary credentials obtained with the AssumeRoleWithSAML API operation. To learn more, see Set Up Passwordless Authentication Using SAML.

## User Authentication or Authorization with LDAP

Atlas supports performing user authentication and authorization with LDAP. To
use LDAP, see Set up User Authentication and Authorization with LDAP.

## User Authentication with X.509

X.509 client certificates provide database users access to the database
deployments in your project. Options for X.509 authentication include Atlas-
managed X.509 authentication and self-managed X.509 authentication. To learn
more about self-managed X.509 authentication, see Set Up Self-Managed X.509
Authentication.

← Set Up Unified AWS AccessConfigure Database Users →

