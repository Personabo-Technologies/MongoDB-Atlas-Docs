Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Clusters

Share Feedback

On this page

  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
  * Americas
  * Asia Pacific
  * Europe
  * Example Request
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Important

### Multi-Cloud Clusters Unsupported

Atlas excludes multi-cloud clusters from this endpoint's response.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/clusters  
      
  
### Request Path Parameters

Path Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique identifier for the project whose clusters you want to retrieve.  
  
### Request Query Parameters

This endpoint may use any of the HTTP request query parameters available to
all Atlas Administration API resources. These are all optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
### Request Body Parameters

This endpoint doesn't use HTTP request body parameters.

## Response

Name

|

Type

|

Description  
  
||  
  
autoScaling

|

object

|

Collection of settings that configures auto-scaling information for the
cluster.

## Tip

### See also:

Configure Auto-Scaling.  
  
autoScaling.compute

|

object

|

Collection of settings that configure how a cluster might scale its cluster
tier and whether the cluster can scale down.  
  
autoScaling.compute.enabled

|

boolean

|

Flag that indicates whether cluster tier auto-scaling is enabled.  
  
autoScaling.compute.scaleDownEnabled

|

boolean

|

Flag that indicates whether the cluster tier can scale down.  
  
autoScaling.diskGBEnabled

|

boolean

|

Flag that indicates whether disk auto-scaling is enabled.  
  
backupEnabled

|

boolean

|

Flag that indicates whether legacy backup has been enabled.

## Important

Clusters running MongoDB `FCV` 4.2 or later and any new Atlas clusters of any
type do not support this parameter. These clusters must use Back Up Your
Database Deployment: **providerBackupEnabled**

This change doesn't affect existing Atlas clusters that use legacy backups.  
  
biConnector

|

object

|

Collection of settings that configure a BI Connector for Atlas for the
cluster.

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.  
  
biConnector.enabled

|

boolean

|

Flag that indicates whether Atlas enabled the BI Connector for Atlas for this
cluster.  
  
biConnector.readPreference

|

string

|

Source from which the BI Connector for Atlas reads data.

|

Value

|

Description  
  
|  
  
primary

|

BI Connector for Atlas reads data from the primary.  
  
secondary

|

BI Connector for Atlas reads data from a secondary.  
  
analytics

|

BI Connector for Atlas reads data from an

    analytics node.  
  
clusterType

|

string

|

Type of the cluster:

|

Value

|

Description  
  
|  
  
REPLICASET

|

replica set  
  
SHARDED

|

sharded cluster  
  
GEOSHARDED

|

global cluster  
  
connectionStrings

|

object

|

Set of connection strings that your applications use to connect to this
cluster.

Use the parameters in this object to connect your applications to this
cluster.

## Tip

### See also:

Connection String Options

Atlas returns the contents of this object after the cluster is operational,
not while it builds the cluster.  
  
connectionStrings.privateEndpoint

|

array of objects

|

Private endpoint connection strings. Each object describes the connection
strings you can use to connect to this cluster through a private endpoint.
Atlas returns this parameter only if you deployed a private endpoint to all
regions to which you deployed this cluster's nodes.  
  
connectionStrings.privateEndpoint[n].connectionString

|

string

|

Private-endpoint-aware **mongodb://** connection string for this private
endpoint.  
  
connectionStrings.privateEndpoint[n].endpoints

|

array of objects

|

Private endpoint through which you connect to Atlas when you use
**connectionStrings.privateEndpoint[n].connectionString** or
**connectionStrings.privateEndpoint[n].srvConnectionString**.  
  
connectionStrings.privateEndpoint[n].endpoints[n].endpointId

|

string

|

Unique identifier of the private endpoint.  
  
connectionStrings.privateEndpoint[n].endpoints[n].providerName

|

string

|

Cloud provider to which you deployed the private endpoint. Atlas returns
**AWS** , **AZURE** , or **GCP**.  
  
connectionStrings.privateEndpoint[n].endpoints[n].region

|

string

|

Region to which you deployed the private endpoint.  
  
connectionStrings.privateEndpoint[n].srvConnectionString

|

string

|

