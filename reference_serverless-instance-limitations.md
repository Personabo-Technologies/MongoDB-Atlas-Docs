Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Serverless Instance Limitations

Share Feedback

On this page

  * Unsupported Configurations
  * Unsupported Actions
  * Operational Limitations and Considerations
  * Minimum Driver Versions for Serverless Instances
  * Minimum `mongosh` Version for serverless instances
  * Minimum MongoDB Compass Version for serverless instances
  * Minimum MongoDB Tools Version for serverless instances

Serverless instances don't currently support the Atlas features listed below.
If you require these capabilities, please use a dedicated cluster.

Serverless instances don't support some features even though they are a part
of the Stable API v1. We note unsupported features that are a part of the
Stable API v1 inline.

MongoDB plans to add support for more configurations and actions on serverless
instances over time. Footnotes indicate that MongoDB plans to support the
feature for serverless instances in the future.

## Unsupported Configurations

Currently, serverless instances don't support the following configurations:

  * Multi-Region Deployments

  * Multi-Cloud Deployments

  * Sharded Deployments

  * Global Clusters

  * Private Endpoints on Google Cloud using Private Service Connect [1]

  * Network Peering (VPC/VNet)

  * Advanced Enterprise Security Features (including LDAP and Database Auditing)

Serverless instances do support X.509 certificates and IAM for authentication.

[1]|  Coming soon.  
|  
  
## Unsupported Actions

Currently, serverless instances don't support the following actions:

  * Convert Atlas serverless instances into clusters. [2]

  * Convert Atlas dedicated clusters into Atlas serverless instances

You can convert a shared cluster to a serverless instance.

  * Live migrate into Atlas serverless instances.

  * Store more than 1 TB of data.

This value includes the number of bytes of all uncompressed BSON documents
stored in all collections, plus the bytes stored in their associated indexes.

  * Configure alerts on service metrics billing metrics. [2]

Atlas supports configuring alerts for your project or organization if your
bill exceeds a certain threshold.

  * Perform automated restores from backup snapshots.

  * Use Atlas Search.

  * Use Online Archive.

  * Use Atlas Device Sync.

  * Use Atlas Triggers.

  * Use predefined replica set tags.

  * Test primary failover.

  * Simulate a regional outage.

  * Encryption at Rest using key management.

  * Track database access.

  * Use server-side JavaScript, such as `$where`, `$function`, `$accumulator` and `map-reduce`.

## Note

Serverless instances don't support these features even though they're a part
of the Stable API v1.

  * Download database logs.

  * Use wire compression between clients and Atlas serverless instances.

  * Use BI Connector.

[2]|  _(1, 2)_ Coming soon.  
|  
  
## Operational Limitations and Considerations

Additionally, serverless instances have the following operational limitations
and considerations:

Operation

|

Limitation  
  
|  
  
Aggregation and Queries

|

Serverless instances don't support the `allowDiskUse` option for the
aggregation command, its helper method, or the cursor.allowDiskUse() query
cursor method.

Serverless instances don't support the $out stage. Use $merge instead.

Aggregation fields on serverless instances that represent database and
collection names (such as $merge values) can't be expressions.

## Note

Serverless instances don't support these features even though they're a part
of the Stable API v1.

Aggregation pipelines for serverless instances don't support the `$currentOp`,
`$listLocalSessions`, `$listSessions`, and `$planCacheStats` stages.

Aggregation pipelines for serverless instances can have a maximum of 50
stages.  
  
Sort

|

The $sort stage has a limit of 32 megabytes of RAM.  
  
Authentication

|

Serverless instances support the following authentication methods only:

  * Password (SCRAM-SHA-256)

  * X.509 Certificates

  * AWS IAM

  
  
Build Index with Rolling Build

|

Serverless instances don't support building indexes with a rolling build.  
  
Real-Time Performance Panel

|

Serverless instances don't provide access to the Real-Time Performance Panel.  
  
Throughput

|

Serverless instances don't routinely cap operation throughput. Atlas may
throttle operations for your serverless instance temporarily while the system
scales.  
  
Connections

|

Serverless instances can support up to 500 simultaneous connections.  
  
Database Commands

|

Some database commands have limitations for serverless instances. To learn
more, see Unsupported Commands in Serverless Instances.

You cannot create a capped collection or convert an existing collection to a
capped collection.  
  
Namespaces and Database Names

|

Atlas limits serverless instance namespaces to 95 characters and database
names to 38 characters.  
  
Database and Collections

|

Serverless instances have a maximum of 50 databases and 500 collections total.  
  
Custom Roles

|

Changes to custom roles may take up to 30 seconds to deploy in serverless
instances.  
  
Access to Collections in `local`, `admin`, and `config` Databases

|

Serverless instances don't allow:

  * Read access to the oplog or any other collection in the `local` database.

  * Write access to any collection in the `local` and `config` databases.

  * Read or write access to any collection in the `admin` database.

Atlas issues an error similar to the following if you attempt to read or write
to collections in these databases:

    
    
    | command <cmd name> is not allowed in this Atlas tier  
      
    (Unauthorized) not authorized on <db name> to execute command  
    <cmd name>  
  
Change Streams

|

Serverless instances don't support change streams.

Serverless instances don't support this feature even though it's a part of the
Stable API v1.  
  
Collation

|

Serverless instances don't support collation on collections, indexes, or
queries.

## Note

Serverless instances don't support these features even though they're a part
of the Stable API v1.  
  
BSON Nested Object Depth

|

Serverless instances can't store documents with more than 50 nested levels.  
  
Transaction Size

|

Serverless instances support multi-document transactions that are up to 700 MB
in size. Atlas aborts any serverless instance transactions that exceed 700 MB.  
  
Write Concern

|

Serverless instances don't support a numeric write concern level greater than
`1`, or custom write concerns. Operations that use a write concern level
greater than `1`, or custom write concerns, might return an
`UnsatisfiableWriteConcern` error. This behavior also applies to operations
sent over a connection created with a write concern option.

## Note

For clusters other than `M0`, `M2`, or `M5` clusters, you can verify whether
you're using a write concern mode that serverless instances don't support with
the serverStatus command's opWriteConcernCounters field.  
  
## Minimum Driver Versions for Serverless Instances

To connect to your serverless instance using a driver, you must use at least
one of the following versions:

Driver

|

Version  
  
|  
  
C

|

1.19.0  
  
C++

|

3.7.0beta1  
  
C#

|

2.13.0  
  
Go

|

1.6.0  
  
Java

|

4.3.0  
  
Motor

|

2.5.0  
  
Node.js

|

4.1.0  
  
PHP

|

1.11.0 (Extension)

1.10.0 (Library)  
  
PyMongo

|

3.12.0  
  
Ruby

|

2.16.0  
  
Rust

|

2.1.0  
  
Scala

|

4.3.0  
  
Swift

|

1.2.0  
  
## Minimum `mongosh` Version for serverless instances

To connect to serverless instances using `mongosh`, you must use version 1.0.0
or later.

## Important

You can't connect to serverless instances using the legacy `mongo` shell.

## Minimum MongoDB Compass Version for serverless instances

To connect to serverless instances using MongoDB Compass, you must use version
1.28 or later.

## Minimum MongoDB Tools Version for serverless instances

To import data using the MongoDB Tools, including `mongodump`, `mongorestore`,
`mongoexport`, and `mongoimport`, you must have MongoDB Tools version 100.5.x
or later.

← Atlas LimitationsAtlas M0 (Free Cluster), M2, and M5 Limitations →

