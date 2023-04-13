Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas M0 (Free Cluster), M2, and M5 Limitations

Share Feedback

On this page

  * Configuration Limitations
  * Operational Limitations
  * Driver Minimum Requirements

## Configuration Limitations

The following table lists the configuration limitations of Atlas `M0` free
clusters and `M2/M5` shared clusters:

Configuration Option

|

Limitation  
  
|  
  
Cloud Service Provider and Region

|

You can deploy `M0` free clusters and `M2/M5` shared clusters only in a subset
of regions on AWS, Google Cloud, and Azure. To learn more about supported
cloud provider regions for free clusters and shared clusters, see:

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

  * Microsoft Azure

  
  
MongoDB Version and Storage Engine

|

Atlas uses MongoDB 5.0 for `M0/M2/M5` clusters.  
  
MongoDB Version Upgrade

|

You can't upgrade the MongoDB version that `M0/M2/M5` clusters run. Atlas
upgrades `M0` free clusters or `M2/M5` shared clusters to the newest MongoDB
version after several patch versions become available for that version. To
learn more, see MongoDB Versioning.  
  
Cluster Tier

|

You must select the `M0` cluster tier to deploy a free cluster.  
  
Cluster Memory

|

You can't configure memory for `M0` free clusters or `M2/M5` shared clusters.  
  
Cluster Storage

|

You can't configure storage size for `M0` free clusters or `M2/M5` shared
clusters.  
  
Replication Factor

|

Replication Factor is set to `3 Nodes` and you can't modify it for `M0` free
clusters or `M2/M5` shared clusters.  
  
Replica Set Tags

|

`M0` free clusters and `M2/M5` shared clusters don't have pre-defined replica
set tags.  
  
Do You Want A Sharded Cluster

|

You can't deploy a `M0` free cluster or `M2/M5` shared cluster as a Sharded
Cluster.  
  
Do You Want To Enable Backup

|

You can't enable backups on `M0` free clusters.

## Tip

### See also:

Backup Alternative: `mongodump`

You may use mongodump to back up your data and mongorestore to restore that
data. To learn how to manually back up your data, see Command Line Tools.  
  
Test Primary Failovers

|

You can't perform primary failover testing on `M0` free clusters or `M2/M5`
shared clusters.  
  
Simulate Regional Outage

|

You can't perform regional outage testing on `M0` free clusters or `M2/M5`
shared clusters.  
  
Database Auditing

|

You can't configure database auditing on `M0` free clusters or `M2/M5` shared
clusters.  
  
Encryption at Rest using your Key Management

|

You can't configure encryption at Rest using Customer Key Management on `M0`
free clusters or `M2/M5` shared clusters.  
  
Network Peering Connections

|

You can't configure network peering connections on `M0` free clusters or
`M2/M5` shared clusters.  
  
Access Tracking

|

You can't view the database access history for `M0` free clusters or `M2/M5`
shared clusters.  
  
## Operational Limitations

The following table lists the operational limitations of Atlas `M0` free
clusters and `M2/M5` shared clusters:

Operation

|

Limitation  
  
|  
  
Aggregation and Queries

|

Atlas `M0` free clusters and `M2/M5` shared clusters don't support the
`allowDiskUse` option for the aggregation command, its helper method, or the
cursor.allowDiskUse() query cursor method.

On `M0` free clusters and `M2/M5` shared clusters, aggregation pipelines don't
support the `$currentOp`, `$listLocalSessions`, `$listSessions`, and
`$planCacheStats` stages.

On `M0` free clusters and `M2/M5` shared clusters, aggregation pipelines can
have a maximum of 50 stages.  
  
API Access

|

While you can create an `M0` free cluster using the Clusters API resource, you
cannot modify an `M0` free cluster using the Clusters API resource. A subset
of API endpoints support `M2` and `M5` shared clusters.

## Note

You can create an `M0` free cluster using the Clusters API resource. You can
create only one `M0` free cluster per project.  
  
Atlas Alerts

|