Private-endpoint-aware **mongodb+srv://** connection string for this private
endpoint.

The **mongodb+srv** protocol tells the driver to look up the seed list of
hosts in DNS. Atlas synchronizes this list with the nodes in a cluster. If the
connection string uses this URI format, you don't need to:

  * Append the seed list or

  * Change the URI if the nodes change.

Use this URI format if your driver supports it. If it doesn't, use
**connectionStrings.privateEndpoint[n].connectionString**.

## Tip

### See also:

Seedlist format  
  
connectionStrings.privateEndpoint[n].type

|

string

|

Type of MongoDB process that you connect to with the connection strings. Atlas
returns:

  *  **MONGOD** for replica sets, or

  *  **MONGOS** for sharded clusters.

  
  
connectionStrings.standard

|

string

|

Public **mongodb://** connection string for this cluster.  
  
connectionStrings.standardSrv

|

string

|

Public **mongodb+srv://** connection string for this cluster.

## Tip

### See also:

Seedlist format  
  
connectionStrings.private

|

string

|

Network-peering-endpoint-aware **mongodb://** connection strings for each
interface VPC endpoint you configured to connect to this cluster. Atlas
returns this parameter only if you created a network peering connection to
this cluster.

## Note

For AWS clusters, Atlas doesn't return this parameter unless you enable custom
DNS.  
  
connectionStrings.privateSrv

|

string

|

Network-peering-endpoint-aware **mongodb+srv://** connection strings for each
interface VPC endpoint you configured to connect to this cluster. Atlas
returns this parameter only if you created a network peering connection to
this cluster.

The **mongodb+srv** protocol tells the driver to look up the seed list of
hosts in DNS. Atlas synchronizes this list with the nodes in a cluster. If the
connection string uses this URI format, you don't need to:

  * Append the seed list or

  * Change the URI if the nodes change.

Use this URI format if your driver supports it. If it doesn't, use
**connectionStrings.private**.

## Tip

### See also:

Seedlist format

## Note

For AWS clusters, Atlas doesn't return this parameter unless you enable custom
DNS.  
  
connectionStrings.awsPrivateLink

|

object

|

## Important

This field is deprecated. Use
**connectionStrings.privateEndpoint[n].connectionString** instead.

## Note

Atlas returns this parameter only if:

  * the cluster is deployed to AWS, and

  * you deployed a AWS PrivateLink private endpoint to the same regions as all of this cluster's nodes.

Private-endpoint-aware **mongodb://** connection strings for each AWS
PrivateLink private endpoint. Atlas returns this parameter only if you
deployed a AWS PrivateLink private endpoint to the same regions as all of this
cluster's nodes.

In this object:

  * Each key is the unique identifier of an interface endpoint.

  * Each value is the **mongodb://** connection string you use to connect to Atlas through the interface endpoint the key names.

  
  
connectionStrings.awsPrivateLinkSrv

|

object

|

## Important

This field is deprecated. Use
**connectionStrings.privateEndpoint[n].srvConnectionString** instead.

## Note

Atlas returns this parameter only if:

  * the cluster is deployed to AWS, and

  * you deployed a AWS PrivateLink private endpoint to the same regions as all of this cluster's nodes.

Private-endpoint-aware **mongodb+srv://** connection strings for each AWS
PrivateLink private endpoint.

In this object:

  * Each key is the unique identifier of an interface endpoint.

  * Each value is the **mongodb+srv://** connection string you use to connect to Atlas through the interface endpoint the key names.

The **mongodb+srv** protocol tells the driver to look up the seed list of
hosts in DNS. Atlas synchronizes this list with the nodes in a cluster. If the
connection string uses this URI format, you don't need to:

  * Append the seed list or

  * Change the URI if the nodes change.

Use this URI format if your driver supports it. If it doesn't, use
**connectionStrings.awsPrivateLink**.

## Tip

### See also:

Seedlist format  
  
createDate

|

string

|

Timestamp in ISO 8601 date and time format in UTC when Atlas created the
cluster.  
  
diskSizeGB

|

number

|

Capacity, in gigabytes, of the host's root volume. Increase this number to add
capacity, up to a maximum possible value of **4096** (4 TB). This value must
be a positive number.

