Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Live Migrate (Push) a Replica Set from Ops Manager or Cloud Manager

Share Feedback

On this page

  * Restrictions
  * Prerequisites
  * Considerations
  * Migrate Your Cluster
  * Push Live Migration APIs
  * Push Live Migration CLI Commands

Atlas can facilitate a live migration where Cloud Manager or Ops Manager
pushes a source replica set to an Atlas cluster. Atlas keeps the target
cluster in sync with the source cluster until you cut your applications over
to the target cluster in Atlas.

Once you reach the cutover step in the following procedure, stop the writes to
the source cluster: stop your application instances, point them to the Atlas
cluster, and restart them.

## Restrictions

  * You can't select an `M0` (Free Tier) or `M2/M5` shared cluster as the target for live migration. To migrate data from an `M0` (Free Tier) or `M2/M5` shared cluster to a paid cluster, see Modify a Cluster.

  * You can't live migrate from Cloud Manager or Ops Manager to an Atlas target cluster that has BI Connector for Atlas enabled.

  * You can't live migrate from Ops Manager in local mode to an Atlas target cluster.

  * During Live Migration, Atlas disables host alerts.

To live migrate a sharded cluster, see Live Migrate (Push) a Sharded Cluster
from Ops Manager or Cloud Manager.

### Support for VPC Peering and Private Endpoints

The following table lists the current support status for VPC peering and
private endpoints for source and target replica set clusters that you live
migrate to Atlas.

Cloud Provider

|

VPC Peering

|

Private Endpoints  
  
||  
  
Azure

|

 __

|

 __  
  
AWS

|

 __

|

 __  
  
Google Cloud

|

 __

|

 __  
  
To enable VPC peering with live migration on Azure, AWS, or Google Cloud:

  * Configure a VPC peering connection between the migration host and the target Atlas cluster.

To enable private endpoints with live migration on Azure, AWS, or Google
Cloud:

  * Configure a private endpoint between the migration host and the target Atlas cluster.

## Note

Private endpoints are supported ONLY for live migration of replica sets
deployed within a single cloud provider and single region. Sharded clusters,
multi-region clusters, and multi-cloud clusters don't support live migration
through private endpoints.

## Prerequisites

Before you begin the live migration from Cloud Manager or Ops Manager to
Atlas:

  * Upgrade the source cluster to MongoDB 4.2 or later.

  * Create an Atlas Account.

  * Create an Atlas organization and then create a project in this organization.

  * Ensure that you have the Atlas `Organization Owner` role.

  * Deploy your cluster in this project.

  * Connect to your cluster from all client servers where your applications run.

  * If migrating from Ops Manager, upgrade Ops Manager to version 5.0.

  * When you migrate from MongoDB 4.4 or earlier to an Atlas cluster that runs MongoDB 5.0 or later, drop any geoHaystack indexes from your collections.

  * On your source cluster in Cloud Manager or Ops Manager, prepare the following items:

    * Provision a migration host in Ops Manager, or provision a migration host in Cloud Manager.

    * Obtain the following external IP addresses from your Cloud Manager or Ops Manager administrator:

      * If migrating from Ops Manager, the external IP addresses or CIDR blocks of the Ops Manager instances. If migrating from Cloud Manager, Atlas automatically obtains these addresses.

      * The external IP addresses or CIDR blocks of the provisioned migration hosts in Cloud Manager or Ops Manager.

    * The username and password used to connect to the source cluster.

    * If the source cluster uses TLS/SSL with a Custom Root Certificate Authority, to ensure the hosts can read the certificate, add the source cluster's CA file to the migration hosts.

    * Consider configuring a VPC peering connection or a private endpoint between each migration host and the target Atlas cluster on the same cloud provider and in the same region as the target cluster.

## Note

If you choose not to use VPC peering or private endpoints, the live migration
process runs over public IP addresses that you add to the Atlas project's IP
access list as part of the live migration procedure.

