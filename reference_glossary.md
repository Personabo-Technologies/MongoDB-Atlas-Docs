Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Glossary

Share Feedback

alert

    

Notification sent by Atlas when your database operations or server usage reach
thresholds that affect cluster performance. To learn what conditions you can
set to trigger alerts, see Review Alert Conditions.

## Tip

### See also:

Resolve Alerts

analytics node

    Specialized read-only node that can isolate queries which you do not want to affect your operational workload. Analytics nodes are useful for handling analytic data such as reporting queries executed by BI tools. You can host analytics nodes in dedicated geographic regions to optimize read performance and reduce latency.
API

    

Communication protocol facilitating interaction between the client and MongoDB
Atlas. You can use the Atlas Administration API to automate many of the tasks
performed in the Atlas UI.

## Tip

### See also:

  * APIs

  * Atlas Administration API Resources

App Services

    

Serverless platform that enables developers to quickly build applications
without having to set up server infrastructure. Atlas App Services
automatically integrates the connection to your Atlas cluster databases,
allowing for seamless interaction between your application and data.

## Tip

### See also:

Atlas App Services Documentation

Atlas Search

    

Fine-grained text indexing enabling advanced text search on your data without
any additional required management. Atlas Search provides options for several
kinds of text analyzers, score-based results ranking, and a rich query
language.

## Tip

### See also:

What is MongoDB Atlas Search?

Atlas user

    

Account used to access the Atlas application. You can grant Atlas users access
to Atlas organizations, projects, or both, with certain permissions defined by
user roles. Atlas users are different than database users. Atlas users do not
provide access to any MongoDB databases.

## Tip

### See also:

Configure Access to the Atlas UI

Atlas user role

    

Set of permissions granted to an Atlas user. You can grant permissions at the
organization or project level.

## Tip

### See also:

Atlas User Roles

auto-scaling

    

Configurable option to have your cluster automatically increase or decrease
its cluster tier, storage capacity, or both in response to cluster usage.

## Tip

### See also:

Configure Auto-Scaling

backup

    

Copy of your data that encapsulates the state of your cluster at a given time.
Backups provide a safety measure in the case of data loss events.

Atlas provides the following fully-managed methods for backups:

  * Cloud Backups

  * Legacy Backups

cloud backups

    

Localized cluster backup storage using the native snapshot functionality of
the cluster's cloud service provider.

Atlas supports Cloud Backups for clusters served on:

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

  * Microsoft Azure

## Tip

### See also:

Back Up Your Database Deployment

cluster

    Set of nodes comprising a MongoDB deployment. In Atlas, clusters can be replica sets or sharded deployments.
cluster class

    

 _Configurable for M40+ clusters hosted on AWS._

Storage class of your cluster. Your selected class affects cluster storage
performance and cluster costs. You can choose one of the following classes:

  * Low CPU

  * General

  * Local NVMe SSD

## Tip

### See also:

  * Customize Cluster Storage

  * NVMe storage

cluster tier

    

Dictates the memory, storage, and IOPS specification for each data-bearing
server in the cluster. Cluster storage size and overall performance increase
as the cluster tier increases.

## Tip

### See also:

  * Select Cluster Tier

  * Atlas Cluster Sizing and Tier Selection

custom role

    

Custom set of MongoDB privilege actions and MongoDB roles that you can save
and assign to database users. Create custom roles when Atlas's built-in roles
don't describe your desired set of privileges.

## Tip

### See also:

Configure Custom Database Roles

Data Explorer

    

Tool within Atlas to view and interact with cluster data. You can also use the
Data Explorer to manage indexes and run aggregation pipelines to process your
data.

## Tip

### See also:

Interact with Your Data

Data Federation

    

MongoDB's solution for querying data stored in low-cost S3 buckets, Atlas
clusters, HTTP endpoints, and Atlas Data Lake datasets using the MongoDB Query
Language. Analytics applications can use Atlas Data Federation to make use of
archived data for their data processing needs.

## Tip

### See also:

Atlas Data Federation

Data Lake

    

MongoDB's solution for storing extracted data in in an analytic-optimized
storage service. Atlas Data Lake provides analytic storage format optimized
for flat or nested data with low latency query performance.

## Tip

### See also:

Atlas Data Lake

Database user

    

Credentials used to authenticate a client to access a MongoDB database
deployment. You can assign privileges to a database user to determine that
user's access level to a database deployment. Database users are different
from Atlas users. Database users have access to MongoDB deployments, not the
Atlas application.

## Tip

### See also:

Configure Database Users

Database user privileges

    

Set of privilege actions or roles granted to a database user. You can assign
database user privileges at the database deployment, database, and collection
level.

## Tip

### See also:

Built-in Roles

dedicated cluster

    

Cluster category containing clusters of tier `M10` and greater.

Tier

|

Recommended environments  
  
|  
  
`M10` and `M20`

|

  * Development

  * Low-traffic production

  
  
`M30` and greater

|

Production  
  
deployment

    A group of MongoDB servers containing your data. Atlas-managed database deployments are either clusters (replica sets or sharded clusters) or serverless instances.