## Note

### When should you use diskSizeGB?

This setting:

  * Cannot be used with clusters with local NVMe SSDs

  * Cannot be used with Azure clusters. Use providerSettings.diskTypeName instead.

  * Must be used when **replicationSpecs** is set

The minimum disk size for dedicated clusters is 10 GB for AWS and Google
Cloud, and 32 GB for Azure. If you specify **diskSizeGB** with a lower disk
size, Atlas defaults to the minimum disk size value.

## Important

Atlas calculates storage charges differently depending on whether you choose
the default value or a custom value.

## Tip

### See also:

Storage Capacity.

Atlas has disk capacity limits on single replica sets, scaling up to 4 TB for
higher cluster tiers. To expand the total cluster storage beyond default
limits, you can enable extended storage in the Project Settings. To
accommodate further scaling in the future, we recommend that you enable
sharding for long-term expansion.  
  
encryptionAtRestProvider

|

string

|

Cloud service provider that offers Encryption at Rest.

## Tip

### See also:

  * Manage Customer Keys with AWS KMS

  * Prerequisites.

  
  
groupId

|

string

|

Unique identifier of the project to which the cluster belongs.  
  
id

|

string

|

Unique identifier of the cluster.  
  
labels

|

array of documents

|

Collection of key-value pairs that tag and categorize the cluster.  
  
mongoDBVersion

|

string

|

Version of MongoDB the cluster runs, in **< major version>.<minor
version>.<patch version>** format.  
  
mongoDBMajorVersion

|

string

|

Major version of MongoDB the cluster runs:

  * 4.2

  * 4.4

  * 5.0

  * 6.0

## Important

If your cluster runs a release candidate of MongoDB 6.0, Atlas will upgrade
the cluster to the stable release version when it is generally available.  
  
mongoURI

|

string

|

Base connection string for the cluster.

Atlas only displays this parameter after the cluster is operational, not while
it builds the cluster.  
  
mongoURIUpdated

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the connection string
was last updated. The connection string changes if you update any of the other
values.  
  
mongoURIWithOptions

|

string

|

connection string for connecting to the Atlas cluster. Includes the
**replicaSet** , **ssl** , and **authSource** query parameters in the
connection string with values appropriate for the cluster.

To review the connection string format, see the connection string format
documentation. To add database users to a Atlas project, see Configure
Database Users.

Atlas only displays this parameter after the cluster is operational, not while
it builds the cluster.  
  
name

|

string

|

Name of the cluster as it appears in Atlas.  
  
numShards

|

number

|

Positive integer that specifies the number of shards for a sharded cluster.

If this is set to **1** , the cluster is a replica set.

If this is set to **2** or higher, the cluster is a sharded cluster with the
number of shards specified.

## Tip

### See also:

Number of Nodes.

Atlas might return values between **1** and **50**.

## Note

Atlas doesn't return this value in the response body for Global Clusters.  
  
paused

|

boolean

|

Flag that indicates whether the cluster is paused.  
  
pitEnabled

|

boolean

|

Flag that indicates if the cluster uses Continuous Cloud Backup backups.  
  
providerBackupEnabled

|

boolean

|

This applies to dedicated clusters, **M10** or greater, only.

Flag that indicates if the cluster uses Back Up Your Database Deployment for
backups.

If **true** , the cluster uses Back Up Your Database Deployment for backups.
If **providerBackupEnabled** _and_ **backupEnabled** are **false** , the
cluster does not use Atlas backups.  
  
providerSettings

|

object

|

Configuration for the provisioned hosts on which MongoDB runs. The available
options are specific to the cloud service provider.  
  
providerSettings.autoScaling

|

object

|

Range of instance sizes to which your cluster can scale.

## Important

You can't specify the **providerSettings.autoScaling** object if
**"autoScaling.compute.enabled" : false**.  
  
providerSettings.autoScaling.compute

|

object

|

Range of instance sizes to which your cluster can scale. Atlas requires this
parameter if **"autoScaling.compute.enabled" : true**.  
  
providerSettings.autoScaling.compute.minInstanceSize

