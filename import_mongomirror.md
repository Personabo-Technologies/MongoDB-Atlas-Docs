Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Migrate with `mongomirror`

Share Feedback

On this page

  * Upgrade Path
  * Download `mongomirror`
  * Prerequisites
  * `mongomirror` Process
  * Run `mongomirror`
  * Switch to Atlas
  * Monitoring
  * Performance
  * Command Syntax, Options, and Examples
  * Troubleshooting

`mongomirror` is a tool for manually migrating data from an existing MongoDB
replica set to a MongoDB Atlas replica set. `mongomirror` does not require you
to shut down your existing replica set or applications, and does not import
user or role data or copy the `config` database.

Use `mongomirror` for:

  * Running a one-time migration of a dataset into a MongoDB Atlas cluster from a MongoDB deployment hosted outside of MongoDB Atlas.

  * Running a one-time migration of a dataset from one Atlas cluster into another Atlas cluster.

See also Choosing a Data Import and Migration Tool.

## Upgrade Path

`mongomirror` supports the following migration paths.

## Important

You can't use `mongomirror` to migrate from a source replica set 6.0.+ to a
target replica set 6.0.+. To migrate replica sets 6.0.+, use Cluster-to-
Cluster Sync.

Source Replica Set

MongoDB Version

|

Target Atlas Replica Set

MongoDB Version  
  
|  
  
5.0

|

4.4, 5.0  
  
4.4

|

4.2, 4.4, 5.0  
  
4.2

|

4.2, 4.4, 5.0  
  
4.0

|

4.2, 4.4, 5.0  
  
3.6

|

4.2, 4.4, 5.0  
  
3.4

|

4.2, 4.4, 5.0  
  
3.2

|

4.2, 4.4, 5.0  
  
3.0

|

4.2, 4.4, 5.0  
  
2.6

|

4.2, 4.4, 5.0  
  
## Note

To downgrade from 5.0 to 4.4, or 4.4 to 4.2, the source `FCV` must match the
target.

## Download `mongomirror`

## Note

On macOS 64-bit, a security alert appears when you first try to open the
`mongomirror` file after you have downloaded it. To proceed, see Open an app
by overriding security settings.

Operating System

|

Download  
  
|  
  
Amazon Linux 1

|

mongomirror-linux-x86_64-enterprise-amzn64-0.12.8.tgz  
  
Amazon Linux 2

|

mongomirror-linux-x86_64-enterprise-amazon2-0.12.8.tgz  
  
Debian 8.1

|

mongomirror-linux-x86_64-debian81-0.12.8.tgz  
  
Debian 9.2

|

mongomirror-linux-x86_64-debian92-0.12.8.tgz  
  
Debian 10

|

mongomirror-linux-x86_64-debian10-0.12.8.tgz  
  
macOS 64-bit

|

mongomirror-osx-x86_64-0.12.8.tgz  
  
RHEL 6.2

|

mongomirror-linux-x86_64-rhel62-0.12.8.tgz  
  
RHEL 7.0

|

mongomirror-linux-x86_64-rhel70-0.12.8.tgz  
  
RHEL 7.1 PPC64LE

|

mongomirror-linux-ppc64le-rhel71-0.12.8.tgz  
  
RHEL 8.0

|

mongomirror-linux-x86_64-rhel80-0.12.8.tgz  
  
RHEL 8.0 s390x

|

mongomirror-linux-s390x-rhel80-0.12.8.tgz  
  
RHEL 8.1 PPC64LE

|

mongomirror-linux-ppc64le-rhel81-0.12.8.tgz  
  
SLES 12

|

mongomirror-linux-x86_64-suse12-0.12.8.tgz  
  
SLES 15

|

mongomirror-linux-x86_64-suse15-0.12.8.tgz  
  
Ubuntu 14.04

|

mongomirror-linux-x86_64-ubuntu1404-0.12.8.tgz  
  
Ubuntu 16.04

|

mongomirror-linux-x86_64-ubuntu1604-0.12.8.tgz  
  
Ubuntu 16.04 ARM

|