electable node

    Node which is eligible to become the primary member of your replica set. Atlas prioritizes nodes in the Highest Priority region for primary eligibility during elections. To ensure reliable elections, the total number of electable nodes across an entire region must be 3, 5, or 7.
encryption key

    

Random string of bits generated specifically to encrypt and decrypt data.

Atlas `Project Owners` can configure an additional layer of encryption on
their data in addition to the default encryption at rest that Atlas provides.
Project owners can use their Atlas-compatible customer key management provider
with the MongoDB encrypted storage engine.

Atlas supports the following customer key management providers when
configuring Encryption at Rest:

  * Amazon Web Services Key Management Service

  * Azure Key Vault

  * Google Cloud Platform Key Management Service

## Tip

### See also:

Encryption at Rest using Customer Key Management

Free Tier

    

Free-to-use cluster tier that provides a small-scale development environment
to host your data. free clusters never expire, and provide access to a subset
of Atlas features and functionality. free clusters might also be referred to
by their instance size, `M0`.

## Tip

### See also:

  * Get Started with Atlas

  * Atlas M0 (Free Cluster), M2, and M5 Limitations

Global Cluster

    

Clusters with defined geographic zones to support location-aware read and
write operations for globally distributed application instances and clients.
You can enable global sharding on clusters of tier `M30` and greater.

## Tip

### See also:

  * Manage Global Clusters

  * Create a Global Cluster

global write zone

    

Geographic zone representing a subset of your global cluster distribution.
Each Global Cluster supports up to 9 distinct global write zones. Each zone
consists of one Highest Priority region and one or more electable, read-only,
or analytics regions.

The available geographic regions depend on the selected cloud service
provider.

group

    See project.
group ID

    See project ID.
Highest Priority region

    

Region in a multi-region cluster which Atlas prioritizes for primary
eligibility during elections.

## Tip

### See also:

Configure High Availability and Workload Isolation

Impact

    

Estimated performance improvement of an index that Performance Advisor
suggests.

## Tip

### See also:

Review Index Ranking

interface endpoint

    

Elastic network interface with a private IP address from the IP address range
of your VPC subnet on AWS. An interface endpoint serves as an entry point for
traffic from clients in your VPC to an Atlas cluster when you create a AWS
PrivateLink connection between an AWS VPC and Atlas clusters in a specified
region.

## Tip

### See also:

Set Up a Private Endpoint

IP access list

    List of IP addresses and CIDR blocks with access to clusters within an Atlas project. Atlas only allows client connections to a cluster from entries in the corresponding project's IP access list. The access list can have up to 200 entries.
LDAP

    

Cross-platform protocol used to authenticate users and authorize them to
access data on a cluster. You can use Atlas to manage user authentication and
authorization from all MongoDB clients using your own LDAP server over TLS. A
single LDAPS configuration applies to all clusters in an Atlas project.

## Tip

### See also:

Set Up User Authentication and Authorization with LDAP

legacy backups

    

Incremental backups of your cluster taken by Atlas that ensure that your
backups are typically just a few seconds behind the operational system. You
can restore your cluster to a state from a selected point in time within the
last 24 hours.

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

## Tip

### See also:

Legacy Backups (Deprecated)

link-token

    

String that contains the information necessary to connect from Cloud Manager
or Ops Manager to Atlas during a live migration from a Cloud Manager or Ops
Manager deployment to a cluster in Atlas.

When you are ready to live migrate data from a Cloud Manager or Ops Manager
deployment, you generate a link-token in Atlas and then enter it in your Cloud
Manager or Ops Manager organization's settings. You use the same link-token to
migrate each deployment in your Cloud Manager or Ops Manager organization
sequentially, one at a time. You can generate multiple link-tokens in Atlas.
Use one unique link-token for each Cloud Manager or Ops Manager organization.

Live Migration

    

Process to seamlessly move an existing source replica set or sharded cluster
to Atlas. During the live migration process, Atlas keeps the target cluster in
sync with the remote source until you cut your applications over to the Atlas
cluster. Atlas offers two modes of live migration:

  * Push live migration, known in the Atlas user interface as Live Migration from Ops Manager or Cloud Manager, where Atlas **pushes** a deployment from Cloud Manager or Ops Manager to Atlas.

  * Pull live migration, known in the Atlas user interface as General Live Migration, where Atlas **pulls** a deployment from a cloud or on-premise deployment to Atlas.

## Tip

### See also:

Live Migrate (Pull) a Replica Set into Atlas

maintenance window

    

Day and time of the week when Atlas should start weekly maintenance on your
cluster. You can set your maintenance window in your Project Settings.

## Important

### Maintenance Window Considerations

Urgent Maintenance Activities

    Urgent maintenance activities such as security patches cannot wait for your chosen window. Atlas will start those maintenance activities when needed.
Ongoing Maintenance Operations

    Once maintenance is scheduled for your cluster, you cannot change your maintenance window until the current maintenance efforts have completed.