|

string

|

Minimum instance size to which your cluster can automatically scale.  
  
providerSettings.autoScaling.compute.maxInstanceSize

|

string

|

Maximum instance size to which your cluster can automatically scale.  
  
providerSettings.backingProviderName

|

string

|

Cloud service provider on which the multi-tenant host is provisioned. Atlas
returns this parameter only if **"providerSettings.providerName" : "TENANT"**.

Atlas can return:

|

|  
  
|  
  
AWS

|

Amazon AWS  
  
GCP

|

Google Cloud Platform  
  
AZURE

|

Microsoft Azure  
  
TENANT

|

 **M2** or **M5** multi-tenant cluster

Use **providerSettings.backingProviderName** to set the cloud service
provider.  
  
providerSettings.providerName

|

string

|

Cloud service provider on which Atlas provisioned the hosts.

Atlas can return:

|

|  
  
|  
  
AWS

|

Amazon AWS  
  
GCP

|

Google Cloud Platform  
  
AZURE

|

Microsoft Azure  
  
TENANT

|

 **M2** or **M5** multi-tenant cluster

Use **providerSettings.backingProviderName** to set the cloud service
provider.  
  
|  
  
|  
  
TENANT

|

 **M2** or **M5** multi-tenant cluster.

See **providerSettings.backingProviderName** for the cloud service provider
where Atlas provisioned the host serving the cluster.  
  
providerSettings.regionName

|

string

|

Physical location of your MongoDB cluster. The region you choose can affect
network latency for clients accessing your databases.

For a complete list of region name values, refer to the the cloud provider
reference pages:

  * AWS

  * GCP

  * Azure

For multi-region clusters, see **replicationSpec. <region>**.  
  
providerSettings.diskIOPS

|

number

|

Maximum IOPS the system can perform.  
  
providerSettings.diskTypeName

|

string

|

Disk type of the host's root volume for Azure instances.

The following table lists the possible values for this parameter, and their
corresponding storage size.

|

diskTypeName

|

Storage Size  
  
|  
  
P2 [1]

|

8GB  
  
P3 [2]

|

16GB  
  
P4 [3]

|

32GB  
  
P6 [4]

|

64GB  
  
P10

|

128GB  
  
P15

|

256GB  
  
P20

|

512GB  
  
P30

|

1024GB  
  
P40

|

2048GB  
  
P50

|

4095GB  
  
[1]|  Default for **M10** Azure clusters  
|  
[2]|  Default for **M20** Azure clusters  
|  
[3]|  Default for **M30** Azure clusters  
|  
[4]|  Default for **M40+** Azure clusters  
|  
  
providerSettings.encryptEBSVolume

|

boolean

|

Flag that indicates whether the Amazon EBS encryption feature encrypts the
host's root volume for both data at rest within the volume and for data moving
between the volume and the cluster.  
  
providerSettings.instanceSizeName

|

string

|

Name of the cluster tier used for the Atlas cluster.

Atlas supports deploying **M0** , **M2** and **M5** tiers into a subset of
available regions. Select your cloud provider's tab for example cluster region
names and available regions:

AWS

Azure

GCP

  * `US_EAST_1`

  * `US_WEST_2`

  * `EU_WEST_1`

For a complete list of supported AWS regions, see Amazon Web Services (AWS).

## Note

### Cluster Tier Naming Conventions

Cluster tier names that are:

  * Appended with **_NVME** ( **M40_NVME** for example) use direct attached NVMe storage for exceptional performance with the most I/O-intensive workloads.

  * Prepended with **R** instead of an **M** ( **R40** for example) run a low CPU version of the cluster.

AWS

Azure

GCP

|

Instance Size

|

Default Storage

|

Default RAM  
  
||  
  
M0

|

.5 GB

|

Shared  
  
M2

|

2 GB

|

Shared  
  
M5

|

5 GB

|

Shared  
  
M10 __

|

10 GB

|

2 GB  
  
M20 __

|

20 GB

|

4 GB  
  
M30 __

|

40 GB

|

8 GB  
  
M40 __

|

80 GB

|

16 GB  
  
R40 __

|

80 GB

|

