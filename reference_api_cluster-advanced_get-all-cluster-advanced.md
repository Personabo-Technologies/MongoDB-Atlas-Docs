Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get All Advanced Clusters

Share Feedback

On this page

  * Considerations
  * Required Roles
  * Resource
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Americas
  * Asia Pacific
  * Europe
  * Americas
  * Asia Pacific
  * Europe
  * Americas
  * Asia Pacific
  * Europe
  * Example Request
  * Example Response
  * Response Header
  * Response Body

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Note

This feature is not available for `M0` free clusters. For more information,
see Atlas M0 free cluster Limitations.

## Considerations

  * Each Atlas project supports up to 25 database deployments. Please contact Atlas support for questions or assistance regarding the database deployment limit. To contact support, select Support from the left-hand navigation bar of the Atlas UI.

## Required Roles

To use this resource, your API Key must have either the `Organization Owner`
or `Project Owner` roles.

## Resource

Base URL: `https://cloud.mongodb.com/api/atlas/v1.5`

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}  
      
  
### Request Path Parameters

Path Element

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

Unique identifier for the project in which to create the cluster.  
  
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

## Response Elements

Body Parameter

|

Type

|

Description  
  
||  
  
backupEnabled

|

Boolean

|

Flag that indicates whether the cluster can perform backups.

  * If **true** , the cluster can perform backups. You must set this value to **true** for NVMe clusters.

Backup uses:

    * Back Up Your Database Deployment for dedicated clusters.

    * Shared Cluster Backups for tenant clusters.

  * If **"backupEnabled" : false** , the cluster doesn't use Atlas backups.

This parameter defaults to **false**.  
  
biConnector

|

object

|

Configuration settings applied to BI Connector for Atlas on this cluster.

The MongoDB Connector for Business Intelligence for Atlas (BI Connector) is
only available for `M10` and larger clusters.

The BI Connector is a powerful tool which provides users SQL-based access to
their MongoDB databases. As a result, the BI Connector performs operations
which may be CPU and memory intensive. Given the limited hardware resources on
`M10` and `M20` cluster tiers, you may experience performance degradation of
the cluster when enabling the BI Connector. If this occurs, upgrade to an
`M30` or larger cluster or disable the BI Connector.  
  
biConnector

.enabled

|

Boolean

|

Flag that indicates whether this cluster has BI Connector for Atlas enabled.  
  
biConnector

.readPreference

|

string

|

Source from which the BI Connector for Atlas reads data. Each BI Connector for
Atlas read preference contains a distinct combination of readPreference and
readPreferenceTags options.

This API resource accepts **primary** , **secondary** , or **analytics**.

This parameter defaults to **analytics** if the cluster includes analytics
nodes. If the cluster lacks analyics nodes, the default value is
**secondary**.

To set the **readPreference** value to **"analytics"** requires the cluster to
have at least one analytics node. Once you have set the **readPreference**
value to **"analytics"** , you must have at least one analytics node in the
cluster.

 **See also:** BI Connector Read Preferences Table.  
  
clusterType

|

string

|

Type of the cluster that you want to create.

This API resource accepts REPLICASET, SHARDED, and GEOSHARDED.  
  
connectionStrings

|

object

|

Set of connection strings that your applications use to connect to this
cluster.

Use the parameters in this object to connect your applications to this
cluster.

 **See also:** Connection String Options

Atlas returns the contents of this object after the cluster has started, not
while it builds the cluster.  
  
connectionStrings

.privateEndpoint

|

array

|

Private endpoint connection strings. Each object describes the connection
strings you can use to connect to this cluster through a private endpoint.
Atlas returns this parameter only if you deployed a private endpoint to all
regions to which you deployed this cluster's nodes.  
  
connectionStrings

.privateEndpoint[n]

.connectionString

|

string

|

Private-endpoint-aware **mongodb://** connection string for this private
endpoint.  
  
connectionStrings

.privateEndpoint[n]

.endpoints

|

array

|

Private endpoint through which you connect to Atlas when you use
**connectionStrings.privateEndpoint[n].connectionString** or
**connectionStrings.privateEndpoint[n].srvConnectionString**.  
  
connectionStrings

.privateEndpoint[n]

.endpoints[n]

.endpointId

|

string

|

Unique identifier of the private endpoint.  
  
connectionStrings

.privateEndpoint[n]

.endpoints[n]

.providerName

|

string

|

Cloud provider to which you deployed the private endpoint. Atlas returns
**AWS** or **AZURE**.  
  
connectionStrings

.privateEndpoint[n]

.endpoints[n]

.region

|

string

|

Region to which you deployed the private endpoint.  
  
connectionStrings

.privateEndpoint[n]

.srvConnectionString

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

 **See also:** Seedlist format  
  
connectionStrings

.privateEndpoint[n]

.type

|

string

|

Type of MongoDB process that you connect to with the connection strings. Atlas
returns:

  *  **MONGOD** for replica sets, or

  *  **MONGOS** for sharded clusters.

  
  
connectionStrings

.standard

|

string

|

Public **mongodb://** connection string for this cluster.  
  
connectionStrings

.standardSrv

|

string

|

Public **mongodb+srv://** connection string for this cluster.

 **See also:** Seedlist format  
  
connectionStrings

.private

|

string

|