`M0` free clusters and `M2/M5` shared clusters can only trigger alerts
configured with one of the following alert conditions:

  * Connections

  * Logical Size

  * Network

  * Opscounter

  
  
Atlas Monitoring

|

The Metrics view of an `M0` free cluster or `M2/M5` shared cluster displays
only the following metrics:

  * Connections

  * Logical Size

  * Network

  * Opscounter

To learn more, see Real Time Metrics.  
  
Authentication

|

`M0` free clusters and `M2/M5` shared clusters support the following
authentication methods only:

  * Password (SCRAM-SHA1)

  * X.509 Certificates

  * AWS IAM

  
  
Auto-Expand Storage

|

`M0` free clusters and `M2/M5` shared clusters don't provide automatically
scaling storage.  
  
BSON Nested Object Depth

|

`M0` free clusters and `M2/M5` shared clusters can store documents with a
maximum of 50 nested levels.  
  
Build Index with Rolling Build

|

`M0` free clusters and `M2/M5` shared clusters don't support building indexes
with a rolling build.  
  
Change Streams Filtering

|

For `M0` free clusters and `M2/M5` shared clusters, you can use only strings
and regular expressions in filters on database names (namespace `ns` fields)
in change streams. You can't use commands, such as `$in`, in database
namespace filters. This limitation doesn't apply to filtering on collection
names in change streams.  
  
Cluster Persistence

|

Atlas may deactivate idle `M0` free clusters as per the Terms of Service.  
  
Command Line Tools

|

`M0` free clusters and `M2/M5` shared clusters don't support the following
command line tool options:

|

Command Line Tool

|

Unsupported Options  
  
|  
  
`mongorestore`

|

  * \--restoreDbUsersAndRoles

  * \--oplogReplay

  * \--preserveUUID

  
  
`mongodump`

|

  * \--dumpDbUsersAndRoles

  * \--oplog

  
  
For `M0` free clusters and `M2/M5` shared clusters, you can't run
`mongorestore` or `mongodump` on the `admin` database. If you use the `--db`
option to set the destination database to `admin`, the program returns an
error.  
  
Connections

|

`M0` free clusters and `M2/M5` shared clusters can only have a maximum of 500
connections.  
  
Cursors

|

Free clusters and shared clusters can't use the noTimeout cursor option.  
  
Custom Roles

|

Changes to custom roles might take up to 30 seconds to deploy in `M0` free
clusters and `M2/M5` shared clusters.  
  
Database and Collections

|

`M0` free clusters and `M2/M5` shared clusters can have a maximum of 100
databases and 500 collections total.  
  
Database Commands

|

Certain database commands are unsupported or behave differently in an `M0`
free cluster. To learn more, see Command Limitations in Free Clusters. For
questions or comments related to restricted commands, contact support.  
  
Access to Collections in `local`, `admin`, and `config` Databases

|

`M0` free clusters and `M2/M5` shared clusters don't allow:

  * Read access to any collection in the `local` database with the exception of read access to the oplog.

  * Write access to any collection in the `local` and `config` databases.

  * Read or write access to any collection in the `admin` database.

Atlas issues an error similar to the following if you attempt to read or write
to collections in these databases:

    
    
    | command <cmd name> is not allowed in this Atlas tier  
      
    (Unauthorized) not authorized on <db name> to execute command <cmd name>  
  
Database Logs

|

`M0` free clusters and `M2/M5` shared clusters don't allow you to download
logs.  
  
Data Recovery

|

  * Custom policies are not supported for `M2` and `M5` cluster snapshots. Atlas always takes a single daily snapshot at the same time, starting 24 hours after the cluster was created.

If you require finer-grained backups, consider upgrading to an `M10` or larger
cluster tier.

  * On-demand snapshots are not supported for `M2` and `M5` clusters.

  * You can't restore `M2` and `M5` snapshots to a sharded cluster. You can only restore `M2` and `M5` snapshots to replica sets.

  * You can't restore serverless instance snapshots to `M2` and `M5` clusters.

  * Starting with MongoDB 5.0, you can restore snapshots of clusters that run only the two most recent major versions of MongoDB to `M2` and `M5` clusters.

