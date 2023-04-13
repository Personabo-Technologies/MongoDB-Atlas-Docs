Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Database Deployments

Share Feedback

On this page

  * View All Database Deployments
  * View Database Deployment Details
  * Take the Next Steps

Atlas offers the following resources to manage your Atlas clusters and
serverless instances.

## View All Database Deployments

The Database Deployments view displays all clusters and serverless instances
to which the user belongs.

1

### Click Database at the top of the Atlas console.

The Database Deployments page displays.

2

### Use the search box and dropdown menus to filter the list of database
deployments.

The Database Deployments page groups clusters and serverless instances under
their Atlas project.

To filter the returned list of database deployments:

  * Use the search box. Enter the organization name, project name, or cluster/serverless instance name to limit returned database deployments to specific organizations, projects, or clusters/serverless instances.

  * Use the dropdown menus to limit the returned list using one or more of the following filters:

Menu

|

Filter Purpose

|

Menu Options  
  
||  
  
Availability

|

Status of the nodes within the database deployment.

|

    * All

    * Nodes Available

    * Some Nodes Available

    * No Primary

    * Has Warnings &amp; Alerts  
  
Type

|

Deployment type of database deployment.

|

    * All

    * Standalones

    * Replica Sets

    * Sharded Clusters  
  
Version

|

MongoDB versions

|

Version of MongoDB that the database deployments are running.

    * All

    * Inconsistent

    * 4.2

    * 4.4

    * 5.0

## Note

If the FCV of your cluster is set and if the FCV is below the MongoDB version
of your cluster, the cluster in the Atlas UI Database Deployments page shows
the `FCV` of your cluster to reflect the features that are currently available
on your cluster during the upgrade. After Atlas upgrades your cluster to the
new version, the cluster in the Atlas UI Database Deployments page shows the
new MongoDB version of your cluster.  
  
Configuration

|

Additional configuration options for the database deployment including
authentication, backup, and TLS.

|

    * All

    * Auth OFF

    * Backup OFF

    * SSL OFF  
  

To display clusters that have not contacted Atlas in the last 6 months, click
Show Inactive Clusters.

### Database Deployment Information

Atlas returns the following information for each database deployment:

Field

|

Description  
  
|  
  
Name

|

Name of the database deployment.  
  
Version

|

MongoDB Version of the database deployment.  
  
Data Size

|

Size of the database deployment data.  
  
Backup

|

Backup enabled status.  
  
Nodes

|

Number of nodes in the database deployment. This only displays for clusters.  
  
SSL

|

SSL enabled status. This displays only for clusters.  
  
Auth

|

Authentication required status. This displays only for clusters.  
  
Alerts

|

Number of open alerts. This displays only for clusters.  
  
## View Database Deployment Details

Through the Database Deployment Detail view, Atlas displays clusters and
serverless instances grouped into their Project.

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Review the database deployment's' details.

The Atlas consoles displays the following for database deployments in the
selected project:

  * Metadata:

Field

|

Description  
  
|  
  
Database Deployment Name

|

Name of the database deployment.  
  
Version

|

Version of MongoDB that the database deployment runs.  
  
Cluster Tier

|

Cluster tiers such as `M10`, `M30`, or the like (clusters only).  
  
Region

|

Cloud region where Atlas hosts the database deployment.  
  
Type

|

Type of structure for the cluster (i.e., Replica Set or Sharded Cluster), and
number of nodes in the cluster (clusters only).  
  
Linked App Services App

|

Name of the Atlas App Services application linked to this cluster, if
appropriate (clusters only).  
  
  * High-level metrics:

    * Read / write operations per second.

    * Number of open connections to the database deployment.

    * Logical size of database deployment data.

    * Database deployment disk IOPS ( _Available on M10+ clusters_ ).

## Note

Atlas pauses monitoring for these metrics on `M0` clusters without connection
activity for seven days. Atlas indicates which clusters fell into this state
in the Database Deployment Detail view. Atlas limits details displayed for
these clusters.

To resume monitoring, make a successful connection to the cluster using:

  * The Atlas Administration API,

  * A Driver,

  * `mongosh`, or

  * The Atlas UI.

## Take the Next Steps

After you view your database deployments, you can:

Action

|

Description  
  
|  
  
Manage Clusters

|

Manage your Atlas clusters with cluster-specific options.  
  
Manage Serverless Instances

|

Manage your Atlas serverless instances with serverless-specific options.  
  
Manage Global Clusters

|

Manage your Atlas Global Clusters. Atlas Global Clusters require that you
define single or multi-region Zones. You can also shard global collections for
global writes.  
  
← Restore a Collection from Queryable Legacy BackupManage Clusters →