Network-peering-endpoint-aware **mongodb://** connection strings for each
interface VPC endpoint you configured to connect to this cluster. Atlas
returns this parameter only if you created a network peering connection to
this cluster.

For AWS clusters, Atlas doesn't return this parameter unless you enable custom
DNS.  
  
connectionStrings

.privateSrv

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

 **See also:** Seedlist format

For AWS clusters, Atlas doesn't return this parameter unless you enable custom
DNS.  
  
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
capacity, up to a maximum possible value of `4096` (i.e., 4 TB). This value
must be a positive number.

Set a value for **diskSizeGB** when you set values for **replicationSpecs**.

You can't set this value with clusters with local NVMe SSDs.

The minimum disk size for dedicated clusters is 10 GB for AWS and Google
Cloud. If you specify **diskSizeGB** with a lower disk size, Atlas defaults to
the minimum disk size value.

If your cluster includes Azure nodes, this value must correspond to an
existing Azure disk type (8, 16, 32, 64, 128, 256, 512, 1024, 2048, or 4095)

Atlas calculates storage charges differently depending on whether you choose
the default value or a custom value.

Atlas has disk capacity limits on single replica sets, scaling up to 4 TB for
higher cluster tiers. To expand the total cluster storage beyond default
limits, you can enable extended storage in the Project Settings. To
accommodate further scaling in the future, we recommend that you enable
sharding for long-term expansion.

If your cluster spans cloud service providers, this value defaults to the
minimum default of the providers involved.

 **See also:** Storage Capacity.  
  
encryptionAtRestProvider

|

string

|

Cloud service provider that offers Encryption at Rest.

AWS

GCP

Azure

NONE

Specify **AWS** to enable Encryption at Rest using the Atlas project AWS Key
Management System settings. The cluster must meet the following requirements:

|

Parameter

|

Requirement  
  
|  
  
replicationSpecs[n].regionConfigs[m].<type>Specs.instanceSize

|

 **M10** or greater  
  
backupEnabled

|

 **false** or omitted  
  
You must configure encryption at rest for the Atlas project before enabling it
on any cluster in the project.

 **See also:**

  * Encryption at Rest using Customer Key Management.

  * Prerequisites.

  
  
groupId

|

string

|

Unique 24-hexadecimal digit string that identifies the project in which the
cluster resides.  
  
id

|

string

|

Unique 24-hexadecimal digit string that identifies the cluster.  
  
labels

|

array

|

Collection of key-value pairs that tag and categorize the cluster. Each key
and value has a maximum length of 255 characters.

    
    
    | "labels": [  
      
       {  
         "key": "example key",  
         "value": "example value"  
       }  
     ]  
  
The Atlas console doesn't display your **labels**. The API returns the labels
in the response body when you use the API to:

  * get one Atlas cluster

  * get all Atlas clusters

  * modify a Atlas cluster

  
  
mongoDBMajorVersion

|

string

|

Version of the cluster to deploy. Atlas supports the following MongoDB
versions for **M10** or greater clusters:

  *  **3.6**

  *  **4.0**

  *  **4.2**

  *  **4.4**

If omitted, Atlas deploys a cluster that runs MongoDB 5.0.

If **"replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize": "M0"**,
**"M2"** , or **"M5"** , deploy MongoDB **5.0**.

Atlas always deploys the cluster with the latest stable release of the
specified version. You can upgrade to a newer version of MongoDB when you
modify a cluster.  
  
mongoDBVersion

|

string

|

Version of MongoDB that the cluster runs, in **X.Y.Z** format.  
  
name

|

string

|

Label that identifies this cluster. After Atlas creates the cluster, you can't
change its name.  
  
paused

|

Boolean

|

Flag that indicates whether the cluster has been paused.  
  
pitEnabled

|

Boolean

|

Flag that indicates whether the cluster uses continuous cloud backups.  
  
replicationSpecs

|

array

|

Configuration for cluster regions and the hardware provisioned in them.  
  
replicationSpecs[n]

.numShards

|

number

|

Positive integer that specifies the number of shards to deploy in each
specified zone.

This API resource accepts **1** through **50** , inclusive. This parameter
defaults to **1**.

If you specify a **numShards** value of **1** and a **clusterType** of
**SHARDED** , Atlas deploys a single-shard sharded cluster.

Don't create a sharded cluster with a single shard for production
environments. Single-shard sharded clusters don't provide the same benefits as
multi-shard configurations.

 **See Also:**

  * Sharding

  * Number of Nodes

  
  
replicationSpecs[n]

.regionConfigs

|

array

|

Hardware specifications for nodes set for a given region. Each
**regionConfigs** object describes the region's priority in elections and the
number and type of MongoDB nodes that Atlas deploys to the region.

Each **regionConfigs** object must have either an **analyticsSpecs** object,
**electableSpecs** object, or **readOnlySpecs** object.

  * Tenant clusters only require **electableSpecs**.

  * Dedicated clusters can specify any of these specifications, but must have at least one **electableSpecs** object within a **replicationSpec**.

  * Every hardware specification must use the same **instanceSize**.

## Example

If you set
**replicationSpecs[n].regionConfigs[m].analyticsSpecs.instanceSize** to
**M30** , you must set
**replicationSpecs[n].regionConfigs[m].electableSpecs.instanceSize** to
**M30** if you have electable nodes and
**replicationSpecs[n].regionConfigs[m].readOnlySpecs.instanceSize** to **M30**
if you have read-only nodes.  
  