### Live Migration Workflow

This section outlines the workflow. For detailed steps, see the procedure for
migrating a replica set from Ops Manager or Cloud Manager to Atlas.

The stages in the live migration workflow are:

  *  **Stage 1: Link with Atlas**. Perform this step in Atlas, after you have created your Atlas account, organization, and project; deployed your paid cluster in this project; and can connect to it.

    1. In the Atlas organization, go to Live Migration.

    2. Select Migrate from Ops Manager or Cloud Manager and start the Live Migration wizard.

    3. If you are migrating from MongoDB Community using Ops Manager, accept the Ops Manager Migration Agreement.

    4. If you are migrating from Ops Manager, enter the external IP addresses of your Ops Manager instances to the Atlas access list. If you are migrating from Cloud Manager, skip this step.

  *  **Stage 2: Provision Migration Host**.

    * Provision a migration host in Ops Manager, or provision a migration host in Cloud Manager. A migration host runs a dedicated MongoDB Agent that orchestrates the live migration process from Cloud Manager or Ops Manager to Atlas.

    * In the Live Migration: Connect to Atlas section of your Cloud Manager or Ops Manager organization's Settings page, select Connect to Atlas and paste the link-token that you created in Atlas. To learn more, see Connect to Atlas for Live Migration in Ops Manager, or Connect to Atlas for Live Migration in Cloud Manager.

  *  **Stage 3: Start the Migration**. In Atlas, follow the steps in the wizard to start the Live Migration process.

### Migration Path and Supported Platforms

Live Migration from Cloud Manager or Ops Manager to Atlas is supported for all
platforms on which you can provision a migration host. For a full list of
supported platforms on which you can provision a migration host, see Cloud
Manager Prerequisites in Cloud Manager or Ops Manager Prerequisites in Ops
Manager.

If you want to live migrate your data from a Windows- or macOS-based
deployment to Atlas, you must provision your migration host on one of the
supported platforms.

Atlas live migration (push) supports the following migration paths:

Source Replica Set

MongoDB Version

|

Target Atlas Replica Set

MongoDB Version  
  
|  
  
4.2

|

4.2 and later  
  
4.4

|

4.4 and later  
  
5.0

|

5.0  
  
#### Network Access for Live Migrating from Ops Manager or Cloud Manager

Contact your Cloud Manager or Ops Manager service administrator and obtain
external IP addresses for the following components:

##### External IP Address of the Source Cluster in Ops Manager

If you are migrating from Ops Manager, the live migration service in Atlas
requires an external IP address or an external CIDR block of the Ops Manager
instance in the source cluster deployment. This address could be from a single
Ops Manager instance, or, if the source deployment uses multiple Ops Manager
instances, from the gateway the Ops Manager instances will use to reach Atlas.

The live migration service uses this external IP address when generating a
link-token. A link-token is a string that contains the information necessary
to connect from Cloud Manager or Ops Manager to Atlas during a Live Migration
from a Cloud Manager or Ops Manager deployment to a cluster in Atlas.

##### External IP Address of the Migration Host in Ops Manager or Cloud
Manager

Before you begin the Live Migration procedure, add the IP addresses or CIDR
blocks of your migration hosts to the project IP access list. Atlas allows
connections to the target cluster only from hosts with entries in the
project's access list.

### Pre-Migration Validation

Before starting the live migration procedure, Atlas runs validation checks on
the source and target clusters.

  * The source cluster is a replica set.

If the source cluster is a standalone, convert the standalone MongoDB node in
Ops Manager, or convert the standalone MongoDB node in Cloud Manager to a
single-node replica set and then live migrate it to Atlas using the procedure
in this section.

  * The target Atlas cluster is a replica set.

  * The target Atlas cluster doesn't have BI Connector for Atlas enabled.

### Index Key Limits

