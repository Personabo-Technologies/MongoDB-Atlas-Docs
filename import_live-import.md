Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Live Migrate (Pull) a Replica Set into Atlas

Share Feedback

On this page

  * Restrictions
  * Prerequisites
  * Considerations
  * Migrate Your Cluster

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Atlas can pull a source replica set to an Atlas cluster using the live
migration process. Atlas keeps the target cluster in sync with the remote
source cluster until you cut your applications over to the target Atlas
cluster.

Once you reach the cutover step in the following procedure, stop writes to the
source cluster: stop your application instances, point them to the Atlas
cluster, and restart them.

## Restrictions

  * You can't select an `M0` (Free Tier) or `M2/M5` shared cluster as the source or target for live migration. To migrate data from an `M0` (Free Tier) or `M2/M5` shared cluster to a paid cluster, change the cluster tier and type.

    * Live migration (pull) doesn't support VPC peering or private endpoints for either the source or target cluster.

To live migrate a sharded cluster, see Live Migrate (Pull) a Sharded Cluster
into Atlas.

  * You can't migrate your cluster to MongoDB v6.0 or later.

  * During Live Migration, Atlas disables host alerts.

## Prerequisites

  * Provide the hostname of the primary node to the live migration service.

  * When you migrate from MongoDB 4.4 or earlier to an Atlas cluster that runs MongoDB 5.0 or later, drop any geoHaystack indexes from your collections.

  * If the cluster runs with authentication, grant the user that will run the migration process the following permissions:

    * Read all databases and collections on the host.

    * Read access to the primary node's oplog.

To learn more Source Cluster Security.

## Important

### Source Cluster Readiness

To help ensure a smooth data migration, your source cluster should meet all
production cluster recommendations. Check the Operations Checklist and
Production Notes before beginning the Live Migration process.

### Migration Path

Atlas live migration (pull) supports the following migration paths:

Source Replica Set

MongoDB Version

|

Target Atlas Replica Set

MongoDB Version  
  
|  
  
2.6

|

4.2.x  
  
3.0

|

4.2.x  
  
3.2

|

4.2.x  
  
3.4

|

4.2.x  
  
3.6

|

4.2.x  
  
4.0

|

4.2.x  
  
4.2

|

4.2.x  
  
4.4

|

4.4.x  
  
5.0

|

5.0.x  
  
## Important

You can't migrate your cluster to MongoDB v6.0 or later.

If you are migrating from a MongoDB 4.0 cluster, update and test your
applications in context of the target Atlas cluster.

#### Network Access

Configure network permissions for the following components:

##### Source Cluster Firewall Allows Traffic from Live Migration Server

Any firewalls for the source cluster must grant the live migration server
access to the source cluster.

The Atlas Live Migration process streams data through a MongoDB-controlled
application server. Atlas provides the IP ranges of the MongoDB Live Migration
servers during the Live Migration process. Grant these IP ranges access to
your source cluster. This allows the MongoDB Live Migration server to connect
to the source clusters.

## Note

If your organization has strict network requirements and you cannot enable the
required network access to MongoDB Live Migration servers, see Live Migrate a
Community Deployment to Atlas.

##### Atlas Cluster Allows Traffic from Your Application Servers

Atlas allows connections to a cluster from hosts added to the project IP
access list. Add the IP addresses or CIDR blocks of your application hosts to
the project IP access list. Do this before beginning the migration procedure.

Atlas temporarily adds the IP addresses of the Atlas migration servers to the
project IP access list. During the migration procedure, you can't edit or
delete this entry. Atlas removes this entry once the procedure completes.

To learn how to add entries to the Atlas IP access list, see Configure IP
Access List Entries.

### Pre-Migration Validation

Before starting the pull live migration procedure, Atlas runs validation
checks on the source and target clusters.

  * The source cluster is a replica set.

If the source cluster is a standalone, convert the standalone to a replica set
first before using the pull-type live migration.

  * The target Atlas cluster is a replica set.

## Note

Unlike for sharded clusters, live migrating your replica set to Atlas doesn't
require that Atlas has connectivity to the hostname and port of each node in
the source cluster. To run the migration process, Atlas automatically
discovers the hostnames for the replica set based on the hostname you provide.
If this fails, Atlas migrates the replica set using your provided reachable
hostname. To learn more, see Network Access.

### Source Cluster Security

Various built-in roles provide sufficient privileges. For example:

  * For source clusters a user must have the `readAnyDatabase`, the `clusterMonitor`, and the `backup` roles.