replicationSpecs[n]

.regionConfigs[m]

.analyticsSpecs

|

object

|

Hardware specifications for analytics nodes needed in the region. Analytics
nodes handle analytic data such as reporting queries from BI Connector for
Atlas. Analytics nodes are read-only and can never become the primary.

If you don't specify this parameter, no analytics nodes deploy to this region.  
  
replicationSpecs[n]

.regionConfigs[m]

.analyticsSpecs

.diskIOPS

|

number

|

Target throughput (IOPS) desired for AWS storage attached to your cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

To change this value from the default, set
**replicationSpecs[n].regionConfigs[m].analyticsSpecs.ebsVolumeType** to
**PROVISIONED**.

Maximum input/output operations per second (IOPS) the cluster can perform. The
possible values depend on the selected **replicationSpecs[n].regionConfigs[m].
<type>Specs.instanceSize** and **diskSizeGB**.

This setting requires you to:

  * Set **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** to **M30** or greater

  * Not use clusters with local NVMe SSDs.

To view the possible range of IOPS values for the selected instance size and
storage capacity:

  1. Open the Atlas web console.

  2. Select Build a New Cluster.

  3. Under Cloud Provider & Region, select **AWS**.

  4. Under Cloud Provider & Region, select the region corresponding to your configured **replicationSpecs[n].regionConfigs[m].regionNamee**.

  5. Under Cluster Tier, select the cluster tier corresponding to your configured **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize**.

  6. Under Cluster Tier, set the Storage Capacity slider to your configured **diskSizeGB**. You can also enter the exact value of **diskSizeGB** in the box to the right of the slider.

Click Provision IOPS to see the available IOPS range.

If you set the **diskIOPS** value to a value higher than the default value for
the selected volume size, Atlas automatically sets
**replicationSpecs[n].regionConfigs[m]. <type>Specs.ebsVolumeType** to
**PROVISIONED**. If you manually set **diskIOPS** to the default value, you
must specify **replicationSpecs[n].regionConfigs[m].
<type>Specs.ebsVolumeType** to be either **PROVISIONED** or **STANDARD**.

This parameter defaults to the cluster tier's Standard IOPS value, as viewable
in the Atlas console.

If you change this value, the cluster cost also changes. To learn more, see
billing.

Atlas enforces the following minimum ratios for given cluster tiers. This
keeps cluster performance consistent with large datasets.

Instance sizes **M10** to **M40** have a ratio of disk capacity to system
memory of 60:1. Instance sizes greater than **M40** have a ratio of 120:1.

## Example

To support 3 TB (or 3,072 GB) of disk capacity, select a cluster tier with a
minimum of 32 GB of RAM. This would be **M50** or greater.  
  
replicationSpecs[n]

.regionConfigs[m]

.analyticsSpecs

.ebsVolumeType

|

string

|

Type of storage you want to attach to your AWS-provisioned cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

The API resource accepts **STANDARD** , the default, and **PROVISIONED**.

  *  **STANDARD** volume types can't exceed the default IOPS rate for the selected volume size.

  *  **PROVISIONED** volume types must fall within the allowable IOPS range for the selected volume size.

  
  
replicationSpecs[n]

.regionConfigs[m]

.analyticsSpecs

.instanceSize

|

string

|

Hardware specification for the instance sizes in this region. Each instance
size has a default storage and memory capacity. The instance size you select
applies to all the data-bearing hosts in your instance size.

 **See Also:** Number of Nodes.

If you deploy a Global Cluster, you must choose a instance size of **M30** or
greater.

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

Atlas supports deploying **M0** , **M2** and **M5** tiers into a subset of
available regions. The documentation for
**replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** includes a
list of these regions.

## Note

### Cluster Tier Naming Conventions

Cluster tier names that are:

  * Appended with **_NVME** ( **M40_NVME** for example) use direct attached NVMe storage for exceptional performance with the most I/O-intensive workloads.

  * Prepended with **R** instead of an **M** ( **R40** for example) run a low CPU version of the cluster.

  
  
replicationSpecs[n]

.regionConfigs[m]

.analyticsSpecs

.nodeCount

|

number

|

Number of analytics nodes for Atlas to deploy to the region. Analytics nodes
are useful for handling analytic data such as reporting queries from BI
Connector for Atlas. Analytics nodes are read-only, and can never become the
primary.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

|

object

|

Collection of settings that configures auto-scaling information for the
cluster.

The values for the **.autoScaling** parameter must be the same for every item
in the **replicationSpecs** array.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.diskGB

.enabled

|

Boolean

|

Flag that indicates whether this cluster enables disk auto-scaling. This
parameter defaults to **true**.

  * Set to **true** to enable disk auto-scaling.

  * Set to **false** to disable disk auto-scaling.

The maximum amount of RAM for the selected cluster tier and the oplog size can
limit storage auto-scaling. To learn more, see Customize Your Storage.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.compute

|

object

|

Collection of settings that configure how a cluster might scale its instance
size and whether the cluster can scale down.

Cluster tiers with **Low CPU** or **NVME** storage classes can't use auto-
scaling.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.compute

.enabled

|

Boolean

|

Flag that indicates whether instance size auto-scaling is enabled. This
parameter defaults to **false**.

  * Set to **true** to enable instance size auto-scaling. If enabled, you must specify a value for **replicationSpecs[n].regionConfigs[m].autoScaling.compute.maxInstanceSize**.

  * Set to **false** to disable instance size auto-scaling.

  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.compute