If your MongoDB deployment contains indexes with keys which exceed the Index
Key Limit, before you start the live migration procedure, modify indexes so
that they do not contain oversized keys. To learn more about about strategies
for dealing with oversized keys, see `failIndexKeyTooLong` in the MongoDB
Server documentation.

## Important

### Index Key Limit

`failIndexKeyTooLong` was deprecated in MongoDB version 4.2 and is removed in
MongoDB 4.4 and later. For MongoDB prior to 4.2, set this parameter to
`false`.

## Considerations

### Network Encryption

During push live migrations, if the source cluster does not use TLS encryption
for its data, the traffic from the source cluster to the migration host is not
encrypted, but the traffic from the migration host to Atlas is encrypted.
Determine if this is acceptable before you start a push live migration
procedure.

### Database Users and Roles

Atlas doesn't migrate any user or role data to the target cluster.

If the source cluster enforced authentication, before you migrate you must re-
create the appropriate authentication mechanism used by your applications on
the target Atlas cluster. The following table lists authentication mechanisms
and how to configure them in Atlas.

Authentication Mechanism

|

Configuration Method  
  
|  
  
SCRAM

|

Create database users with SCRAM for password authentication.  
  
LDAP

|

Set up LDAP.  
  
AWS KMS, Azure Key Vault, Google Cloud KMS

|

Set up KMS encryption.  
  
### Target Cluster Configuration

For the target cluster, consider the following:

  * The live migration process may not be able to keep up with a source cluster whose write workload is greater than what can be transferred and applied to the target cluster. You may need to scale up the target cluster to a tier with more processing power, bandwidth or disk IO.

  * The target Atlas cluster must be a replica set.

  * You can't select an `M0` (Free Tier) or `M2/M5` shared-tier cluster as the target for live migration.

  * Do **not** change the `featureCompatibilityVersion` flag while Atlas live migration is running.

### Avoid Workloads on the Target Cluster

Avoid running any workloads, including those that might be running on
namespaces that don't overlap with the live migration process, on the target
cluster. This action avoids potential locking conflicts and performance
degradation during the live migration process.

Don't run multiple migrations to the same target cluster at the same time.

Don't start the cutover process for your applications to the target cluster
while the live migration process is syncing.

### Avoid Cloud Backups

Atlas stops taking on-demand cloud backup snapshots of the target cluster
during live migration. Once you complete the cutover step in the live
migration procedure on this page, Atlas resumes taking cloud backup snapshots
based on your backup policy.

### Avoid Namespace Changes

Don't make any namespace changes during the migration process, such as using
the `renameCollection` command or executing an aggregation pipeline that
includes the `$out` aggregation stage.

### Avoid Elections

The live migration process makes a best attempt to continue a migration during
temporary network interruptions and elections on the source or target
clusters. However, these events might cause the live migration process to
fail. If the live migration process can't recover automatically, restart it
from the beginning.

### Rolling Restarts

After the migration process completes, your cluster restarts each of its
members one at a time. This is called a rolling restart, and as a consequence,
a failover will occur on the primary. To ensure a smooth migration, consider
running a Test Primary Failover procedure before migrating your data to the
target cluster.

### Staging and Production Environments

Consider running the following procedure twice. Perform a partial migration
that stops at the Perform the Cutover step _first_. This creates an up-to-date
Atlas-backed staging cluster to test application behavior and performance
using the latest driver version that supports the MongoDB version of the Atlas
cluster.

After you test your application, run the full migration procedure using a
separate Atlas cluster to create your Atlas-backed production environment.

### Migrating from MongoDB Community

If you are migrating to Atlas from MongoDB Community using Ops Manager, you
must accept the Ops Manager Migration Agreement as the first step in the Live
Migration procedure.

## Migrate Your Cluster

## Important

Avoid making changes to the source cluster configuration while the live
migration procedure runs, such as removing replica set members or modifying
`mongod` runtime settings, such as `featureCompatibilityVersion`.

### Procedure

1