16 GB  
  
M40_NVME

|

380 GB

|

15.25 GB  
  
M50 __

|

160 GB

|

32 GB  
  
R50 __

|

160 GB

|

32 GB  
  
M50_NVME

|

760 GB

|

30.5 GB  
  
M60 __

|

320 GB

|

64 GB  
  
R60 __

|

320 GB

|

64 GB  
  
M60_NVME

|

1.6 TB

|

61 GB  
  
M80 __

|

760 GB

|

131 GB  
  
R80 __

|

750 GB

|

122 GB  
  
M80_NVME

|

1.6 TB

|

122 GB  
  
M100

|

1 TB

|

160 GB  
  
M140 __

|

1 TB

|

192 GB  
  
M200 __

|

1.5 TB

|

256 GB  
  
R200 __

|

1.5 TB

|

256 GB  
  
M200_NVME

|

3.1 TB

|

244 GB  
  
M300 ____

|

2 TB

|

384 GB  
  
R300 __

|

2 TB

|

384 GB  
  
R400 __

|

3 TB

|

488 GB  
  
M400_NVME

|

4 TB

|

512 GB  
  
R700

|

4 TB

|

768 GB  
  
 __Can use this tier for a multi-cloud cluster.

 __Unavailable in the **AP_SOUTHEAST_2** region.

 **M0** , **M2** , and **M5** clusters are multi-tenant deployments. You must
set **providerSettings.providerName** to **TENANT** and specify the cloud
service provider in **providerSettings.backingProviderName**.  
  
replicationFactor

|

number

|

Number of replica set members. Each member keeps a copy of your databases,
providing high availability and data redundancy.

For multi-region clusters, add the total number of **replicationSpec.
<region>.electableNodes** to calculate the replication factor of the cluster.

If your cluster is a sharded cluster, each shard is a replica set with the
specified replication factor.

Atlas may return **3** , **5** , or **7**.

## Tip

### See also:

  * Number of Nodes

  * Replication

  
  
replicationSpec

|

object

|

Configuration of each region in the cluster. Each element in this object
represents a region where Atlas deploys your cluster.  
  
replicationSpec.<region>

|

object

|

Physical location of the region. The **< region>** string corresponds to a
region where Atlas deploys your cluster.

Each **< region>** object describes the region's priority in elections and the
number and type of MongoDB nodes Atlas deploys to the region.  
  
replicationSpec.<region>.analyticsNodes

|

number

|

Number of analytics nodes in the region. Analytics nodes are useful for
handling analytic data such as reporting queries from BI Connector for Atlas.
Analytics nodes are read-only, and can never become the primary.  
  
replicationSpec.<region>.electableNodes

|

number

|

Number of electable nodes in the region. Electable nodes can become the
primary and can facilitate local reads.  
  
replicationSpec.<region>.priority

|

number

|

Election priority of the region. The highest possible priority is **7** ,
which identifies the **Preferred Region** of the cluster. Atlas places the
primary node in the **Preferred Region**. The lowest possible priority is
**0** , which identifies a read-only region.

You can have any number of priority **0** read only regions. Priorities **1**
through **7** are exclusive: only one region per cluster can be assigned a
given priority.  
  
replicationSpec.<region>.readOnlyNodes

|

number

|

Number of read-only nodes in the region. Read-only nodes can never become the
primary member, but can facilitate local reads.  
  
replicationSpecs

|

array

|

Configuration for each zone in a Global Cluster. Each object in this array
represents a zone where Atlas deploys nodes for your Global Cluster.  
  
replicationSpecs[n].id

|

string

|

Unique identifier of the replication object.  
  
replicationSpecs[n].zoneName

|

string

|

Name for the zone.  
  
replicationSpecs[n].numShards

|

number

|

Number of shards to deploy in the specified zone.  
  
replicationSpecs[n].regionsConfig

|

object

|

Physical location of the region. Each **regionsConfig** object describes the
region's priority in elections and the number and type of MongoDB nodes that
Atlas deploys to the region.  
  
replicationSpecs[n].regionsConfig.<region>.analyticsNodes

|

number

|

