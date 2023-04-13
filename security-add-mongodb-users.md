Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Database Users

Share Feedback

On this page

  * Database User Authentication
  * Add Database Users
  * View Database Users and Certificates
  * Modify Database Users
  * Delete Database Users
  * Built-in Roles
  * Specific Privileges

Create database users to provide clients access to the database deployments in
your project. A database user's access is determined by the roles assigned to
the user. When you create a database user, any of the built-in roles add the
user to all database deployments in your Atlas project. You can remove the
default built-in role and set specific privileges and custom roles to add the
user to specific database deployments.

Database users are separate from Atlas users. Database users have access to
MongoDB databases, while Atlas users have access to the Atlas application
itself. Atlas supports creating temporary database users that automatically
expire within a user-configurable 7-day period.

Atlas audits the creation, deletion, and updates of database users in the
project's Activity Feed. Atlas audits actions pertaining to both temporary and
non-temporary database users. To view the project's Activity Feed, click
Activity Feed in the Project section of the left navigation. For more
information on the project Activity Feed, see View All Activity.

The available Atlas built-in roles and specific privileges support a subset of
MongoDB commands. See Unsupported Commands in `M10+` Clusters for more
information.

Atlas supports a maximum of 100 database users per Atlas project. If you
require more than 100 database users on a project, contact Atlas support.

## Important

Atlas rolls back any user modifications not made through the UI or Atlas
Administration API. You must use the Atlas UI or Atlas Administration API to
add, modify, or delete database users on Atlas database deployments.

## Database User Authentication

Atlas offers the following forms of authentication for database users:

Password Authentication

X.509 Certificates

AWS IAM Authentication

LDAP Authentication

SCRAM is MongoDB's default authentication method. SCRAM requires a password
for each user.

The authentication database for SCRAM-authenticated users is the `admin`
database.

## Note

By default, Atlas supports SCRAM-SHA-256 authentication. If you have any
database users created before the release of MongoDB 4.0, update their
passwords to generate SCRAM-SHA-256 credentials. You may reuse existing
passwords.

## Add Database Users

A project can have users with different authentication methods.

You cannot change a user's authentication method after creating that user. To
use an alternative authentication method, you must create a new user.

Atlas CLI

Atlas Administration API

Atlas UI

The Atlas CLI uses the following commands to create new database users and
X.509 certificates. The options you specify determine the authentication
method.

To create a database user for your project using the Atlas CLI, run the
following command:

    
    
    atlas dbusers create [builtInRole]... [options]  
      
  