mongomirror-linux-arm64-ubuntu1604-0.12.8.tgz  
  
Ubuntu 16.04 PPC64LE

|

mongomirror-linux-ppc64le-ubuntu1604-0.12.8.tgz  
  
Ubuntu 18.04

|

mongomirror-linux-x86_64-ubuntu1804-0.12.8.tgz  
  
Ubuntu 18.04 ARM

|

mongomirror-linux-arm64-ubuntu1804-0.12.8.tgz  
  
Ubuntu 18.04 PPC64LE

|

mongomirror-linux-ppc64le-ubuntu1804-0.12.8.tgz  
  
Ubuntu 20.04

|

mongomirror-linux-x86_64-ubuntu2004-0.12.8.tgz  
  
Ubuntu 20.04 ARM

|

mongomirror-linux-arm64-ubuntu2004-0.12.8.tgz  
  
Windows

|

mongomirror-win32-x86_64-0.12.8.zip  
  
## Prerequisites

### Source MongoDB Deployment

  * The source MongoDB deployment must be a replica set. If the source is a standalone MongoDB deployment, before running `mongomirror`, convert the standalone to a replica set.

  * The source replica set must run MongoDB version 2.6 or higher.

  * The source MongoDB replica set cannot be an `M0` free cluster or `M2/M5` shared cluster.

  * Don't change the `featureCompatibilityVersion` flag at any time during the procedure.

  * When you migrate from MongoDB 4.4 or earlier to an Atlas cluster that runs MongoDB 5.0 or later, drop any geoHaystack indexes from your collections.

  * `mongomirror` is not compatible with TTL indexes. Drop any existing TTL indexes and rebuild them when the migration process is complete. If you do not want to drop an existing index because it is important for query performance, contact support for alternative options.

  * Don't make any namespace changes during the migration process, such as using the `renameCollection` command or executing an aggregation pipeline that includes the `$out` aggregation stage.

  * You can't use the `renameCollection` command or the `$out` aggregation stage as part of initial sync, which runs as a part of the `mongomirror` process.

  * You must not restart the primary during the initial sync stage of the migration.

  * If your MongoDB deployment contains indexes with keys which exceed the Index Key Limit, before you start the live migration procedure, modify indexes so that they do not contain oversized keys. To learn more about about strategies for dealing with oversized keys, see `failIndexKeyTooLong` in the MongoDB Server documentation.

## Important

### Index Key Limit

`failIndexKeyTooLong` was deprecated in MongoDB version 4.2 and is removed in
MongoDB 4.4 and later. For MongoDB prior to 4.2, set this parameter to
`false`.

### Required Access on Source Replica Set

`mongomirror` must have network access to the source replica set. If the
source replica set requires authentication, you must include user credentials
when running `mongomirror`.

You must specify a database user with, at a minimum, the following privileges:

  * Read all databases and collections. The `readAnyDatabase` role on the `admin` database covers this requirement.

  * Read the oplog. See Oplog Access.

  * Run the `getParameter` command.

If no such user exists, create the user in your source MongoDB replica set.
Different MongoDB server versions have different built-in roles. Select a
built-in role based on your MongoDB server version and run the appropriate
commands in the `mongosh`:

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
  

### Target Atlas Deployment

The target Atlas deployment:

  * Can't be an `M0` free cluster, `M2`, or `M5` shared cluster.

  * Can't be a serverless instance.

  * Must be a replica set.

  * Must have the version that is the same as or later than the source cluster MongoDB version. See Upgrade Path.

  * Must not contain any namespaces that overlap with the source cluster. If `mongomirror` detects overlapping namespaces on the target cluster it fails before starting the process. If your target cluster contains overlapping namespaces, delete all data from the target cluster with `--drop`, or list the namespaces to import from the source cluster with `--includeNamespace`.

  * Must include in its IP access list either:

    * The public IP address of the server on which `mongomirror` is running, or

    * If set up for VPC peering, either the peer's VPC CIDR block (or a subset) or the Security Group of the peer VPC.

### Required Access on Target Cluster

`mongomirror` must have network access to the target cluster.