.scaleDownEnabled

|

Boolean

|

Flag that indicates whether the instance size may scale down. Atlas requires
this parameter if
**"replicationSpecs[n].regionConfigs[m].autoScaling.compute.enabled" : true**.

If you enable this option, specify a value for
**replicationSpecs[n].regionConfigs[m].autoScaling.compute.minInstanceSize**.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.compute

.minInstanceSize

|

string

|

Minimum instance size to which your cluster can automatically scale (such as
**M10** ). Atlas requires this parameter if
**"replicationSpecs[n].regionConfigs[m].autoScaling.compute. scaleDownEnabled"
: true**.  
  
replicationSpecs[n]

.regionConfigs[m]

.autoScaling

.compute

.maxInstanceSize

|

string

|

Maximum instance size to which your cluster can automatically scale (such as
**M40** ). Atlas requires this parameter if
**"replicationSpecs[n].regionConfigs[m].autoScaling.compute .enabled" :
true**.  
  
replicationSpecs[n]

.regionConfigs[m]

.backingProviderName

|

string

|

Cloud service provider on which you provision the host for a multi-tenant
cluster.

Use this setting only when
**"replicationSpecs[n].regionConfigs[m].providerName" : "TENANT"** and
**"replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize": M2** or
**M5**.

The API resource accepts the following values:

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

Use **replicationSpecs[n].regionConfigs[m].backingProviderName** to set the
cloud service provider.  
  
replicationSpecs[n]

.regionConfigs[m]

.electableSpecs

|

number

|

Hardware specifications for electable nodes in the region. Electable nodes can
become the primary and can enable local reads.

If you do not specify this option, no electable nodes are deployed to the
region.  
  
replicationSpecs[n]

.regionConfigs[m]

.electableSpecs

.diskIOPS

|

number

|

Target throughput (IOPS) desired for AWS storage attached to your cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

To change this value from the default, set **.ebsVolumeType** to
**PROVISIONED**.

Maximum input/output operations per second (IOPS) the cluster can perform. The
possible values depend on the selected **replicationSpecs[n].regionConfigs[m].
<type>Specs.instanceSize** and **diskSizeGB**.

This setting requires you to:

  * Set **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** to **M30** or greater

  * Not use clusters with local NVMe SSDs.

To view the possible range of IOPS values for the selected instance size and
storage capacity:

  1. Open the Atlas web console.

  2. Select Build a New Cluster.

  3. Under Cloud Provider & Region, select **AWS**.

  4. Under Cloud Provider & Region, select the region corresponding to your configured **replicationSpecs[n].regionConfigs[m].regionNamee**.

  5. Under Cluster Tier, select the cluster tier corresponding to your configured **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize**.

  6. Under Cluster Tier, set the Storage Capacity slider to your configured **diskSizeGB**. You can also enter the exact value of **diskSizeGB** in the box to the right of the slider.

Click Provision IOPS to see the available IOPS range.

If you set the **diskIOPS** value to a value higher than the default value for
the selected volume size, Atlas automatically sets
**replicationSpecs[n].regionConfigs[m]. <type>Specs.ebsVolumeType** to
**PROVISIONED**. If you manually set **diskIOPS** to the default value, you
must specify **replicationSpecs[n].regionConfigs[m].
<type>Specs.ebsVolumeType** to be either **PROVISIONED** or **STANDARD**.

This parameter defaults to the cluster tier's Standard IOPS value, as viewable
in the Atlas console.

If you change this value, the cluster cost also changes. To learn more, see
billing.

Atlas enforces the following minimum ratios for given cluster tiers. This
keeps cluster performance consistent with large datasets.

Instance sizes **M10** to **M40** have a ratio of disk capacity to system
memory of 60:1. Instance sizes greater than **M40** have a ratio of 120:1.

## Example

To support 3 TB (or 3,072 GB) of disk capacity, select a cluster tier with a
minimum of 32 GB of RAM. This would be **M50** or greater.  
  
replicationSpecs[n]

.regionConfigs[m]

.electableSpecs

.ebsVolumeType

|

string

|

Type of storage you want to attach to your AWS-provisioned cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

The API resource accepts **STANDARD** , the default, and **PROVISIONED**.

  *  **STANDARD** volume types can't exceed the default IOPS rate for the selected volume size.

  *  **PROVISIONED** volume types must fall within the allowable IOPS range for the selected volume size.

  
  
replicationSpecs[n]

.regionConfigs[m]

.electableSpecs

.instanceSize

|

string

|

Hardware specification for the instance sizes in this region. Each instance
size has a default storage and memory capacity. The instance size you select
applies to all the data-bearing hosts in your instance size.

 **See Also:** Number of Nodes.

If you deploy a Global Cluster, you must choose a instance size of **M30** or
greater.

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

Atlas supports deploying **M0** , **M2** and **M5** tiers into a subset of
available regions. The documentation for
**replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** includes a
list of these regions.

## Note

### Cluster Tier Naming Conventions

Cluster tier names that are:

  * Appended with **_NVME** ( **M40_NVME** for example) use direct attached NVMe storage for exceptional performance with the most I/O-intensive workloads.

  * Prepended with **R** instead of an **M** ( **R40** for example) run a low CPU version of the cluster.

  
  