Maintenance Requires Replica Set Elections

    Atlas performs maintenance the same way as the maintenance procedure described in the MongoDB Manual. This procedure requires at least one replica set election during the maintenance window per replica set.
Maintenance Starts As Close to the Hour As Possible

    Maintenance always begins as close to the scheduled hour as possible, but in-progress cluster updates or unexpected system issues could delay the start time.

MongoDB Charts

    

Visualization tool for your Atlas data. You can launch MongoDB Charts from
your Atlas cluster and view your data with the Charts application to begin
visualizing your data.

## Tip

### See also:

MongoDB Charts

multi-region cluster

    

Atlas cluster spanning multiple geographic regions. Multi-region clusters can
increase availability and improve performance by routing application queries
to the most appropriate geographic regions.

Multi-region clusters must contain electable nodes.

Multi-region clusters may contain read-only nodes and analytics nodes.

network peering connection

    

Process by which two Internet networks connect and exchange traffic. You can
directly peer your VPC with the Atlas VPC created for your MongoDB clusters.
Using network peering, your application servers can directly connect to Atlas
while remaining isolated from public networks.

## Tip

### See also:

Set Up a Network Peering Connection

NVMe storage

    

 _Available for M40+ clusters hosted on AWS_

For applications hosted on AWS which require low-latency and high-throughput
IO, you can use the NVMe cluster class. The NVMe cluster class leverages a
unique data protocol to greatly improve data access speeds.

NVMe clusters use a hidden secondary node consisting of a provisioned volume
with high throughput and IOPS to facilitate backup.

## Tip

### See also:

Customize Cluster Storage

organization

    

Logical grouping of Atlas projects. You can leverage an organization to manage
billing, users, and security settings for the projects it contains.

  * Billing happens at the organization level while preserving visibility into usage in each project.

  * You can view all projects within an organization.

  * You can use teams to bulk assign organization users to projects within the organization.

## Tip

### See also:

Organizations

organization ID

    Unique 24-digit hexadecimal string used to identify your Atlas organization. The Return All Organizations endpoint returns the ID of all organizations that the authenticated user executing the API call can access.
Performance Advisor

    

Atlas tool that monitors slow queries executed on your cluster and suggests
indexes to improve query performance. Each index that the Performance Advisor
suggests include an Impact score indicating the potential performance
improvement that index would bring.

## Tip

### See also:

Monitor and Improve Slow Queries

primary

    In a replica set, the primary is the member that receives all write operations. In multi-region clusters, Atlas prioritizes nodes in the Highest Priority region for primary eligibility during elections.
project

    

Logical grouping of database deployments. You can have multiple database
deployments within a single project and multiple projects within a single
organization.

## Note

Project is synonymous with group.

project ID

    

Unique 24-digit hexadecimal string used to identify your Atlas project. The
Get All Projects API endpoint returns the ID of all projects that the
authenticated user executing the API call can access.

## Note

Project ID is synonymous with group ID.

Query Profiler

    

Atlas tool that diagnoses and monitors performance issues in your cluster. The
Query Profiler can expose long-running queries and their performance
statistics. You can filter the data returned by the Query Profiler to hone in
on specific namespaces and operation types.

## Tip

### See also:

Monitor Query Performance

read-only node

    Replica set in a dedicated geographic region that supplements your electable node regions. You can use read-only nodes to localize data where it is most frequently read to improve performance.
Real-Time Performance Panel

    

Atlas monitoring service that displays current network traffic, database
operations on your clusters, and hardware statistics about your host machines.
Use the RTPP to visually evaluate query execution times, monitor network
activity, and discover potential replication lag on secondary members of
replica sets.

## Tip

### See also:

Monitor Real-Time Performance

replica set

    

Group of MongoDB servers that maintain the same data set. Replica sets provide
redundancy, high availability, and are the basis for all production
deployments.

## Tip

### See also:

Replication

rolling restart

    Process that restarts all nodes in the cluster in sequence. To maintain cluster availability, Atlas restarts one node at a time starting with a secondary node. Atlas always maintains a primary node until the rolling restart completes.
sharded cluster

    

Set of nodes comprising a sharded MongoDB deployment. A sharded cluster
consists of config servers, shards, and one or more `mongos` routing
processes.

## Tip

### See also:

Sharded Cluster Components

shared cluster

    

Cluster category containing `M0` (Free Tier), `M2`, and `M5` tier clusters.
Shared clusters are generally used for development and small production
workloads.

## Tip

### See also:

Atlas M0 (Free Cluster), M2, and M5 Limitations

snapshot

    

Backup of your data captured at a specific interval and stored in a backup
data center. The Snapshot Schedule determines the interval for taking
snapshots and how long to store them.

## Tip

### See also:

Back Up, Restore, and Archive Data

team

    

Group of Atlas users in the same organization. You can use teams to grant
access to the same group of Atlas users across multiple projects. All users in
the team share the same project access.

## Note

Atlas users can belong to multiple teams.

## Tip

### See also:

  * Manage Organization Teams

  * Configure Access to the Atlas UI

← FAQ: SupportGet Help with Atlas →