To create a new Atlas-managed X.509 certificate for the specified database
user using the Atlas CLI, run the following command:

    
    
    atlas dbusers certs create [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas dbusers create and atlas dbusers certs
create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View Database Users and Certificates

Atlas CLI

Atlas Administration API

Atlas UI

### View Database Users

To list all Atlas database users for your project using the Atlas CLI, run the
following command:

    
    
    atlas dbusers list [options]  
      
  
To return the details for a single Atlas database user in the project you
specify using the Atlas CLI, run the following command:

    
    
    atlas dbusers describe <username> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas dbusers list and atlas dbusers describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### View X.509 Certificates for a Database User

To list all Atlas-managed, unexpired certificates for a database user using
the Atlas CLI, run the following command:

    
    
    atlas dbusers certs list <username> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas dbusers certs list.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Modify Database Users

Atlas CLI

Atlas Administration API

Atlas UI

To update a database user from your project using the Atlas CLI, run the
following command:

    
    
    atlas dbusers update <username> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas dbusers update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Delete Database Users

Atlas CLI

Atlas Administration API

Atlas UI

To delete a database user from your project using the Atlas CLI, run the
following command:

    
    
    atlas dbusers delete <username> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas dbusers delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Built-in Roles

The following table describes the Atlas built-in roles and the MongoDB Roles
or privilege actions they represent.

## Note

### Protected MongoDB Database Namespaces

The following databases are read-only for _all_ users, including those with
the `atlasAdmin` or `clusterMonitor` role.

  * `local`

  * `config`

We discourage writing to the `admin` database. Atlas manages multiple
collections in the `admin` database, and these collections are read-only for
all users.

`atlasAdmin` has the `update` privilege on the `config.settings` collection to
manage the balancer.

Atlas Built-in Role

|

MongoDB Role

|

Inherited Roles or Privilege Actions  
  
||  
  
`Atlas admin`

    

|

`atlasAdmin`

    

|

  * `readWriteAnyDatabase`

  * `readAnyDatabase`

  * `dbAdminAnyDatabase`

  * `clusterMonitor`

  * `cleanupOrphaned`

  * `enableSharding`

  * `flushRouterConfig`

  * `moveChunk`

  * `viewUser`

  
  
`Read and write to any database`

    

|

`readWriteAnyDatabase`

    

|

  * `readWriteAnyDatabase`

  
  
`Only read any database`

    

|

`readAnyDatabase`

    

|

  * `readAnyDatabase`

  
  
To learn more about common commands that Atlas doesn't support with the
current Atlas user privileges, see Unsupported Commands in `M10+` Clusters

## Specific Privileges

The following table describes the Atlas specific privileges, the database it
applies to, and the privilege actions they represent.

Atlas Specific Privilege

|

Database

|

Privilege Actions  
  
||  
  
`backup`

|

`admin`

|

  * `listDatabases`

  * `listCollections`

  * `listIndexes`

  * `appendOplogNote`

  * `getParameter`

  * `serverStatus`

  
  
`clusterMonitor`

|

`admin`

|

  * `checkFreeMonitoringStatus`

  * `connPoolStats`

  * `getCmdLineOpts`

  * `getDefaultRWConcern`

  * `getLog`

  * `getParameter`

  * `getShardMap`

  * `hostInfo`

  * `inprog`

  * `listDatabases`

  * `listSessions`

  * `listShards`

  * `netstat`

  * `replSetGetConfig`

  * `replSetGetStatus`

  * `serverStatus`

  * `setFreeMonitoring`

  * `shardingState`

  * `top`

  
  
`dbAdmin`

|

User configured

|

  * `bypassDocumentValidation`

  * `changeStream`

  * `collMod`

  * `collStats`

  * `compact`

  * `convertToCapped`

  * `createCollection`

  * `createIndex`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `dropDatabase`

  * `dropIndex`

  * `enableProfiler`

  * `find`

  * `killCursors`

  * `listCollections`

  * `listIndexes`

  * `planCacheIndexFilter`

  * `planCacheRead`

  * `planCacheWrite`

  * `reIndex`

  * `renameCollectionSameDB`

  * `storageDetails`

  * `validate`

  
  
`dbAdminAnyDatabase`

|

User configured except `local` and `config`

|

  * `dbAdminAnyDatabase`

  
  
`enableSharding`

|

|

  * `enableSharding`

  
  
`read`

|

User configured

|

  * `changeStream`

  * `collStats`

  * `dbHash`

  * `dbStats`

  * `find`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  
  
`readWrite`

|

User configured

|

  * `changeStream`

  * `collStats`

  * `convertToCapped`

  * `createCollection`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `createIndex`

  * `dropIndex`

  * `find`

  * `insert`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `remove`

  * `renameCollectionSameDB`

  * `update`

  
  
`killOpSession`

|

User configured

|

  * `inprog`

  * `killop`

  * `killAnySession`

  * `listSessions`

  
  
`readWriteAnyDatabase`

|

User configured except `local` and `config`

|

  * `readWriteAnyDatabase`

  * `changeStream`

  * `collStats`

  * `convertToCapped`

  * `createCollection`

  * `dbHash`

  * `dbStats`

  * `dropCollection`

  * `createIndex`

  * `dropIndex`

  * `find`

  * `insert`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `listDatabases`

  * `remove`

  * `renameCollectionSameDB`

  * `update`

  
  
`readAnyDatabase`

|

User configured except `local` and `config`

|

  * `readAnyDatabase`

  * `changeStream`

  * `collStats`

  * `dbHash`

  * `dbStats`

  * `find`

  * `killCursors`

  * `listIndexes`

  * `listCollections`

  * `listDatabases`

  
  
← Configure Database Deployment Authentication and AuthorizationConfigure
Custom Database Roles →