replicationSpecs[n]

.regionConfigs[m]

.electableSpecs

.nodeCount

|

number

|

Number of electable nodes for Atlas to deploy to the region. Electable nodes
can become the primary and can enable local reads.

The combined **electableSpecs.nodeCount** across all
**replicationSpecs[n].regionConfigs[m]** objects must total **3** , **5** , or
**7**.

You cannot create electable nodes if the
**replicationSpecs[n].regionConfigs[m].priority** is **0**.  
  
replicationSpecs[n]

.regionConfigs[m]

.priority

|

Integer

|

Precedence is given to this region when a primary election occurs.

If your **regionConfigs** has only **.readOnlySpecs** , **.analyticsSpecs** ,
or both, set this value to **0**.

If you have multiple **regionConfigs** objects (your cluster is multi-region
or multi-cloud), they must have priorities in descending order. The highest
priority is **7**.

## Example

Set your highest priority region to **7** , your second-highest priority to
**6** , and your third-priority region to **5**. If you have no electable
nodes, set this value to **0**.

If your region has set **.electableSpecs.nodeCount** to **1** or higher, it
must have a priority of exactly one **(1)** less than another region in the
**replicationSpecs[n].regionConfigs[m]** array. The highest-priority region
**must** have a priority of **7**. The lowest possible priority is **1**.

The priority **7** region identifies the **Preferred Region** of the cluster.
Atlas places the primary node in the **Preferred Region**. Priorities **1**
through **7** are exclusive: you can't assign a given priority to more than
one region per cluster.

## Example

If you have three regions, their priorities would be **7** , **6** , and **5**
respectively. If you added two more regions for supporting electable nodes,
the priorities of those regions would be **4** and **3** respectively.  
  
replicationSpecs[n]

.regionConfigs[m]

.providerName

|

string

|

Cloud service provider on which Atlas provisions the hosts.

  * Set dedicated clusters to **AWS** , **GCP** , or **AZURE**.

  * Set M2/M5 clusters to **TENANT**.

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

Use **replicationSpecs[n].regionConfigs[m].backingProviderName** to set the
cloud service provider.  
  
 **M2** and **M5** clusters are multi-tenant deployments. You must set this
parameter to **TENANT** and specify the cloud service provider in
**replicationSpecs[n].regionConfigs[m].backingProviderName**.  
  
replicationSpecs[n]

.regionConfigs[m]

.readOnlySpecs

|

object

|

Hardware specifications for read-only nodes in the region. Read-only nodes can
never become the primary member, but can enable local reads.

If you don't specify this parameter, no read-only nodes are deployed to the
region.  
  
replicationSpecs[n]

.regionConfigs[m]

.readOnlySpecs

.diskIOPS

|

number

|

Target throughput (IOPS) desired for AWS storage attached to your cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

To change this value from the default, set **.ebsVolumeType** must be
**PROVISIONED**.

Maximum input/output operations per second (IOPS) the cluster can perform. The
possible values depend on the selected **replicationSpecs[n].regionConfigs[m].
<type>Specs.instanceSize** and **diskSizeGB**.

This setting requires you to:

  * Set **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** to **M30** or greater

  * Not use clusters with local NVMe SSDs.

To view the possible range of IOPS values for the selected instance size and
storage capacity:

  1. Open the Atlas web console.

  2. Select Build a New Cluster.

  3. Under Cloud Provider & Region, select **AWS**.

  4. Under Cloud Provider & Region, select the region corresponding to your configured **replicationSpecs[n].regionConfigs[m].regionNamee**.

  5. Under Cluster Tier, select the cluster tier corresponding to your configured **replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize**.

  6. Under Cluster Tier, set the Storage Capacity slider to your configured **diskSizeGB**. You can also enter the exact value of **diskSizeGB** in the box to the right of the slider.

Click Provision IOPS to see the available IOPS range.

If you set the **diskIOPS** value to a value higher than the default value for
the selected volume size, Atlas automatically sets
**replicationSpecs[n].regionConfigs[m]. <type>Specs.ebsVolumeType** to
**PROVISIONED**. If you manually set **diskIOPS** to the default value, you
must specify **replicationSpecs[n].regionConfigs[m].
<type>Specs.ebsVolumeType** to be either **PROVISIONED** or **STANDARD**.

This parameter defaults to the cluster tier's Standard IOPS value, as viewable
in the Atlas console.

If you change this value, the cluster cost also changes. To learn more, see
billing.

Atlas enforces the following minimum ratios for given cluster tiers. This
keeps cluster performance consistent with large datasets.

Instance sizes **M10** to **M40** have a ratio of disk capacity to system
memory of 60:1. Instance sizes greater than **M40** have a ratio of 120:1.

## Example

To support 3 TB (or 3,072 GB) of disk capacity, select a cluster tier with a
minimum of 32 GB of RAM. This would be **M50** or greater.  
  
replicationSpecs[n]

.regionConfigs[m]

.readOnlySpecs

.ebsVolumeType

|

string

|

Type of storage you want to attach to your AWS-provisioned cluster.

Set only if you selected AWS as your cloud service provider. You can't set
this parameter for a multi-cloud cluster.