#### Start the migration process.

  1. In the left-side panel of your organization's page, click Live Migration.

  2. Click Migrate from Ops Manager or Cloud Manager.

  3. Click I'm Ready to Start and, if you are migrating from MongoDB Community using Ops Manager, click Ops Manager License Agreement to read and accept it. To read the agreement outside of the Live Migration Wizard, see the Ops Manager Migration Agreement.

Atlas displays a Live Migration wizard with instructions on how to proceed
with the process. The process pushes the data from your source cluster to the
new target cluster. After you complete the wizard steps, you can point your
application to the new cluster.

2

#### Link with Atlas.

  1. Click Generate Link-Token. Atlas displays the page for generating a link-token.

    * If you are migrating from Ops Manager, enter the external IP addresses or a CIDR block of your Ops Manager instances to add them to the access list of the API Key embedded in the link-token. This allows Ops Manager to send project and cluster information to Atlas. Ops Manager does not send any data stored in your MongoDB databases in this step. For example, enter `23.248.95.14`.

    * If you are migrating from Cloud Manager, skip this step.

  2. Click Next to see a page that contains the generated link-token.

  3. Copy the link-token and store it in a secure location. Atlas never displays the contents of the link-token. Atlas also does not display the link-token after generating it. Do not share it publicly.

## Note

Use one unique link-token for live migrating all projects in one Cloud Manager
or Ops Manager organization to Atlas.

  4. Click Done.

3

#### Paste the link-token into Ops Manager or Cloud Manager.

  1. Access the organization in Cloud Manager or Ops Manager:

Open Ops Manager or Cloud Manager, and navigate to the organization whose
project's cluster you are live migrating to Atlas.

  2. Click Settings in the left navigation panel.

  3. In the Live Migration: Connect to Atlas section, click Connect to Atlas. The Connect to Atlas dialog opens.

  4. Paste the link-token you generated in the previous step of the Live Migration wizard and click Connect to Atlas. Cloud Manager or Ops Manager establishes the connection to Atlas. Use the Refresh button to send an update to Atlas, if needed. To learn more, see Connect to Atlas for Live Migration in Ops Manager, or Connect to Atlas for Live Migration in Cloud Manager.

4

#### Create the target Atlas cluster.

If you haven't already, create a target cluster in Atlas. See Prerequisites.

5

#### Initiate the migration from the target cluster.

  1. Click Select Target Cluster from Projects.

  2. Go to your target Atlas cluster's project and find your target cluster.

  3. Click __and select Migrate Data to this Cluster from the dropdown list to start the migration. The Migrate Data to This Cluster page opens.

  4. Click Migrate from Ops Manager or Cloud Manager and fill in the fields as follows:

    * Select the source project in Cloud Manager or Ops Manager, if it is not already selected.

    * Select a migration host for handling the migration.

    * Review the IP address access list and check that the migration host's external IP address is included in this list. If it is not added, add it now:

      * Click Set Network Access for Host

      * Click \+ Add IP Address

      * Return to the Live Migration wizard. Select the source cluster from the dropdown and choose Migrate data to this cluster under __.

    * Select the source cluster from the drop-down.

    * If you suspend the source cluster from automation in Cloud Manager or Ops Manager, but continue to monitor the source cluster with the Monitoring Agent, the Username and Password display. If your deployment requires user authentication, provide the user name and password in these fields. The database user whose credentials you provide must have at least the backup role on the admin database and must be authenticated using both SCRAM-SHA-1 and SCRAM-SHA-256.

    * If the source cluster uses TLS/SSL, toggle the Is TLS enabled on the source cluster? button.

    * If the source cluster uses TLS/SSL with a custom Root Certificate Authority (CA), copy the path to the CA file from your migration host and paste this path into the provided text box. The file must be present on the migration host to ensure the migration host can read the certificate. Atlas check that the certificate is present and readable.

    * If your replica set target cluster has data, and you want to preserve it, keep the Clear any existing data on your target cluster option unchecked. The live migration service warns you if it finds duplicate namespaces. If you want to delete the existing data, check this option.

    * Choose a connection to connect to the cluster. The Standard connection always shows as available in the UI. However, other connection options are enabled only if you have previously configured a VPC peering connection or a private endpoint. If Atlas detects that you don't have VPC connections or private endpoints configured, these options are grayed out.

      * If you aren't using VPC peering or a private endpoint, click Standard connection and proceed to the Validation stage of this step.

      * If you configured a VPC peering connection between the migration host and the Atlas cluster, the VPC Peering option is active. Click VPC Peering to connect using VPC peering for live migration. If the VPC Peering option is grayed out, configure a VPC peering connection before starting this procedure. To learn more, see Support for VPC Peering and Private Endpoints.

      * If you are migrating a replica set and configured a private endpoint between the migration host and the Atlas cluster, the Private Endpoint option is active. Click Private Endpoint to connect with a private endpoint, and then select a previously-configured private endpoint from the dropdown. Only private endpoints that are in `AVAILABLE` state are valid. If the Private Endpoint option is grayed out, configure a private endpoint before starting this procedure. To learn more, see Support for VPC Peering and Private Endpoints.

