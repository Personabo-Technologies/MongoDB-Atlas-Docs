Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Limitations

Share Feedback

On this page

  * Cluster Limits
  * Connection Limits and Cluster Tier
  * Collection and Index Limits
  * Organization and Project Limits
  * Label Limits
  * Database User Privilege Limits
  * Serverless Instance Limits
  * Multi-Cloud Deployment Limits

Atlas limits how many of each kind of component you can create, and the number
of connections allowed to a database deployments. For clusters, the number of
connections allowed is based on cluster tier. These tables outline component
and connection limits.

## Important

If any of these limits present a problem for your organization, please contact
Atlas support.

## Cluster Limits

Component

|

Limit  
  
|  
  
Shards in Multi-Region Clusters

|

12  
  
Shards in Single-region clusters

|

50  
  
Cross-region network permissions for a Multi-Region Cluster

|

40

## Note

If any project's cluster spans more than 40 regions, you can't create a multi-
region cluster in this project.  
  
Electable Nodes per Replica Set or Shard

|

7  
  
Config Server Tier (minimum and maximum)

|

`M30`  
  
## Connection Limits and Cluster Tier

Atlas sets the `limits for concurrent incoming connections` based on the
cluster tier and class. Atlas connection limits apply per node. For sharded
clusters, Atlas connection limits apply per mongos router. The number of
mongos routers is equal to the number of replica set nodes across all shards.

Your read preference also contributes to the total number of connections Atlas
can allocate for a given query.

## Example

Your M2 cluster has three nodes with a 500 connection limit per node. Atlas
reserves 10 connections per node. If you set your read preference to
secondary, Atlas can read from the two secondary nodes for a combined 980
connection limit.

AWS

Azure and GCP

General Class

Low-CPU Class

Cluster Tier

|

Maximum Connections Per Node  
  
|  
  
`M0`

|

500  
  
`M2`

|

500  
  
`M5`

|

500  
  
`M10`

|

1500  
  
`M20`

|

3000  
  
`M30`

|

3000  
  
`M40`

|

6000  
  
`M50`

|

16000  
  
`M60`

|

32000  
  
`M80`

|

96000  
  
`M140`

|

96000  
  
`M200`

|

128000  
  
`M300`

|

128000  
  
## Note

Atlas reserves a small number of connections to each Atlas cluster for
supporting Atlas services. Contact Atlas support for more information on Atlas
reserved connections.

## Collection and Index Limits

While there is no hard limit on the number of collections in a single cluster,
the performance of a cluster might degrade if it serves a large number of
collections and indexes. Larger collections have a greater impact on
performance.

The recommended maximum combined number of collections and indexes by Atlas
cluster tier are as follows:

Cluster tier

|

Recommended maximum  
  
|  
  
M10

|

5,000 collections and indexes  
  
M20 / M30

|

10,000 collections and indexes  
  
M40+

|

100,000 collections and indexes  
  
## Organization and Project Limits

Component

|

Limit  
  
|  
  
Database Users per Atlas Project

|

100  
  
Atlas Users per Atlas Project

|

500  
  
Atlas Users per Atlas Organization

|

500  
  
API Keys per Atlas Organization

|

500  
  
Access List Entries per Atlas Project

|

200  
  
Users per Atlas Team

|

250  
  
Teams per Atlas Project

|

100  
  
Teams per Atlas Organization

|

250  
  
Teams per Atlas User

|

100  
  
Organizations per Atlas User

|

250  
  
Linked Organizations per Atlas User

|

50  
  
Clusters per Atlas Project

|

25  
  
Projects per Atlas Organization

|

250  
  
Custom MongoDB roles per Atlas Project

|

100  
  
Assigned Roles per Database User

|

100  
  
Hourly Billing per Atlas Organization

|

$50  
  
Federated database instances per Atlas Project

|

25  
  
Total Network Peering Connections per Atlas Project

|

50

## Note

Atlas limits the number of nodes per Network Peering connection based on the
CIDR block and the region selected for the project.  
  
Pending Network Peering Connections per Atlas Project

|

25  
  
AWS PrivateLink Addressable Targets per Region

|

50  
  
Azure Private Link Addressable Targets per Region

|

150  
  
## Label Limits

Atlas also limits how long particular labels of components can be.

Component

|

Character Limit

|

RegEx Pattern  
  
||  
  
Cluster Name

|

64 [1]

|

`^([a-zA-Z0-9]([a-zA-Z0-9-]){0,21}(?<!-)([\w]{0,42}))$` [2]  
  
Project Name

|

64

|

`^[\p{L}\p{N}\-_.(),:&@+']{1,64}$` [3]  
  
Organization Name

|

64

|

`^[\p{L}\p{N}\-_.(),:&@+']{1,64}$` [3]  
  
API Key Description

|

250

|  
  
[1]|  If you have peering-only mode enabled, the cluster name character limit
is 23.  
|  
[2]|  Atlas uses the first _23 characters_ of a cluster name. These characters
must be unique within the containing project. Cluster names with less than 23
characters can't end with hyphen (`-`). Cluster names with more than 23
characters can't have a hyphen as the 23rd character.  
|  
[3]|  _(1, 2)_ Organization and Product names can include any Unicode letter
or number plus the following punctuation: `-_.(),:&@+'`.  
|  
  
## Database User Privilege Limits

To learn more about unsupported commands, see the unsupported commands for
free or shared clusers, paid clusters, and serverless instances.

## Serverless Instance Limits

Serverless instances have different limitations. To learn more, see Serverless
Instance Limitations.

## Multi-Cloud Deployment Limits

Multi-cloud deployments have different limitations. To learn more, see Multi-
Cloud Deployment Limitations.

← LimitationsServerless Instance Limitations →