To verify that the database user that will run the live migration process has
these roles, run the db.getUser() command on the `admin` database.

    
        use admin  
      
    db.getUser("admin")  
    {  
      "_id" : "admin.admin",  
      "user" : "admin",  
      "db" : "admin",  
      "roles" : [  
        {  
          "role" : "backup",  
          "db" : "admin"  
        },  
        {  
          "role" : "clusterMonitor",  
          "db" : "admin"  
        }  
        {  
          "role" : "readAnyDatabase",  
          "db" : "admin"  
        }  
      ]  
    } ...  
  
In addition, the database user from your source cluster must have the role to
read the oplog on your `admin` database. To learn more, see Oplog Access.

  * For source clusters running MongoDB 3.4 a user must have, at a minimum, both `clusterMonitor` and `readAnyDatabase` roles. For example:
    
         use admin  
      
     db.createUser(  
       {  
         user: "mySourceUser",  
         pwd: "mySourceP@$$word",  
         roles: [ "clusterMonitor", "readAnyDatabase" ]  
       }  
     )  
  
  * For source clusters running MongoDB 3.2 a user must have, at a minimum, both `clusterManager` and `readAnyDatabase` roles, as well as read access on the `local` database. This requires a custom role, which you can create with the following commands:
    
          use admin  
      
      db.createRole(  
           {  
             role: "migrate",  
             privileges: [  
               { resource: { db: "local", collection: "" }, actions: [ "find" ] }  
             ],  
             roles: ["readAnyDatabase", "clusterManager"]  
           }  
         )  
       db.createUser(  
           {  
             user: "mySourceUser",  
             pwd: "mySourceP@$$word",  
             roles: [ "migrate" ]  
           }  
         )  
  
  * For source clusters running MongoDB 2.6 or 3.0 a user must have, at a minimum, the `readAnyDatabase` role. For example:
    
          use admin  
      
         db.createUser(  
           {  
             user: "mySourceUser",  
             pwd: "mySourceP@$$word",  
             roles: [ "readAnyDatabase" ]  
           }  
         )  
  

Specify the user name and password to Atlas when prompted by the live
migration procedure.

Atlas only supports SCRAM for connecting to source clusters that enforce
authentication.

Support for SCRAM authentication began in MongoDB 3.0. If the source cluster
is running MongoDB 2.6, you can migrate it using pull live migration without
enabling SCRAM authentication.

If the source cluster uses a different authentication mechanism to connect,
you can use mongomirror to migrate data from the source cluster to the target
Atlas cluster.

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

During pull live migrations, if the source cluster does not use TLS encryption
for its data, the traffic from the source cluster to Atlas is not encrypted.
Determine if this is acceptable before you start a pull live migration
procedure.

### Database Users and Roles

Atlas doesn't migrate any user or role data to the target cluster.

If the source cluster enforced authentication, you must re-create the
credentials that your applications use on the target Atlas cluster. Atlas uses
SCRAM for user authentication. To learn more, see Configure Database Users.

Support for SCRAM authentication began in MongoDB 3.0. If the source cluster
is running MongoDB 2.6, you can migrate it using pull live migration without
enabling SCRAM authentication.

### Target Cluster Configuration

When you configure the target cluster, consider the following:

  * The live migration process streams data through a MongoDB-managed application server. Each server runs on infrastructure hosted in the nearest region to the source cluster. The following regions are available:

Europe

    
    * Frankfurt

    * Ireland

    * London

Americas

    
    * Eastern US

    * Western US

APAC

    
    * Mumbai

    * Singapore

    * Sydney

    * Tokyo

  * Due to network latency, the live migration process may not be able to keep up with a source cluster that has an extremely heavy write load. In this situation, you can still migrate directly from the source cluster by pointing the mongomirror tool to the destination Atlas cluster.

  * The live migration process may not be able to keep up with a source cluster whose write workload is greater than what can be transferred and applied to the target cluster. You may need to scale up the target cluster to a tier with more processing power, bandwidth or disk IO.

  * The target Atlas cluster must be a replica set.

  * You can't select an `M0` (Free Tier) or `M2/M5` shared-tier cluster as the target cluster for live migration.

  * You can't migrate your cluster to MongoDB v6.0 or later.

  * Don't change the `featureCompatibilityVersion` flag while Atlas live migration is running.

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

## Migrate Your Cluster

## Note

### Staging and Production Migrations

Consider running this procedure twice. Run a partial migration that stops at
the Perform the Cutover step _first_. This creates an up-to-date Atlas-backed
staging cluster to test application behavior and performance using the latest
driver version that supports the MongoDB version of the Atlas cluster.

After you test your application, run the full migration procedure using a
separate Atlas cluster to create your Atlas-backed production environment.

## Important

Avoid making changes to the source cluster configuration while the live
migration process runs, such as removing replica set members or modifying
`mongod` runtime settings, such as `featureCompatibilityVersion`.

### Pre-Migration Checklist

