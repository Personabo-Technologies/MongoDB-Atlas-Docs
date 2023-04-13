Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Live Migrate (Pull) a Sharded Cluster into Atlas

Share Feedback

On this page

  * Restrictions
  * Prerequisites
  * Considerations
  * Migrate Your Sharded Cluster

Atlas can pull a source sharded cluster into an Atlas sharded cluster using
the live migration process. Atlas keeps the target cluster in sync with the
remote source until you cut your applications over to the Atlas target
cluster. Once you reach the cutover step in the following procedure, stop
writes to the source cluster by stopping your application instances, pointing
them to the Atlas cluster, and restarting them.

## Restrictions

  * You can't migrate your sharded cluster to MongoDB v6.0 or later.

  * You can't use a Global Cluster as the target for live migration.

  * Live migration doesn't support VPC peering or private endpoints for either the source or target cluster.

  * During Live Migration, Atlas disables host alerts.

To live migrate a replica set, see Live Migrate (Pull) a Replica Set into
Atlas.

## Prerequisites

  * When you migrate from MongoDB 4.4 or earlier to an Atlas cluster that runs MongoDB 5.0 or later, drop any geoHaystack indexes from your collections.

  * If the source cluster runs with authentication, specify a user to Atlas that exists on every shard _and_ the config server replica set. The user must have permissions to:

    * Stop or start the sharded cluster balancer.

    * Read all databases and collections on the host.

    * Read the oplog on the host.

To learn more, see Source Cluster Security.

## Important

### Source Cluster Readiness

To help ensure a smooth data migration, your source cluster should meet all
production cluster recommendations. Check the Operations Checklist and
Production Notes before beginning the Live Migration process.

### Migration Path

Atlas live migration (pull) supports the following migration paths:

Source Sharded Cluster

MongoDB Version

|

Target Atlas Sharded Cluster

MongoDB Version  
  
|  
  
4.0

|

4.0  
  
4.2

|

4.2  
  
4.4

|

4.4  
  
5.0

|

5.0  
  
## Note

You can't migrate your sharded cluster to MongoDB v6.0 or later.

For sharded clusters, the major MongoDB versions on the source and target
clusters must be exactly the same. The major MongoDB version in the full
**4.4.x** version is **4.4**.

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

Atlas performs a number of validation checks on the source and target clusters
before starting the live migration procedure.

  * The source cluster must be a sharded cluster.

If the source is replica set cluster, use pull-type live migration to migrate
the cluster to a Atlas replica set first, then scale your cluster to a sharded
cluster.

If the source is a standalone, convert the standalone to a replica set first
before using pull-type live migration. Then scale your cluster to a sharded
cluster.

  * The source cluster must use CSRS (Config Server Replica Sets). See Replica Set Config Servers.

  * Atlas must have connectivity to the hostname and port of each node in the source cluster.

  * Atlas must be able to stop and start the Sharded Cluster Balancer on the source cluster.

  * The source cluster has the same feature compatibility version _and_ major MongoDB version as the target cluster. The major MongoDB version in the full **4.4.x** version is **4.4**.

To check the feature compatibility version of a host in the source cluster,
run the following command from `mongosh`:

    
        db.runCommand( { getParameter : 1, "featureCompatibilityVersion" : 1 } )  
      
  
Use the setFeatureCompatibilityVersion database command to set the
`featureCompatibilityVersion` flag as needed.

  * The target Atlas sharded cluster must have the same number of shards as the source sharded cluster.

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
SCRAM for user authentication. To learn how to create database users in Atlas,
see Configure Database Users.

Support for SCRAM authentication began in MongoDB 3.0. If the source cluster
is running MongoDB 2.6, you can migrate it using pull live migration without
enabling SCRAM authentication.

### Source Cluster Balancer

Atlas live migration stops the sharded cluster balancer on the source cluster
at the start of the procedure, and starts the balancer at the end of the
procedure.

If you cancel live migration, Atlas restarts the balancer on the source
cluster.

## Note

Under some circumstances Atlas can't restart the balancer on the source
cluster at the end of a live migration process. If the balancer fails to
restart, the live migration still succeeds but a warning banner indicates that
you must manually restart the source cluster balancer.

### Target Cluster Configuration

When you configure the target Atlas cluster, consider the following:

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

  * You cannot target a Global Cluster as the target for live migration.

## Important

Once you start the live migration process, you can't modify the target Atlas
cluster. To scale up the target cluster, cancel the live migration process,
scale up the cluster, and restart the live migration process.

### Target Cluster Network Access

During live migration, the `mongos` processes on the target cluster are shut
down and cluster connectivity via the `mongos` servers is suspended. The
`mongos` processes restart automatically once the migration is complete.

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

### Canceling Live Migration

You can cancel the process at any time by clicking Cancel. Atlas displays the
Sharded Cluster Live Import in Progress message for the target cluster until
the cluster is ready for normal access.

If you cancel the live migration process before it completes, Atlas doesn't
remove any data migrated up to that point. If you restart the live migration
process using the same Atlas cluster as the target cluster, Atlas wipes all
data from the cluster.

### Testing the Target Cluster

Consider migrating data to your target cluster, then stopping the migration
process and testing your target cluster while leaving the source cluster
running and serving data to your applications.

To test your target cluster with production data, follow the migration
procedure all the way to the testing step. When you're ready to perform the
complete migration process, skip the testing step and proceed to the cutover
step.

## Migrate Your Sharded Cluster

## Note

### Staging and Production Migrations

Consider running a partial live migration procedure first to create a staging
environment before repeating the procedure to create your production
environment. The following procedure includes a callout for the appropriate
time to cancel the procedure and create a staging environment.