Number of analytics nodes for Atlas to deploy to the region. Analytics nodes
are useful for handling analytic data such as reporting queries from BI
Connector for Atlas. Analytics nodes are read-only, and can never become the
primary.  
  
replicationSpecs[n].regionsConfig.<region>.electableNodes

|

number

|

Number of electable nodes for Atlas to deploy to the region. Electable nodes
can become the primary and can facilitate local reads.  
  
replicationSpecs[n].regionsConfig.<region>.readOnlyNodes

|

number

|

Number of read-only nodes for Atlas to deploy to the region. Read-only nodes
can never become the primary, but can facilitate local-reads.

Specify **0** if you do not want any read-only nodes in the region.  
  
replicationSpecs[n].regionsConfig.<region>.priority

|

number

|

Election priority of the region. If you have regions with only read-only
nodes, set this value to **0**.  
  
replicationSpecs[n].zoneName

|

string

|

Name for the zone in a Global Cluster. Do not provide this value if
**clusterType** is not **GEOSHARDED**.  
  
rootCertType

|

string

|

Certificate Authority that MongoDB Atlas clusters use. Value can be
`ISRGROOTX1` (for ISRG Root X1).

## Note

Beginning on 1 May 2021, new TLS certificates that MongoDB Atlas creates use
ISRG instead of IdenTrust for their root Certificate Authority in line with
Let's Encrypt's announcement of this transition.  
  
srvAddress

|

string

|

Connection string for connecting to the Atlas cluster. The **+srv** modifier
forces the connection to use TLS. The **mongoURI** parameter lists additional
options.  
  
stateName

|

string

|

Current state of the cluster. The possible states are:

  *  **IDLE**

  *  **CREATING**

  *  **UPDATING**

  *  **DELETING**

  *  **DELETED**

  *  **REPAIRING**

  
  
versionReleaseSystem

|

string

|

Release cadence that Atlas uses for this cluster. Atlas supports:

  *  **CONTINUOUS** : Atlas automatically updates your cluster to the latest major and rapid MongoDB releases as they become available.

  *  **LTS** : Atlas automatically updates your cluster to subsequent patch releases of this MongoDB version. Atlas doesn't update your cluster to newer rapid or major MongoDB releases as they become available.

  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/clusters/?pretty=true"  
  
### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 200 OK  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "autoScaling":{  
    3|     "compute":{  
    4|       "enabled":false,  
    5|       "scaleDownEnabled":false  
    6|     },  
    7|     "diskGBEnabled":true  
    8|   },  
    9|   "backupEnabled":false,  
    10|   "biConnector":{  
    11|     "enabled":false,  
    12|     "readPreference":"secondary"  
    13|   },  
    14|   "clusterType":"REPLICASET",  
    15|   "connectionStrings":{  
    16|     "privateEndpoint":[  
    17|       {  
    18|         "connectionString":"mongodb://pl-0-us-east-1.uzgh6.mongodb.net:1024,pl-0-us-east-1.uzgh6.mongodb.net:1025,pl-0-us-east-1.uzgh6.mongodb.net:1026/?ssl=true&authSource=admin&replicaSet=atlas-8dhkjj-shard-0",  
    19|         "endpoints":[  
    20|           {  
    21|             "endpointId":"vpce-0c86b555d9a233152",  
    22|             "providerName":"AWS",  
    23|             "region":"US_EAST_1"  
    24|           }  
    25|         ],  
    26|         "srvConnectionString":"mongodb+srv://cluster1-pl-0.uzgh6.mongodb.net",  
    27|         "type":"MONGOD"  
    28|       }  
    29|     ],  
    30|     "standardSrv":"mongodb+srv://cluster1.uzgh6.mongodb.net",  
    31|     "awsPrivateLink":{  
    32|       "vpce-0c86b555d9a233152":"mongodb://pl-0-us-east-1.uzgh6.mongodb.net:1024,pl-0-us-east-1.uzgh6.mongodb.net:1025,pl-0-us-east-1.uzgh6.mongodb.net:1026/?ssl=true&authSource=admin&replicaSet=atlas-8dhkjj-shard-0"  
    33|     },  
    34|     "awsPrivateLinkSrv":{  
    35|       "vpce-0c86b555d9a233152":"mongodb+srv://cluster1-pl-0.uzgh6.mongodb.net"  
    36|     },  
    37|     "standard":"mongodb://cluster1-shard-00-00.uzgh6.mongodb.net:27017,cluster1-shard-00-01.uzgh6.mongodb.net:27017,cluster1-shard-00-02.uzgh6.mongodb.net:27017/?ssl=true&authSource=admin&replicaSet=atlas-8dhkjj-shard-0"  
    38|   },  
    39|   "createDate":"2020-10-03T17:34:08Z",  
    40|   "diskSizeGB":10.0,  
    41|   "encryptionAtRestProvider":"NONE",  
    42|   "groupId":"5df90590f10fab5e33de2305",  
    43|   "id":"5e5ff4e65cba47109cf84f1a",  
    44|   "labels":[],  
    45|   "mongoDBMajorVersion":"4.2",  
    46|   "mongoDBVersion":"4.2.3",  
    47|   "mongoURI":"mongodb://cluster0-shard-00-00-auylw.mongodb.net:27017,cluster0-shard-00-01-auylw.mongodb.net:27017,cluster0-shard-00-02-auylw.mongodb.net:27017",  
    48|   "mongoURIUpdated":"2020-10-04T18:41:14Z",  
    49|   "mongoURIWithOptions":"mongodb://cluster0-shard-00-00-auylw.mongodb.net:27017,cluster0-shard-00-01-auylw.mongodb.net:27017,cluster0-shard-00-02-auylw.mongodb.net:27017/?ssl=true&authSource=admin&replicaSet=Cluster0-shard-0",  
    50|   "name":"Cluster0",  
    51|   "numShards":1,  
    52|   "paused":false,  
    53|   "pitEnabled":false,  
    54|   "providerBackupEnabled":false,  
    55|   "providerSettings":{  
    56|     "providerName":"AWS",  
    57|     "autoScaling":{  
    58|       "compute":{  
    59|         "maxInstanceSize":null,  
    60|         "minInstanceSize":null  
    61|       }  
    62|     },  
    63|     "diskIOPS":100,  
    64|     "encryptEBSVolume":true,  
    65|     "instanceSizeName":"M10",  
    66|     "regionName":"US_EAST_1",  
    67|     "volumeType":"STANDARD"  
    68|   },  
    69|   "replicationFactor":3,  
    70|   "replicationSpec":{  
    71|     "US_EAST_1":{  
    72|       "analyticsNodes":0,  
    73|       "electableNodes":3,  
    74|       "priority":7,  
    75|       "readOnlyNodes":0  
    76|     }  
    77|   },  
    78|   "replicationSpecs":[  
    79|     {  
    80|       "id":"5e5ff4df5cba47109cf84ee8",  
    81|       "numShards":1,  
    82|       "regionsConfig":{  
    83|         "US_EAST_1":{  
    84|           "analyticsNodes":0,  
    85|           "electableNodes":3,  
    86|           "priority":7,  
    87|           "readOnlyNodes":0  
    88|         }  
    89|       },  
    90|       "zoneName":"Zone 1"  
    91|     }  
    92|   ],  
    93|   "rootCertType": "ISRGROOTX1",  
    94|   "srvAddress":"mongodb+srv://cluster0-auylw.mongodb.net",  
    95|   "stateName":"IDLE",  
    96|   "links":[  
    97|     {  
    98|       "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/5df90590f10fab5e33de2305/clusters/Cluster0",  
    99|       "rel":"self"  
    100|     },  
    101|     {  
    102|       "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/5df90590f10fab5e33de2305/clusters/Cluster0/restoreJobs",  
    103|       "rel":"http://mms.mongodb.com/restoreJobs"  
    104|     },  
    105|     {  
    106|       "href":"https://cloud.mongodb.com/api/atlas/v1.0/groups/5df90590f10fab5e33de2305/clusters/Cluster0/snapshots",  
    107|       "rel":"http://mms.mongodb.com/snapshots"  
    108|     }  
    109|   ]  
    110| }  
  
What is MongoDB Atlas? →