## Note

Private endpoints are supported ONLY for live migration of replica sets
deployed within a single cloud provider and single region. Sharded clusters,
multi-region clusters, and multi-cloud clusters don't support live migration
through private endpoints.

    * Click Validate. The validation process verifies that your migration host is reachable, and performs the following validation checks to ensure that you can start live migration to Atlas.

To take advantage of the following validation checks, upgrade the MongoDB
Agent in Ops Manager, or upgrade the MongoDB Agent in Cloud Manager to the
latest version. If the live migration process detects that the source cluster
is running a version of MongoDB Agent earlier than 12.0.11.7606 for Ops
Manager, or 12.5.0.7713 for Cloud Manager, it displays a banner warning
suggesting that you upgrade the MongoDB Agent.

The following validation checks run during the live migration:

      * The migration host can connect to the target cluster.

      * If the source cluster uses TLS/SSL with a custom Root Certificate Authority (CA), the migration host can access the source cluster using TLS/SSL.

      * The database user credentials are valid. This validation check runs only if you suspend the source cluster from automation in Cloud Manager or Ops Manager, but continue to monitor the source cluster with the Monitoring Agent.

      * If you are migrating from Ops Manager before version 5.0.9, the live migration process validates that the target cluster has enough disk space based on the data size. If you are migrating from Cloud Manager or Ops Manager 5.0.9 or later, the migration process validates that the target cluster has enough disk space based on the storage size of the compressed data. To learn more about data and storage sizes, see dbStats.

    * If validation fails, check the migration host, the validity of your external IP addresses or CIDR block, and the link-token. Also check the database user credentials, your TLS/SSL certificates, and the amount of disk storage size on the target cluster.

    * If validation succeeds, click Next. The Migrate from Ops Manager or Cloud Manager page displays.

6

#### Start the migration.

  1. Review the report listing your source organization, project and cluster, and the migration host that the live migration process will use.

  2. Click Start the Migration.

7

#### Prepare to Cut Over.

A lag time value dispays during the final oplog tailing phase that represents
the current lag between the source and target clusters. This lag time may
fluctuate depending on the rate of oplog generation on the source cluster, but
should decrease over time as the live migration process copies the oplog
entries to the target cluster.

  1. When the lag timer and the Prepare to Cutover button turn green, click it to proceed to the next step.

8

#### Perform the cutover.

When Atlas detects that the source and target clusters are nearly in sync, it
starts an extendable 120 hour (5 day) timer to begin the cutover stage of the
live migration procedure. If the 120 hour period passes, Atlas stops
synchronizing with the source cluster. You can extend the time remaining by 24
hours by clicking Extend time below the <time> left to cut over timer.