You must specify a database user with the `Atlas admin` role to run
`mongomirror`. To learn more, see Add Database Users.

## `mongomirror` Process

When you start `mongomirror`, it:

  1. Connects to Atlas over TLS/SSL.

  2. Performs an initial sync, copying collections from the existing MongoDB replica set to the target cluster in Atlas.

  3. After the initial sync, continuously tails the replica set's oplog for incoming changes and replays them on the target cluster in Atlas. `mongomirror` does not copy the `config` database. As of version 0.9.0, `mongomirror` uses wire compression if you enable it on either the source or the target cluster and use `--compressors` to specify which compression libraries to allow.

## Note

Starting in version 0.5.0, `mongomirror` builds all indexes on the target
cluster in the foreground, regardless of how the indexes were built on the
source cluster. Foreground index builds block all other operations on the
database. To learn more, see Index Build Operations on a Populated Collection.

Once started, `mongomirror` runs continuously until you shut it down:

  * If you shut down `mongomirror` during the initial sync stage, before you restart `mongomirror`, check that the target cluster is empty, or run `mongomirror` with `--drop`.

  * If you shut down `mongomirror` during the oplog tailing stage, the process stops tailing the oplog. You can restart `mongomirror` to continue tailing from the last processed oplog record using `--bookmarkFile`.

## Run `mongomirror`

1

### Set up database user in the source replica set.

If the source replica set requires authentication, you must include user
credentials when running `mongomirror`. For requirements, see Required Access
on Source Replica Set.

Make note of the username and password for this user, as you must specify
these credentials when running `mongomirror`.

2

### Set up a database user in the target Atlas cluster.

You must specify a database user with the `Atlas admin` role to run
`mongomirror`. See Add Database Users for documentation on creating a database
user.

If no such user exists, create the user:

  1. In the Security section of the left navigation, click Database Access. The Database Users tab displays.

  2. Click __ Add New Database User.

  3. Add an Atlas admin user.

Make note of the username and password selected for the new user, as you must
specify these credentials when running `mongomirror`.

3

### Update IP Access List.

If the host where you will run `mongomirror` is not in your cluster's IP
Access List, update the list. You can specify either:

  * The public IP address of the server on which `mongomirror` will run, or

  * If set up for VPC peering, either the peer's VPC CIDR block (or a subnet) or the Security Group of the peer VPC.

4

### Open the connect dialog.

  1. Click Database in the top-left corner of Atlas.

  2. From the Database Deployments view, click Connect for the Atlas cluster into which you want to migrate data.

5

### Copy the target cluster host information.

You can get your Atlas cluster's hostname information from the Atlas user
interface.

## Note

You don't need to use a driver to migrate data with `mongomirror`.

  1. From the Connect dialog, click Connect with the MongoDB Shell.

  2. From the drop-down list, select 3.4 or earlier. The connection string should look similar to the following example. This example has been broken into multiple lines for readability:
    
        mongodb://<username>:<PASSWORD>@  
      
    00.foo.mongodb.net:27017,  
    01.foo.mongodb.net:27017,  
    02.foo.mongodb.net:27017/test?  
    ssl=true&replicaSet=myAtlasRS&authSource=admin  
  
  3. In a text editor, paste the value of `replicaSet`, add a forward slash (`/`), and then append the host list as comma-separated values, as shown in the following example:
    
        myAtlasRS/00.foo.mongodb.net:27017,01.foo.mongodb.net:27017,02.foo.mongodb.net:27017  
      
  

Use this value for `--destination` in the next step.

6

### Start `mongomirror`.

Start `mongomirror` with the following options:

  * `--host` set to the host string of the source cluster.

  * `--ssl` if the source cluster has TLS/SSL enabled.

  * `--username` to the source cluster username created for this procedure.

  * `--password` to the password for the source cluster username.

  * `--authenticationDatabase` to the database in the source cluster where the username specified to `--username` was created.

  * `--destination` to the Atlas cluster host string.

  * `--destinationUsername` to the target Atlas cluster username.

  * `--destinationPassword` to the password for the target Atlas cluster username.

