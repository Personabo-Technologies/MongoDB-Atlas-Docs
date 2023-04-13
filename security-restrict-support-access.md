Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure MongoDB Support Access to Atlas Backend Infrastructure

Share Feedback

On this page

  * Block Access at the Organization Level
  * Grant Infrastructure Access to MongoDB Support for 24 hours
  * Grant Sync Data Access to MongoDB Support for 24 hours
  * Revoke Temporary Infrastructure Access to MongoDB Support

As an organization owner, you can set up your Atlas organization so that
MongoDB Production Support Employees, including Technical Service Engineers,
can only access your production servers with your explicit permission. If an
issue that requires MongoDB Support arises and you want to grant 24-hour
temporary infrastructure access to MongoDB Support, you can grant access at
the database deployments level. You can also revoke temporary infrastructure
access at any time prior to the automatic 24-hour expiration.

## Important

Blocking infrastructure access from MongoDB Support may increase support issue
response and resolution time and negatively impact your database deployment's
availability.

## Block Access at the Organization Level

You must be an organization owner to adjust this setting.

1

### Navigate to your Organization Settings.

In the Atlas console, click on your username in the top-right corner and
select Organizations.

2

### Select the organization to which to restrict support access.

3

### Select Settings in the left-side navigation.

4

### Toggle the setting.

Toggle the switch marked Block MongoDB Production Support Employee Access to
Atlas Infrastructure to the On position.

## Grant Infrastructure Access to MongoDB Support for 24 hours

If an issue that requires MongoDB Support arises and you want to allow MongoDB
support staff limited-time access to a database deployment within your
organization, you can do so with the following procedure.

1

### Navigate to your Cluster Overview.

Click Database near the top of the Atlas console.

2

### Locate the database deployment to which to grant access from the list of
database deployments.

3

### Select the ellipsis icon (...) to the right of the database deployment.

4

### Select Grant Temporary Infrastructure Access to MongoDB Support.

5

### Click Grant Access.

## Grant Sync Data Access to MongoDB Support for 24 hours

The procedure you follow to grant sync data access to MongoDB Support for 24
hours depends on whether your organization owner has enabled Block MongoDB
Support Access to Atlas Infrastructure.

Select the tab applicable to your organization.

Support Access Blocked

Support Access Enabled

If App Services sync is enabled and an issue that requires MongoDB Support
arises, you can allow MongoDB support staff limited-time access to App
Services sync data in a database deployment within your organization with the
following procedure.

1

### Navigate to your Cluster Overview.

Click Database near the top of the Atlas console.

2

### Locate the database deployment to which to grant access from the list of
database deployments.

3

### Select the ellipsis icon (...) to the right of the database deployment.

4

### Select Grant Temporary Infrastructure Access to MongoDB Support.

A Grant Infrastructure Access to MongoDB Support for 24 hours modal appears.

5

### Select Grant Infrastructure and App Services Sync Data to grant temporary
infrastructure and sync data access to MongoDB Support.

When you successfully grant temporary access to MongoDB Support, a new item
appears in the dropdown that informs you when your access expires.

## Revoke Temporary Infrastructure Access to MongoDB Support

If you want to revoke access to a database deployment within your organization
that has been granted 24-hour temporary infrastructure access, you can do so
with the following procedure.

## Important

Temporary infrastructure access that is not revoked will automatically expire
at the end of 24 hours. Atlas displays a timer indicating the amount of time
left before 24-hour temporary infrastructure access expires.

1

### Navigate to your Cluster Overview.

Click Database near the top of the Atlas console.

2

### Locate the database deployment to which to grant access from the list of
database deployments.

3

### Select the ellipsis icon (...) to the right of the database deployment.

4

### Select Revoke Temporary Infrastructure Access to MongoDB Support.

## Important

Ensure that all issues requiring MongoDB Support have been addressed before
revoking access.

5

### Click Revoke Access.

Click Revoke Access to revoke temporary infrastructure access.

← Manage Your MongoDB Atlas AccountMigrate or Import Data →