Use the staging environment to test application behavior and performance using
the latest driver version that supports the MongoDB version of the target
Atlas cluster. Then, repeat the live migration procedure in full to transition
your applications from your source cluster to the Atlas target cluster.

## Important

Avoid making changes to the source cluster configuration while the live
migration procedure runs, such as removing replica set members or modifying
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

  2. Navigate to the target Atlas cluster and click the ellipsis ... button. On the Cluster list, the ellipsis ... button appears beneath the cluster name, as shown in the following screenshot. When you view a cluster's details, the ellipsis ... appears on the right-hand side of the screen, next to the Connect and Configuration buttons.

click to enlarge

  3. Click Migrate Data to this Cluster.

  4. Atlas displays a walk-through screen with instructions on how to proceed with the live migration. Prepare the information as stated in the walk-through screen, then click I'm Ready To Migrate.

  5. Atlas displays a walk-through screen that collects information required to connect to the source cluster.

    * Atlas displays the IP address of the MongoDB application server responsible for your live migration at the top of the walk-through screen. Configure your source cluster firewall to grant access to the displayed IP address.

    * Enter the hostname and port of any `mongos` of the source sharded cluster into the provided text box. For example, `mongos.example.net:27017`.

    * If the source cluster enforces authentication, enter a username and password into the provided text boxes.

See Source Cluster Security for guidance on the user permissions required by
Atlas live migration.

    * If the source cluster uses `TLS/SSL`, toggle the `SSL` button.

    * If the source cluster uses `TLS/SSL` _and_ is not using a public Certificate Authority (CA), copy the contents of the source cluster's CA file into the provided text box.

  6. Click Validate to confirm that Atlas can connect to the source cluster.

If validation fails, check that:

    * You have granted the Live Migration servers network access on your source cluster firewall.

    * The provided user credentials, if any, exist on the source cluster and have the required permissions.

    * The SSL toggle is enabled only if the source cluster requires it.

    * The CA file provided, if any, is valid and correct.

    * The provided hostnames are valid and reachable over the public internet.

  7. Click Start Migration to start the migration process.

Atlas displays the live migration progress in the UI. During live migration,
you cannot view metrics or access data for the target cluster.

A lag time value is displayed during the final oplog tailing phase that
represents the current lag between the source and target clusters. This lag
time may fluctuate depending on the rate of oplog generation on the source,
but should decrease over time as oplog entries are copied to the target
cluster.

Click View Progress per Shard to view the sync progress and migration time
remaining per shard. If the initial sync process for a given shard fails, you
can try to restart the sync by clicking Restart.

When the lag timer and the Prepare to Cutover button turn green, proceed to
the next step.

2

#### (Optional) Test the target cluster.

Optional. If you wish to skip testing and complete the migration, proceed to
step 3.

If you wish to do a dry run of the migration process and test the target
cluster for performance and data integrity, you may optionally click the
Cancel button at this point. The source cluster stops syncing data with the
target cluster, but all the transferred data remains, so you can test your
applications with the new cluster.

When your testing is complete and you're ready to perform the complete
migration process, begin again from step 1. All the databases and collections
which were created during the test run will be deleted and rebuilt.

3

#### Perform the cutover.

When Atlas detects that the source and target clusters are nearly in sync, it
starts an extendable 120 hour (5 day) timer to begin the cutover stage of the
live migration procedure. If the 120 hour period passes, Atlas stops
synchronizing with the source cluster. You can extend the time remaining by 24
hours by clicking Extend time below the <time> left to cut over timer.

## Important

The cutover procedure requires stopping your application and all writes to the
source cluster. Consider scheduling and announcing a maintenance period to
minimize interruption of service on the dependent applications.

  1. Once you are prepared to cut your applications over to the target Atlas cluster, click Prepare to Cutover.

Atlas displays a walk-through screen with instructions on how to proceed with
the cutover. The optime gap displays how far behind the target cluster is
compared to the source cluster. You must stop your application and all writes
to the source cluster to allow the target cluster to close the optime gap.

Perform the steps described in the walk-through screen to cut over your
applications to the Atlas cluster. These steps are also outlined below:

    1. Stop your application. This ensures that no more writes occur on the source cluster.

    2. Wait for the optime gap to reach zero. When the counter reaches zero, the source and target clusters are in sync.

    3. Restart your application using the new connection string provided in step 3 of the live migration cutover user interface.

## Note

### Staging Migration

If you are creating a staging environment to test your applications, note the
optime gap to identify how far behind your staging environment will be
compared with your source cluster.

Press Cancel to cancel the live migration. Atlas terminates the migration at
that point in time, leaving any migrated data in place. Atlas displays the
Sharded Cluster Live Import in Progress message for the target cluster until
the cluster is ready for normal access. To learn more, see Canceling Live
Migration. Once the cancellation is complete, you can test your staging
application against the partially migrated data.

  2. Click Cut Over when you have completed the cutover sequence and updated your applications to point at the service cluster. The optime gap must be `0:00` before you can complete the procedure.

Atlas automatically prepares the Atlas cluster once you complete the cutover
sequence. During this time, you cannot access the Atlas cluster. Atlas
displays the status of the cluster configuration in the user interface.

Once Atlas displays the cluster as active and ready, you can point your
applications at the Atlas cluster and begin performing write operations.

## Important

Write operations issued to the source cluster after the cutover sequence are
not mirrored to the target Atlas cluster. Check that your applications use the
connection string for the new Atlas cluster before restarting them.

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

← Live Migrate (Pull) a Replica Set into AtlasTroubleshoot Live Migration
(Pull) →