The API resource accepts **STANDARD** , the default, and **PROVISIONED**.

  *  **STANDARD** volume types can't exceed the default IOPS rate for the selected volume size.

  *  **PROVISIONED** volume types must fall within the allowable IOPS range for the selected volume size.

  
  
replicationSpecs[n]

.regionConfigs[m]

.readOnlySpecs

.instanceSize

|

string

|

Hardware specification for the instance sizes in this region. Each instance
size has a default storage and memory capacity. The instance size you select
applies to all the data-bearing hosts in your instance size.

 **See Also:** Number of Nodes.

If you deploy a Global Cluster, you must choose a instance size of **M30** or
greater.

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

Atlas supports deploying **M0** , **M2** and **M5** tiers into a subset of
available regions. The documentation for
**replicationSpecs[n].regionConfigs[m]. <type>Specs.instanceSize** includes a
list of these regions.

## Note

### Cluster Tier Naming Conventions

Cluster tier names that are:

  * Appended with **_NVME** ( **M40_NVME** for example) use direct attached NVMe storage for exceptional performance with the most I/O-intensive workloads.

  * Prepended with **R** instead of an **M** ( **R40** for example) run a low CPU version of the cluster.

  
  
replicationSpecs[n]

.regionConfigs[m]

.readOnlySpecs

.nodeCount

|

number

|

Number of read-only nodes for Atlas to deploy to the region. Read-only nodes
can never become the primary, but can enable local reads.  
  
replicationSpecs[n]

.regionConfigs[m]

.regionName

|

string

|

Physical location of your MongoDB cluster nodes. The region you choose can
affect network latency for clients accessing your databases.

When Atlas deploys a dedicated cluster, Atlas checks if a VPC or VPC
connection exists for that provider and region. If not, Atlas creates them as
part of the deployment. Atlas assigns the VPC a CIDR block.

To limit a new VPC peering connection to one CIDR block and region, create the
connection first. Deploy the cluster after the connection starts.

Google Cloud Clusters

    Google Cloud Atlas clusters use a default CIDR block of **/18**. If your application requires a smaller block, create a network peering container first. Atlas limits the clusters you create to the regions in this new container you created.
Multi-Region Clusters

    Multi-region clusters require one VPC peering connection for each region. MongoDB nodes can use only the peering connection that resides in the same region as the nodes to communicate with the peered VPC.

To learn more, see Set Up a Network Peering Connection.

Select your cloud service provider's tab for example cluster region names:

AWS

Azure

GCP

  * `US_EAST_1`

  * `US_WEST_2`

  * `EU_WEST_1`

For a complete list of supported AWS regions, see Amazon Web Services (AWS).  
  
replicationSpecs[n]

.zoneName

|

string

|

Name for the zone in a Global Cluster. Provide this value if you set
**clusterType** to **GEOSHARDED**.  
  
rootCertType

|

string

|

Certificate Authority that MongoDB Atlas clusters use. You can specify
`ISRGROOTX1` (for ISRG Root X1).

## Note

Beginning on 1 May 2021, new TLS certificates that MongoDB Atlas creates use
ISRG instead of IdenTrust for their root Certificate Authority in line with
Let's Encrypt's announcement of this transition.  
  
stateName

|

string

|

Condition in which the API resource finds the cluster when you called the
resource. The resource returns one of the following states:

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

Method by which this cluster maintains the MongoDB versions. The resource
returns **CONTINUOUS** or **LTS** (Long Term Support).  
  
## Example Request

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Content-Type: application/json" \  
    3|      --include \  
    4|      --request GET "https://cloud.mongodb.com/api/atlas/v1.5/groups/{GROUP-ID}/clusters?pretty=true"  
  
## Example Response

### Response Header

    
    
    HTTP/1.1 401 Unauthorized  
      
    Content-Type: application/json;charset=ISO-8859-1  
    Date: {dateInUnixFormat}  
    WWW-Authenticate: Digest realm="MMS Public API", domain="", nonce="{nonce}", algorithm=MD5, op="auth", stale=false  
    Content-Length: {requestLengthInBytes}  
    Connection: keep-alive  
      
    
    HTTP/1.1 201 Created  
      
    Vary: Accept-Encoding  
    Content-Type: application/json  
    Strict-Transport-Security: max-age=300  
    Date: {dateInUnixFormat}  
    Connection: keep-alive  
    Content-Length: {requestLengthInBytes}  
  