## Example

    * You can restore snapshots taken from clusters that run MongoDB 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

    * You can't restore snapshots taken from clusters that run MongoDB version earlier than 4.4 to an `M2` or `M5` cluster that runs MongoDB 5.0.

  
  
Data Transfer Limits

|

`M0` free clusters and `M2/M5` shared clusters limit the total data
transferred into or out of the cluster in a rolling seven-day period. The rate
limits vary by cluster tier as follows:

  * `M0`: 10 GB in and 10 GB out per period

  * `M2`: 20 GB in and 20 GB out per period

  * `M5`: 50 GB in and 50 GB out per period

Atlas handles clusters that exceed the rate limit as follows:

  * Atlas throttles the network speed of the cluster.

  * Atlas triggers a one second cooldown period before resuming the cluster's operations on a given connection. If the queue is greater than the operations per second limit, operations might wait for more than a second in the queue.

  * If the amount of transferred data drops below the rate limit threshold, Atlas resumes processing of the queued data transfers on each connection before processing any new data transfers on that connection.

  
  
JavaScript

|

`M0` free clusters and `M2/M5` shared clusters don't support server-side
JavaScript. For example, $where and map-reduce are unsupported.  
  
Namespaces and Database Names

|

`M0` free cluster and `M2/M5` shared cluster namespaces are limited to 95
bytes. Database names are limited to 38 bytes.  
  
Number of Free Clusters

|

You can deploy at most _one_ `M0` free cluster per Atlas project.  
  
Performance Advisor

|

`M0` free clusters and `M2/M5` shared clusters don't provide access to the
Performance Advisor.  
  
Query Utilization

|

The percentage of time that a query is running over any five minute period
must remain under 100% on `M0` free clusters and `M2/M5` shared clusters.  
  
Real-Time Performance Panel

|

`M0` free clusters and `M2/M5` shared clusters don't provide access to the
Real-Time Performance Panel.  
  
Sort in Memory

|

`M0` free clusters and `M2/M5` shared clusters sort in memory limit is 32 MB.  
  
Throughput

|

`M0` free clusters and `M2/M5` shared clusters limit the number of read and
write operations per second. The rate limits vary by cluster tier as follows:

  * `M0`: 100 operations per second

  * `M2`: 200 operations per second

  * `M5`: 500 operations per second

Atlas handles clusters that exceed the operations per second rate limit as
follows:

  * Atlas throttles the network speed of the cluster.

  * Atlas triggers a one second cooldown period before resuming the cluster's operations on a given connection. If the queue is greater than the operations per second limit, operations might wait for more than a second in the queue.

  * If the number of operations per second drops below the rate limit threshold, Atlas resumes processing of the queued operations on each connection before processing any new operations on that connection.

  
  
Automatic Pause of Idle Clusters

|

Atlas automatically pauses `M0` free clusters after 60 days of inactivity
where there are zero connections to the cluster. You can resume the cluster at
any time.  
  
## Driver Minimum Requirements

Driver

|

Description  
  
|  
  
Drivers that use a JRE or JDK'

|

Due to an issue with TLS 1.3 support in the Java JDK' (JDK-8236039), upgrade
the JDK' that supports the driver you use to connect to Atlas.

Minimum versions of the JDK' include:

|

|  
  
|  
  
14u-cpu

|

JDK-8249107  
  
14.0.2

|

JDK-8247954  
  
13.0.3

|

JDK-8241515  
  
11.0.8-oracle

|

JDK-8238504  
  
11.0.7

|

JDK-8237387  
  
8u261

|

JDK-8243759  
  
emb-8u261

|

JDK-8247097  
  
To learn more about support for TLS 1.3 in Java-based languages, libraries,
and drivers, see:

  * MongoDB Java, Reactive Streams, and Scala Drivers

  * Scala

  * Kafka

  
  
← Serverless Instance LimitationsUnsupported Commands in Atlas →