To finish migrating your MongoDB data to your Atlas cluster, complete the
following steps on the Your migration is almost complete! page:

  1. Prepare to point to your Atlas cluster. Copy the new connection string so that you can update it and point your application to the target Atlas cluster.

  2. Stop your application. This action ensures that no more writes occur on the source cluster.

  3. Wait for the optime gap to reach zero. When the counter reaches zero, the source and target clusters are in sync.

  4. Wait for additional time until Atlas configures your target cluster and it is ready to use. For smaller clusters, this time is 3-5 minutes. For larger clusters, this time can extend up to 10 minutes or longer, depending on the cluster size and configuration.

  5. Restart your application using the new Atlas connection string and confirm that your application is working with the Atlas cluster.

  6. Click Cut Over to complete the migration process.

If you click Cancel on the live migration progress bar, Atlas stops
synchronizing writes from the source cluster. All migrated data remains on
your Atlas cluster.

You can click Cut Over again to allow Atlas to complete the migration process.

## Push Live Migration APIs

To run tasks associated with the live migration procedure, see Push Live
Migration API.

### Migration Support

If you have any questions regarding migration support beyond what is covered
in this documentation, or if you encounter an error during migration, please
request support through the Atlas UI.

To file a support ticket:

  1. Click Support in the left-hand navigation.

  2. Click Request Support.

  3. For Issue Category, select `Help with live migration`.

  4. For Priority, select the appropriate priority. For questions, please select `Medium Priority`. If there was a failure in migration, please select `High Priority`.

  5. For Request Summary, please include `Live Migration` in your summary.

  6. For More details, please include any other relevant details to your question or migration error.

  7. Click the Request Support button to submit the form.

## Push Live Migration CLI Commands

To migrate a cluster using the Atlas CLI, you can perform the following steps:

  * Create or delete a link-token

  * Create or view a validation job

  * Create or view a migration job

  * Perform the cutover

For other steps in the live migration procedure, you must use the Cloud
Manager UI or the Atlas UI. To learn more, see the live migration workflow.

Before you migrate a cluster using the Atlas CLI, complete the pre-migration
validation.

## Note

Before you run any Atlas CLI commands, you must:

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Create or Delete a Link-Token

To create a new link-token using the Atlas CLI, run the following command:

    
    
    atlas liveMigrations link create [options]  
      
  
To delete the link-token you specify using the Atlas CLI, run the following
command:

    
    
    atlas liveMigrations link delete [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas liveMigrations link create and atlas
liveMigrations link delete.

If you are migrating from Ops Manager, request an external IP address and
specify it in the link-token. To learn more, see Request an External IP
Address in the Ops Manager documentation.

### Create and View a Validation Job

To create a new validation request using the Atlas CLI, run the following
command:

    
    
    atlas liveMigrations validation create [options]  
      
  
To return the details for the validation request you specify using the Atlas
CLI, run the following command:

    
    
    atlas liveMigrations validation describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas liveMigrations validation create and
atlas liveMigrations validation describe.

To learn what Atlas validates, see the Validate bullet in the Migrate Your
Cluster section on this page.

### Create and View a Migration Job

To create one new migration job using the Atlas CLI, run the following
command:

    
    
    atlas liveMigrations create [options]  
      
  
To return the details of the migration job you specify using the Atlas CLI,
run the following command:

    
    
    atlas liveMigrations describe [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas liveMigrations create and atlas
liveMigrations describe.

### Perform the Cutover

To start the cutover for live migration using the Atlas CLI, run the following
command:

    
    
    atlas liveMigrations cutover [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas liveMigrations cutover.

When the cutover completes, Atlas completes the live migration process and
stops synchronizing with the source cluster. To learn more, see the Migrate
Your Cluster section on this page.

← Live Migrate: Push Your Data from Cloud Manager or Ops Manager to AtlasLive
Migrate (Push) a Sharded Cluster from Ops Manager or Cloud Manager →