Before starting the import process:

  * If you don't already have a destination cluster, create a new Atlas deployment and configure it as needed. For complete documentation on creating an Atlas cluster, see Create a Cluster.

  * After your Atlas cluster is deployed, ensure that you can connect to it from all client hardware where your applications run. Testing your connection string helps ensure that your data migration process can complete with minimal downtime.

    1. Download and install `mongosh` on a representative client machine, if you don't already have it.

    2. Connect to your destination cluster using the connection string from the Atlas UI. For more information, see Connect via `mongosh`.

Once you have verified your connectivity to your target cluster, start the
import procedure.

### Procedure

1

#### Start the migration process.

  1. In the left-side panel of your organization's page, click Live Migration and choose Select Cluster for General Live Migration.

  2. Navigate to the target Atlas cluster and click the ellipsis ... button. On the cluster list, the ellipsis ... button appears beneath the cluster name, as shown in the following screenshot. When you view a cluster's details, the ellipsis ... appears on the right-hand side of the screen, next to the Connect and Configuration buttons.

click to enlarge

  3. Click Migrate Data to this Cluster.

  4. Atlas displays a walk-through screen with instructions on how to proceed with the live migration. The process copies the data from your source cluster to the new target cluster. After you complete the walk-through, you can point your application to the new cluster.

You will need the following details for your source cluster to facilitate the
migration:

    * The hostname and port of the source cluster's primary member

    * The username and password used to connect to the source cluster

    * If the source cluster uses `TLS/SSL` and is not using a public Certificate Authority (CA), you will need the source cluster's CA file.

Prepare the information as stated in the walk-through screen, then click I'm
Ready To Migrate.

  5. Atlas displays a walk-through screen that collects information required to connect to the source cluster.

    * Atlas displays the IP address of the MongoDB application server responsible for your live migration at the top of the walk-through screen. Configure your source cluster firewall to grant access to the displayed IP address.

    * Enter the hostname and port of the primary member of the source cluster into the provided text box. For example, `mongoPrimary.example.net:27017`.

    * If the source cluster enforces authentication, enter a username and password into the provided text boxes.

See Source Cluster Security for guidance on the user permissions required by
Atlas live migration.

    * If the source cluster uses `TLS/SSL`, toggle the `SSL` button.

    * If the source replica set uses `TLS/SSL` _and_ is not using a public Certificate Authority (CA), copy the contents of the source cluster's CA file into the provided text box.

    * If you wish to drop all collections on the target cluster before beginning the migration process, toggle the switch marked Clear any existing data on your target cluster? to Yes.

  6. Click Validate to confirm that Atlas can connect to the source replica set.

If validation fails, check that:

    * You have added Atlas to the IP access list on your source cluster.

    * The provided user credentials, if any, exist on the source cluster and have the required permissions.

    * The SSL toggle is enabled only if the source cluster requires it.

    * The CA file provided, if any, is valid and correct.

  7. Click Start Migration to start the migration process.

Once the migration process begins, the Atlas user interface displays the
Migrating Data walk-through screen for the target Atlas cluster.

The walk-through screen updates as the target cluster proceeds through the
migration process. The migration process includes:

    * Copying collections from the source to the target cluster.

    * Creating indexes on the target cluster.

    * Tailing of oplog entries from the source cluster.

A lag time value displays during the final oplog tailing phase that represents
the current lag between the source and target clusters. This lag time may
fluctuate depending on the rate of oplog generation on the source cluster, but
should decrease over time as the live migration process copies the oplog
entries to the target cluster.

When the lag timer and the Prepare to Cutover button turn green, proceed to
the next step.

2

#### Perform the cutover.

When Atlas detects that the source and target clusters are nearly in sync, it
starts an extendable 120 hour (5 day) timer to begin the cutover stage of the
live migration procedure. If the 120 hour period passes, Atlas stops
synchronizing with the source cluster. You can extend the time remaining by 24
hours by clicking Extend time below the <time> left to cut over timer.

  1. Once you are prepared to cut your applications over to the target Atlas cluster, click Prepare to Cutover.

  2. Atlas displays a walk-through screen with instructions on how to proceed with the cutover. These steps are also outlined below:

    1. Stop your application. This ensures that no more writes occur on the source cluster.

    2. Wait for the optime gap to reach zero. When the counter reaches zero, the source and target clusters are in sync.

    3. Restart your application using the new connection string provided in step 3 of the live migration cutover user interface.

  3. Once you have completed the cutover stage of the procedure and confirm that your application is working with the Atlas cluster, click Cut Over to complete the migration procedure. This allows Atlas to:

    * Remove the Application Server subnets from the target cluster's IP access list.

    * Remove the database user that live migration used to import data to the target cluster.

    * Mark the migration process as complete.

#### Migration Support

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

← Live Migrate: Pull Your Data into AtlasLive Migrate (Pull) a Sharded Cluster
into Atlas →