### Response Body

    
    
    1| {  
    |  
    2|   "links": [  
    3|     {  
    4|       "href": "https://cloud.mongodb.com/api/atlas/v1.5/groups/{GROUP-ID}/clusters?pageNum=1&itemsPerPage=100",  
    5|       "rel": "self"  
    6|     }  
    7|   ],  
    8|   "results": [  
    9|     {  
    10|       "backupEnabled": true,  
    11|       "biConnector": {  
    12|         "enabled": false,  
    13|         "readPreference": "secondary"  
    14|       },  
    15|       "clusterType": "REPLICASET",  
    16|       "connectionStrings": {},  
    17|       "createDate": "2021-03-02T22:25:18Z",  
    18|       "diskSizeGB": 10.0,  
    19|       "encryptionAtRestProvider": "NONE",  
    20|       "groupId": "{GROUP-ID}",  
    21|       "id": "{CLUSTER-ID-1}",  
    22|       "labels": [],  
    23|       "mongoDBMajorVersion": "4.4",  
    24|       "mongoDBVersion": "4.4.4",  
    25|       "name": "basicReplicaSet",  
    26|       "paused": false,  
    27|       "pitEnabled": true,  
    28|       "replicationSpecs": [  
    29|         {  
    30|           "id": "{CLUSTER-1-ZONE-1}",  
    31|           "numShards": 1,  
    32|           "regionConfigs": [  
    33|             {  
    34|               "analyticsSpecs": {  
    35|                 "instanceSize": "M10",  
    36|                 "diskIOPS": 100,  
    37|                 "ebsVolumeType": "STANDARD",  
    38|                 "nodeCount": 0  
    39|               },  
    40|               "electableSpecs": {  
    41|                 "instanceSize": "M10",  
    42|                 "diskIOPS": 100,  
    43|                 "ebsVolumeType": "STANDARD",  
    44|                 "nodeCount": 3  
    45|               },  
    46|               "priority": 7,  
    47|               "providerName": "AWS",  
    48|               "readOnlySpecs": {  
    49|                 "instanceSize": "M10",  
    50|                 "diskIOPS": 100,  
    51|                 "ebsVolumeType": "STANDARD",  
    52|                 "nodeCount": 0  
    53|               },  
    54|               "regionName": "US_EAST_1"  
    55|             }  
    56|           ],  
    57|           "zoneName": "Zone 1"  
    58|         }  
    59|       ],  
    60|       "rootCertType": "ISRGROOTX1",  
    61|       "stateName": "CREATING"  
    62|     },  
    63|     {  
    64|       "backupEnabled": true,  
    65|       "biConnector": {  
    66|         "enabled": false,  
    67|         "readPreference": "secondary"  
    68|       },  
    69|       "clusterType": "REPLICASET",  
    70|       "connectionStrings": {},  
    71|       "createDate": "2021-03-02T22:36:20Z",  
    72|       "diskSizeGB": 2.0,  
    73|       "encryptionAtRestProvider": "NONE",  
    74|       "groupId": "{GROUP-ID}",  
    75|       "id": "{CLUSTER-ID-2}",  
    76|       "labels": [],  
    77|       "mongoDBMajorVersion": "4.4",  
    78|       "mongoDBVersion": "4.4",  
    79|       "name": "tenantCluster",  
    80|       "paused": false,  
    81|       "pitEnabled": false,  
    82|       "replicationSpecs": [  
    83|         {  
    84|           "id": "{CLUSTER-2-ZONE-1}",  
    85|           "numShards": 1,  
    86|           "regionConfigs": [  
    87|             {  
    88|               "electableSpecs": {  
    89|                 "instanceSize": "M2"  
    90|               },  
    91|               "backingProviderName": "AWS",  
    92|               "priority": 7,  
    93|               "providerName": "TENANT",  
    94|               "regionName": "US_EAST_1"  
    95|             }  
    96|           ],  
    97|           "zoneName": "Zone 1"  
    98|         }  
    99|       ],  
    100|       "rootCertType": "ISRGROOTX1",  
    101|       "stateName": "CREATING"  
    102|     },  
    103|     {  
    104|       "backupEnabled": true,  
    105|       "biConnector": {  
    106|         "enabled": false,  
    107|         "readPreference": "secondary"  
    108|       },  
    109|       "clusterType": "REPLICASET",  
    110|       "connectionStrings": {},  
    111|       "createDate": "2021-03-02T22:26:28Z",  
    112|       "diskSizeGB": 32.0,  
    113|       "encryptionAtRestProvider": "NONE",  
    114|       "groupId": "{GROUP-ID}",  
    115|       "id": "{CLUSTER-ID-3}",  
    116|       "labels": [],  
    117|       "mongoDBMajorVersion": "4.4",  
    118|       "mongoDBVersion": "4.4.4",  
    119|       "name": "crossCloudCluster",  
    120|       "paused": false,  
    121|       "pitEnabled": true,  
    122|       "replicationSpecs": [  
    123|         {  
    124|           "id": "{CLUSTER-3-ZONE-1}",  
    125|           "numShards": 1,  
    126|           "regionConfigs": [  
    127|             {  
    128|               "analyticsSpecs": {  
    129|                 "instanceSize": "M30",  
    130|                 "diskIOPS": 100,  
    131|                 "ebsVolumeType": "STANDARD",  
    132|                 "nodeCount": 1  
    133|               },  
    134|               "electableSpecs": {  
    135|                 "instanceSize": "M30",  
    136|                 "diskIOPS": 100,  
    137|                 "ebsVolumeType": "STANDARD",  
    138|                 "nodeCount": 3  
    139|               },  
    140|               "priority": 7,  
    141|               "providerName": "AWS",  
    142|               "readOnlySpecs": {  
    143|                 "instanceSize": "M30",  
    144|                 "diskIOPS": 100,  
    145|                 "ebsVolumeType": "STANDARD",  
    146|                 "nodeCount": 0  
    147|               },  
    148|               "regionName": "US_EAST_1"  
    149|             },  
    150|             {  
    151|               "analyticsSpecs": {  
    152|                 "instanceSize": "M30",  
    153|                 "nodeCount": 0  
    154|               },  
    155|               "electableSpecs": {  
    156|                 "instanceSize": "M30",  
    157|                 "nodeCount": 2  
    158|               },  
    159|               "priority": 6,  
    160|               "providerName": "GCP",  
    161|               "readOnlySpecs": {  
    162|                 "instanceSize": "M30",  
    163|                 "nodeCount": 0  
    164|               },  
    165|               "regionName": "NORTH_AMERICA_NORTHEAST_1"  
    166|             },  
    167|             {  
    168|               "analyticsSpecs": {  
    169|                 "instanceSize": "M30",  
    170|                 "nodeCount": 0  
    171|               },  
    172|               "electableSpecs": {  
    173|                 "instanceSize": "M30",  
    174|                 "nodeCount": 0  
    175|               },  
    176|               "priority": 0,  
    177|               "providerName": "GCP",  
    178|               "readOnlySpecs": {  
    179|                 "instanceSize": "M30",  
    180|                 "nodeCount": 1  
    181|               },  
    182|               "regionName": "NORTHEASTERN_ASIA_PACIFIC"  
    183|             },  
    184|             {  
    185|               "analyticsSpecs": {  
    186|                 "instanceSize": "M30",  
    187|                 "nodeCount": 0  
    188|               },  
    189|               "electableSpecs": {  
    190|                 "instanceSize": "M30",  
    191|                 "nodeCount": 0  
    192|               },  
    193|               "priority": 0,  
    194|               "providerName": "AZURE",  
    195|               "readOnlySpecs": {  
    196|                 "instanceSize": "M30",  
    197|                 "nodeCount": 1  
    198|               },  
    199|               "regionName": "EUROPE_NORTH"  
    200|             }  
    201|           ],  
    202|           "zoneName": "Zone 1"  
    203|         }  
    204|       ],  
    205|       "rootCertType": "ISRGROOTX1",  
    206|       "stateName": "CREATING"  
    207|     },  
    208|     {  
    209|       "backupEnabled": true,  
    210|       "biConnector": {  
    211|         "enabled": false,  
    212|         "readPreference": "secondary"  
    213|       },  
    214|       "clusterType": "GEOSHARDED",  
    215|       "connectionStrings": {},  
    216|       "createDate": "2021-03-02T22:27:46Z",  
    217|       "diskSizeGB": 40.0,  
    218|       "encryptionAtRestProvider": "NONE",  
    219|       "groupId": "{GROUP-ID}",  
    220|       "id": "{CLUSTER-ID-4}",  
    221|       "labels": [],  
    222|       "mongoDBMajorVersion": "4.4",  
    223|       "mongoDBVersion": "4.4.4",  
    224|       "name": "globalCluster",  
    225|       "paused": false,  
    226|       "pitEnabled": true,  
    227|       "replicationSpecs": [  
    228|         {  
    229|           "id": "{CLUSTER-4-ZONE-1}",  
    230|           "numShards": 1,  
    231|           "regionConfigs": [  
    232|             {  
    233|               "analyticsSpecs": {  
    234|                 "instanceSize": "M30",  
    235|                 "nodeCount": 0  
    236|               },  
    237|               "electableSpecs": {  
    238|                 "instanceSize": "M30",  
    239|                 "nodeCount": 3  
    240|               },  
    241|               "priority": 7,  
    242|               "providerName": "GCP",  
    243|               "readOnlySpecs": {  
    244|                 "instanceSize": "M30",  
    245|                 "nodeCount": 0  
    246|               },  
    247|               "regionName": "NORTH_AMERICA_NORTHEAST_1"  
    248|             }  
    249|           ],  
    250|           "zoneName": "Zone 1"  
    251|         },  
    252|         {  
    253|           "id": "{CLUSTER-4-ZONE-2}",  
    254|           "numShards": 1,  
    255|           "regionConfigs": [  
    256|             {  
    257|               "analyticsSpecs": {  
    258|                 "instanceSize": "M30",  
    259|                 "nodeCount": 0  
    260|               },  
    261|               "electableSpecs": {  
    262|                 "instanceSize": "M30",  
    263|                 "nodeCount": 3  
    264|               },  
    265|               "priority": 7,  
    266|               "providerName": "GCP",  
    267|               "readOnlySpecs": {  
    268|                 "instanceSize": "M30",  
    269|                 "nodeCount": 0  
    270|               },  
    271|               "regionName": "ASIA_NORTHEAST_2"  
    272|             }  
    273|           ],  
    274|           "zoneName": "Zone 2"  
    275|         },  
    276|         {  
    277|           "id": "{CLUSTER-4-ZONE-3}",  
    278|           "numShards": 1,  
    279|           "regionConfigs": [  
    280|             {  
    281|               "analyticsSpecs": {  
    282|                 "instanceSize": "M30",  
    283|                 "nodeCount": 0  
    284|               },  
    285|               "electableSpecs": {  
    286|                 "instanceSize": "M30",  
    287|                 "nodeCount": 3  
    288|               },  
    289|               "priority": 7,  
    290|               "providerName": "GCP",  
    291|               "readOnlySpecs": {  
    292|                 "instanceSize": "M30",  
    293|                 "nodeCount": 0  
    294|               },  
    295|               "regionName": "EUROPE_WEST_6"  
    296|             }  
    297|           ],  
    298|           "zoneName": "Zone 3"  
    299|         }  
    300|       ],  
    301|       "rootCertType": "ISRGROOTX1",  
    302|       "stateName": "CREATING"  
    303|     }  
    304|   ],  
    305| "totalCount": 4  
    306| }  
  
What is MongoDB Atlas? →

