Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Administration API Resources

Share Feedback

## Important

Each Atlas API has its own resources and requires initial setup. The Data API
also uses different access keys from the Atlas Administration API and the App
Services Admin API.

To learn more, see APIs.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API provides the resources listed here. The resources
give programmatic access to Atlas's features. For information on the API's
principles and conventions, see API.

The Atlas Administration API provides the following resources:

|  
  
|  
  
Root

|

The starting point for the Atlas Administration API.  
  
Database Users

|

Retrieves and edits the database users who have access to your MongoDB
clusters.  
  
Custom Roles

|

Retrieves and edits custom roles, which specify a custom set of user
privileges on your Atlas project.  
  
Project IP Access List

|

Retrieves and edits the project IP access list, which controls client access
to MongoDB clusters in a given Atlas project.  
  
Organizations

|

Retrieve, rename, or delete Atlas organizations. Invite users to an
organization. Update or delete invitations.  
  
Invoices

|

Retrieve invoices for any given Atlas organization.  
  
Projects

|

Retrieves or creates projects in any given Atlas organization.  
  
Teams

|

Retrieves, creates, edits, or deletes teams for any given Atlas organization.  
  
Clusters

|

Create, retrieve, update, or delete a cluster in a given Atlas project.
Retrieve or update advanced cluster options for a cluster in a given Atlas
project.  
  
Clusters (Advanced)

|

Create, retrieve, update, or delete a multi-cloud cluster in a given Atlas
project.  
  
Serverless Instances

|

Create, retrieve, update, or delete a serverless instance in a given Atlas
project.  
  
Global Clusters

|

Add, remove, and retrieve namespaces, and add and remove custom zone mappings
associated with Global Clusters.  
  
Alerts

|

Retrieves and acknowledges alerts.  
  
Alert Configurations

|

Retrieves and edits alert configurations, which define the conditions that
trigger alerts and the methods of notification.  
  
Maintenance Windows

|

Retrieves and edits preferred maintenance windows. These windows set when you
would prefer Atlas runs its regular maintenance.  
  
LDAP Configuration

|

Create an LDAP configuration request for an Atlas project.  
  
Federated Authentication Configuration

|

Returns, adds, edits, and removes federation-related features such as role
mappings and connected organization configurations.  
  
Atlas Search

|

Retrieves and edits Atlas Search index configurations and analyzers.  
  
Legacy Backup Snapshots

|

Enables you to view snapshot metadata, edit snapshot expiration dates, and
remove existing snapshots. A snapshot is a backup of your data captured at a
specific point in time.  
  
Legacy Backup Snapshot Schedule

|

View or edit the cluster's backup snapshot schedule.  
  
Legacy Backup Restore Job

|

Create and retrieve restores jobs for a MongoDB cluster. A restore job
restores a MongoDB cluster to its state from an existing snapshot or a
specific Continuous Cloud Backup.  
  
Cloud Backup

|

View and delete backup snapshots for an Atlas cluster with Back Up Your
Database Deployment enabled.  
  
Cloud Backup Restore

|

Create or View restore jobs for an Atlas cluster with Back Up Your Database
Deployment enabled.  
  
Cloud Backup Backup Policy

|

View and modify the snapshot schedule and retention settings for an Atlas
cluster with Back Up Your Database Deployment enabled.  
  
Cloud Backup Snapshot Export

|

Create, retrieve, and delete snapshot export buckets and export jobs for an
Atlas cluster with Back Up Your Database Deployment enabled.  
  
Shared-Tier Snapshots

|

View backup snapshots for an `M2` or `M5` shared cluster.  
  
Shared-Tier Restore Jobs

|

View and create restore jobs from an `M2` or `M5` shared cluster.  
  
Legacy Backup Checkpoints

|

Retrieve checkpoints metadata. Checkpoints are additional restore points for
sharded clusters at points in time between regular snapshots.  
  
Network Peering

|

API for managing VPC peering.  
  
Private Endpoints

|

API for managing private endpoints for Atlas dedicated clusters.  
  
Serverless Private Endpoints

|

API for managing private endpoints for Atlas serverless instances.  
  
Programmatic API Keys

|

API for managing programmatic API keys.  
  
Monitoring and Logs

|

Retrieve monitoring and logging data for MongoDB processes in a Atlas project.  
  
Query Analysis

|

Retrieve existing and suggested indexes for a deployment, as well as the
namespaces on which slow queries were run and the queries that were slow. To
learn about monitoring slow queries, see the Performance Advisor monitoring
page.  
  
Auditing

|

View or edit the project's database auditing configuration.  
  
Encryption at Rest using Customer Key Management

|

Enable, disable, configure, and retrieve configuration for Encryption at Rest.  
  
Atlas Users

|

Create or manage Atlas users.  
  
Cloud Provider Access

|

Create or manage AWS IAM roles.  
  
Events

|

Retrieve events for an Atlas organization or project.  
  
Access Tracking

|

View the list of all authentication attempts made against a cluster.  
  
Atlas Data Federation

|

Manage the Atlas Data Federation configuration for a project.  
  
Rolling Index

|

Create a rolling index for a cluster.  
  
Custom DNS for Atlas Clusters Deployed to AWS

|

Retrieve and update custom DNS configuration for an Atlas project's clusters
deployed to AWS.  
  
Triggers

|

Manage Configure Database Triggers.  
  
Live Migration (Push)

|

List, create, and validate push live migrations of deployments to Atlas.  
  
Atlas Data Federation

|

List, create, and validate push live migrations of deployments to Atlas.  
  
What is MongoDB Atlas? →