Your final command should resemble the following example:

    
    
    mongomirror --host "MySourceRS/host1.example.net:27017,host2.example.net:27017,host3.example.net:27017" \  
      
       --ssl \  
       --username "mySourceUser" \  
       --password "mySourceP@$$word" \  
       --authenticationDatabase "admin" \  
       --destination "myAtlasRS/00.foo.mongodb.net:27017,01.foo.mongodb.net:27017,02.foo.mongodb.net:27017" \  
       --destinationUsername "myAtlasAdminUser" \  
       --destinationPassword "atlasPassword"  
  
See Options for more `mongomirror` options.

To complete the migration process, switch to Atlas.

## Switch to Atlas

After `mongomirror` completes the initial sync and tails the replica set's
oplog, you can switch over to the target Atlas cluster.

1

### Stop your application.

This ensures that no additional writes occur on the source cluster.

2

### Wait for `mongomirror` to report 0s of lag between the source and
destination clusters.

This signifies that the source and destination clusters are in a consistent
state.

3

### Stop `mongomirror`.

Once the Atlas cluster is up to date, stop `mongomirror`.

4

### Update client applications to use the Atlas cluster.

Update your client application(s) with the Atlas connection string provided
via the Connect button on the cluster panel.

For details on connections to Atlas, see Connect via Your Application.

## Monitoring

`mongomirror` logs its progress to the standard output in the terminal. During
the initial sync, `mongomirror` logs a progress bar for each collection it
copies. For example:

    
    
    2021-08-09T16:35:50.227-0000  [#....................]  park.events  2179/34184    (6.4%)  
      
    2021-08-09T16:35:50.227-0000  [#############........]  zoo.animals  29000/49778  (58.3%)  
  
When tailing the oplog, `mongomirror` logs the lag time, in seconds, between
the most recent oplog entry on the source cluster and the last processed oplog
entry on the target cluster. For example:

    
    
    2016-12-12T16:22:17.027-0800 Current lag from source: 6s  
      
  
A lag time of 6 seconds means that the last oplog entry `mongomirror`
processed occurred 6 seconds before the most recent one available on the
source cluster.

## Note

The amount of time it takes `mongomirror` to catch up may be greater or less
than 6 seconds, depending on the number of entries that arrive per second.

A lag time of 0 seconds indicates that `mongomirror` is processing entries
that arrived less than one second before the latest oplog entry.

If the source cluster has indexes, `mongomirror` builds the same indexes on
the target cluster. The progress log shows the start and end times of the
index building process. To view the progress of the index builds, you can
either:

  * Use the currentOp command on the primary node of the target cluster. The `command` field shows information about the running operation. Index building entries look similar to the following:
    
            "command" : {  
      
               "createIndexes" : "perfs",  
               "indexes" : [  
                       {  
                               "key" : {  
                                       "animal" : "text"  
                               },  
                               "name" : "animal_text"  
                       }  
               ]...  
  
  * Download the mongodb logs for your target cluster and search for recent entries for index-related lines. Log messages related to index building look similar to the following:
    
        {"t":{"$date":"2021-08-09T16:35:50.227+00:00"},"s":"I",  "c":"INDEX",    "id":20447,   "ctx":"conn1080","msg":"Index build: completed","attr":{"buildUUID":{"uuid":{"$uuid":"c4a62739-bf19-456d-bbd6-7baa29f1063b"}}}}  
      
  

## Performance

To avoid contention for network and CPU resources, run `mongomirror` on hosts
other than your replica set's `mongod` instance hosts.

  * `mongomirror` affects your source replica set's performance similar to having a secondary:

    * For the initial sync stage, the load scales with the size of your data set.

    * Once an initial sync completes, the load scales with oplog gigabytes used per hour.

## Command Syntax, Options, and Examples

For `mongomirror` syntax, options, and examples, see the mongomirror reference
page.

## Troubleshooting

For `mongomirror` troubleshooting, see Common Post-Validation Errors for Live
Migration (Pull).

← Migrate Data with Self-Managed Toolsmongomirror →

