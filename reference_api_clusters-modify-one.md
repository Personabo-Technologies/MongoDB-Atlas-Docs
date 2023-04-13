Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Modify a Cluster

Share Feedback

On this page

  * Considerations
  * Request
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response
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

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Considerations

Clusters can span regions and cloud service providers. The total number of
nodes in clusters spanning across regions has a specific constraint on a per-
project basis.

Atlas limits the total number of nodes in other regions in one project to a
total of 40. This total excludes:

  * Google Cloud regions communicating with each other

  * Free clusters or shared clusters

The total number of nodes between any two regions must meet this constraint.

## Example

If an Atlas project has nodes in clusters spread across three regions:

  * 30 nodes in **Region A**

  * 10 nodes in **Region B**

  * 5 nodes in **Region C**

You can only add 5 more nodes to **Region C** because:

  1. If you exclude Region C, Region A + Region B = 40. __

  2. If you exclude Region B, Region A + Region C = 35, <= 40. __

  3. If you exclude Region A, Region B + Region C = 15, <= 40. __

  4. Each combination of regions with the added 5 nodes still meets the per-project constraint:

    * Region A + B = 40 __

    * Region A + C = 40 __

    * Region B + C = 20 __

You can't create a multi-region cluster in a project if it has one or more
clusters spanning 40 or more nodes in other regions.

Contact Atlas support for questions or assistance with raising this limit.

## Request

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    PATCH /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}  
      
  
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

Unique identifier for the project containing the cluster.  
  
CLUSTER-NAME

|

string

|

Required

|

Name of the cluster to modify.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

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
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

## Important

If modifying any of the `providerSettings` or `replicationSpec` values, you
_must_ specify the `providerSettings.providerName`. For `M2` and `M5`
clusters, you must also specify the `providerSettings.backingProviderName`.

You can't modify a `paused` cluster other than to resume the cluster. Nor can
you pause a cluster with pending changes.

You do not need to provide all parameters when modifying a cluster, only the
parameters you want to change and any parameters required to make that change.

Body Parameter

|

Type

|

Necessity

|

Description  
  
|||  
  
autoScaling

|

object

|

Optional

|

Collection of settings that configures auto-scaling information for the
cluster.

If you specify the **autoScaling** object, you must also specify the
**providerSettings.autoScaling** object.

## Tip

### See also:

Configure Auto-Scaling.  
  
autoScaling.compute

|

object

|

Optional

|

Specifies whether the cluster automatically scales its cluster tier and
whether the cluster can scale down.

## Important

Cluster tier auto-scaling is not available for clusters using **NVME** storage
classes.  
  
autoScaling.compute.enabled

|

boolean

|

Optional

|

Flag that indicates whether cluster tier auto-scaling is enabled. The default
is **false**.

  * Set to **true** to enable cluster tier auto-scaling. If enabled, you must specify a value for **providerSettings.autoScaling.compute.maxInstanceSize**.

  * Set to **false** to disable cluster tier auto-scaling.

## Note

If you disable auto-scaling for your cluster, Atlas sets your minimum and
maximum autoscaling bounds to **null**. If you re-enable autoscaling at a
later time, you must set new values for
**providerSettings.autoScaling.compute.minInstanceSize** and
**providerSettings.autoScaling.compute.maxInstanceSize**.  
  
autoScaling.compute.scaleDownEnabled

|

boolean

|

Conditional

|

Flag that indicates whether the cluster tier may scale down. Atlas requires
this parameter if **"autoScaling.compute.enabled" : true**.

If you enable this option, specify a value for
**providerSettings.autoScaling.compute.minInstanceSize**.

## Note

To configure this value, you must set `autoScaling.compute.enabled` to `true`.
In previous versions of Atlas, you could configure this value when
`autoScaling.compute.enabled` was `false`.  
  
autoScaling.diskGBEnabled

|

boolean

|

Optional

|

Flag that indicates whether disk auto-scaling is enabled. The default is
**true**.

  * Set to **true** to enable disk auto-scaling.

  * Set to **false** to disable disk auto-scaling.

The maximum amount of RAM for the selected cluster tier and the oplog size can
limit storage auto-scaling. To learn more, see Customize Your Storage.  
  
backupEnabled

|

boolean

|

Optional

|

Flag that indicates whether legacy backups have been enabled.

Set to **false** to disable legacy backups for the cluster. Atlas deletes any
stored snapshots. See the legacy backup Snapshot Schedule for more
information.

You cannot enable legacy backups if you have an existing cluster in the
project with Back Up Your Database Deployment enabled.

The default value is **false**.

## Note

This option is not supported on clusters running MongoDB 4.2. Clusters running
MongoDB 4.2 must use Back Up Your Database Deployment.

## Important

Clusters running MongoDB `FCV` 4.2 or later and any new Atlas clusters of any
type do not support this parameter. These clusters must use Back Up Your
Database Deployment: **providerBackupEnabled**

If you create a new Atlas cluster and set **"backupEnabled" : true** , the API
responds with an error.

This change doesn't affect existing clusters that use legacy backups.  
  
biConnector

|

object

|

Optional

|

Configuration of BI Connector for Atlas on this cluster.

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

Optional

|

Flag that indicates whether or not BI Connector for Atlas is enabled on the
cluster.

  * Set to **true** to enable BI Connector for Atlas.

  * Set to **false** to disable BI Connector for Atlas.

  
  
biConnector.readPreference

|

string

|

Optional

|

Source from which the BI Connector for Atlas reads data. Each BI Connector for
Atlas read preference contains a distinct combination of readPreference and
readPreferenceTags options.

## Tip

### See also:

BI Connector Read Preferences Table.

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

BI Connector for Atlas reads data from a secondary. _The preference defaults
to this value if there are no analytics nodes in the cluster_.  
  
analytics

|

BI Connector for Atlas reads data from an analytics node. _Default if the
cluster contains analytics nodes_.  
  
## Note

To set the **readPreference** value to **"analytics"** , the cluster must have
at least one analytics node.

If the **readPreference** value is **"analytics"** , you cannot remove all
analytics nodes from the cluster.  
  
clusterType

|

string

|

Conditional

|

Type of the cluster that you want to modify.

You cannot convert a sharded cluster deployment to a replica set deployment.

## Note

### When should you use clusterType?

|

Condition

|

Necessity  
  
|  
  
You set **replicationSpecs**.

|

Required  
  
You are deploying Global Clusters.

|

Required  
  
You are deploying non-Global replica sets and sharded clusters.

|

Optional  
  
Atlas accepts:

Value

|

Cluster Type  
  
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
  
diskSizeGB

|

number

|

Conditional

|

Capacity, in gigabytes, of the host's root volume. Increase this number to add
capacity, up to a maximum possible value of **4096** (4 TB). This value must
be a positive integer.

## Note

### When should you use diskSizeGB?

This setting:

  * Cannot be used with clusters with local NVMe SSDs.

  * Cannot be used with Azure clusters. Use providerSettings.diskTypeName instead.

  * Must be used when **replicationSpecs** is set.

The minimum disk size for dedicated clusters is 10 GB for AWS and Google
Cloud, and 32 GB for Azure. If you specify **diskSizeGB** with a lower disk
size, Atlas defaults to the minimum disk size value.

Each cluster tier has its own default value. If you set a value below the
cluster default, Atlas replaces it with the default value. To view default
values: open the Atlas web interface; click the button to add a new cluster;
view the available default sizes; close the window without saving changes.

## Important

Atlas calculates storage charges differently depending on whether you choose
the default value or a custom value. For details, see Storage Capacity.

Atlas has disk capacity limits on single replica sets, scaling up to 4 TB for
higher cluster tiers. To expand the total cluster storage beyond default
limits, you can enable extended storage in the Project Settings. To
accommodate further scaling in the future, we recommend that you enable
sharding for long-term expansion.

## Note

When you increase the storage capacity of a cluster, Atlas increases the
cluster's oplog size. Atlas scales the oplog to 5% of the cluster capacity,
not to exceed 50 GB. NVMe storage requires an oplog which is 10% of the
storage capacity. Atlas doesn't change the oplog size if it exceeds 5% of the
new storage capacity (10% in the case of NVMe storage).

As cluster storage capacity decreases, Atlas doesn't change the oplog size
unless it exceeds a certain maximum determined according to MongoDB best
practices.  
  
encryptionAtRestProvider

|

string

|

Optional

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
  
providerSettings.instanceSizeName

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

  
  
labels

|

array of objects

|

Optional

|

Collection of key-value pairs that tag and categorize the cluster.

Each key and value has a maximum length of 255 characters.

    
    
    | "labels": [  
      
       {  
         "key": "example key",  
         "value": "example value"  
       }  
     ]  
  
## Note

The Atlas console doesn't display your **labels**. Atlas returns them in the
response body when you use the Atlas Administration API to

  * get one Atlas cluster

  * get all Atlas clusters

  * modify a Atlas cluster

  
  
mongoDBMajorVersion

|

string

|

Optional

|

Version of the cluster to deploy. Atlas supports the following MongoDB
versions for **M10+** clusters:

  * 4.2

  * 4.4

  * 5.0

  * 6.0

## Important

If your cluster runs a release candidate of MongoDB 6.0, Atlas will upgrade
the cluster to the stable release version when it is generally available.

You must deploy MongoDB **5.0** if **"providerSettings.instanceSizeName" :
"M0"** , **"M2"** or **"M5"**.

Atlas always deploys the cluster with the latest stable release of the
specified version. You can upgrade to a newer version of MongoDB when you
modify a cluster

## Note

If you are upgrading from version **4.0** to **4.2** and you have legacy
backups enabled, you must set **backupEnabled** to **false** and set
**providerBackupEnabled** to **true** as part of the API request. Continuous
backups are no longer supported in MongoDB version **4.2**. Instead, use Back
Up Your Database Deployment.

If **mongoDBMajorVersion** is set to **CONTINUOUS** , you must omit the
**mongoDBMajorVersion** field. You can't modify the MongoDB version that you
clusters run when you choose the continuous release cadence.  
  
name

|

string

|

Optional

|

Name of the cluster as it appears in Atlas. After Atlas creates the cluster,
you can't change its name.  
  
numShards

|

number

|

Conditional

|

Positive integer that specifies the number of shards to deploy for a sharded
cluster.

## Important

If you use the **replicationSpecs** parameter, you must set **numShards**.

Atlas accepts **1** through **50** , inclusive. The default value is **1**.

  * If you specify a **numShards** value of **1** and a **clusterType** of **SHARDED** , Atlas deploys a single-shard sharded cluster.

  * If you specify a **numShards** value of **1** and a **clusterType** of **REPLICASET** , Atlas deploys a replica set.

Don't create a sharded cluster with a single shard for production
environments. Single-shard sharded clusters don't provide the same benefits as
multi-shard configurations.

For more information on sharded clusters, see Sharding in the MongoDB manual.

For details on how this setting affects costs, see Number of Nodes.

## Note

Do not include in the request body for Global Clusters.  
  
paused

|

boolean

|

Optional

|

Indicates whether the cluster is paused or not. The default value is false.

You cannot create a paused cluster. Either omit the parameter or explicitly
set to false.  
  
pitEnabled

|

boolean

|

Optional

|

Indicates if the cluster uses continuous cloud backups. If set to **true** ,
**providerBackupEnabled** must also be set to **true**.  
  
providerBackupEnabled

|

boolean

|

Conditional

|

Set **true** or **false** to enable or disable Back Up Your Database
Deployment for cluster backups. If **providerBackupEnabled** _and_
**backupEnabled** are **false** , the cluster does not use Atlas backups.

If you disable legacy backups for the cluster, Atlas deletes all stored
snapshots. See the legacy backup Snapshot Schedule for more information.

You cannot enable Cloud Backups if you have an existing cluster in the project
with Legacy Backups (Deprecated) enabled.

## Important

You must set this value to **true** for NVMe clusters.  
  
providerSettings

|

object

|

Optional

|

Configuration for the provisioned servers on which MongoDB runs. The available
options are specific to the cloud service provider.  
  
providerSettings.autoScaling

|

object

|

Conditional

|

Contains the **minInstanceSize** and **maxInstanceSize** parameters which
specify the range of instance sizes to which your cluster can scale. Atlas
requires this parameter if **"autoScaling.compute.enabled" : true**.

## Important

To configure this value, you must set `autoScaling.compute.enabled` to `true`.
In previous versions of Atlas, you could configure this value when
`autoScaling.compute.enabled` was `false`.  
  
providerSettings.autoScaling.compute

|

object

|

Conditional

|

Range of instance sizes to which your cluster can scale. Atlas requires this
parameter if **"autoScaling.compute.enabled" : true**.  
  
providerSettings.autoScaling.compute.minInstanceSize

|

string

|

Conditional

|

Minimum instance size to which your cluster can automatically scale (such as
**M10** ). Atlas requires this parameter if
**"autoScaling.compute.scaleDownEnabled" : true**.  
  
providerSettings.autoScaling.compute.maxInstanceSize

|

string

|

Conditional

|

Maximum instance size to which your cluster can automatically scale (such as
**M40** ). Atlas requires this parameter if **"autoScaling.compute.enabled" :
true**.  
  
providerSettings.backingProviderName

|

string

|

Conditional

|

Cloud service provider on which the server for a multi-tenant cluster is
provisioned.

This setting only works when **"providerSetting.providerName" : "TENANT"** and
**"providerSetting.instanceSizeName" : "M0"** , **"M2"** , or **"M5"**.

Atlas accepts the following values:

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
  
providerSettings.diskIOPS

|

number

|

Conditional

|

Disk IOPS setting for AWS storage. Set only if you selected AWS as your cloud
service provider.

Maximum input/output operations per second (IOPS) the cluster can perform. The
possible values depend on the selected **providerSettings.instanceSizeName**
and **diskSizeGB**.

This setting requires that **providerSettings.instanceSizeName** to be **M30**
or greater and cannot be used with clusters with local NVMe SSDs.

To view the possible range of IOPS values for the selected instance size and
storage capacity:

  1. Open the Atlas web console.

  2. Select Build a New Cluster.

  3. Under Cloud Provider & Region, select **AWS**.

  4. Under Cloud Provider & Region, select the region corresponding to your configured **providerSettings.regionName**.

  5. Under Cluster Tier, select the cluster tier corresponding to your configured **providerSettings.instanceSizeName**.

  6. Under Cluster Tier, set the Storage Capacity slider to your configured **diskSizeGB**. Alternatively, input the exact value of **diskSizeGB** in the input box to the right of the slider.

Click Provision IOPS to see the available IOPS range.

If you set the **diskIOPS** value to a value higher than the default value for
the selected volume size, Atlas automatically sets
**providerSettings.volumeType** to **PROVISIONED**. If you manually set
**diskIOPS** to the default value, you must specify
**providerSettings.volumeType** to be either **PROVISIONED** or **STANDARD**.

The default value for **providerSettings.diskIOPS** is the same as the cluster
tier's Standard IOPS value, as viewable in the Atlas console.

Changing this value affects the cost of running the cluster as described in
the billing documentation.

Atlas enforces the following minimum ratios for given cluster tiers. This
keeps cluster performance consistent with large datasets.

Instance sizes **M10** to **M40** have a ratio of disk capacity to system
memory of 60:1. Instance sizes greater than **M40** have a ratio of 120:1.

## Example

To support 3 TB (or 3,072 GB) of disk capacity, select a cluster tier with a
minimum of 32 GB of RAM. This would be **M50** or greater.  
  
providerSettings.diskTypeName

|

string

|

Conditional

|

Type of disk if you selected Azure as your cloud service provider.

Disk type of the server's root volume for Azure instances. If omitted, Atlas
uses the default disk type for the selected
`providerSettings.instanceSizeName`.

The following table lists the possible values for this field, and their
corresponding storage size.

|

`diskTypeName`

|

Storage Size  
  
|  
  
`P2` 1

|

8GB  
  
`P3` 2

|

16GB  
  
`P4` 3

|

32GB  
  
`P6` 4

|

64GB  
  
`P10`

|

128GB  
  
`P15`

|

256GB  
  
`P20`

|

512GB  
  
`P30`

|

1024GB  
  
`P40`

|

2048GB  
  
`P50`

|

4095GB  
  
1 Default for `M10` Azure clusters

2 Default for `M20` Azure clusters

3 Default for `M30` Azure clusters

4 Default for `M40+` Azure clusters  
  
providerSettings.encryptEBSVolume

|

boolean

|

Conditional

|

Flag that indicates whether the Amazon EBS encryption feature encrypts the
host's root volume for both data at rest within the volume and for data moving
between the volume and the cluster.

## Note

This setting is always enabled for clusters with local NVMe SSDs.

The default value is **true**.  
  
providerSettings.instanceSizeName

|

string

|

Required

|

Atlas provides different cluster tiers, each with a default storage capacity
and RAM size. The cluster you select is used for all the data-bearing servers
in your cluster.

## Tip

### See also:

Number of Nodes.

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

 **M0** , **M2** , and **M5** clusters are multi-tenant deployments. You must
set **providerSettings.providerName** to **TENANT** and specify the cloud
service provider in **providerSettings.backingProviderName**.  
  
providerSettings.providerName

|

string

|

Conditional

|

Cloud service provider on which Atlas provisions the hosts.

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
  
 **M0** , **M2** , and **M5** clusters are multi-tenant deployments. You must
set **providerSettings.providerName** to **TENANT** and specify the cloud
service provider in **providerSettings.backingProviderName**.  
  
providerSettings.regionName

|

string

|

Conditional

|

## Note

### Required if setting replicationSpecs array to empty

This parameter is _required_ if you have not set any values in the
**replicationSpecs** array.

Physical location of your MongoDB cluster. The region you choose can affect
network latency for clients accessing your databases.

Do _not_ specify this parameter when creating a multi-region cluster using the
**replicationSpec** document.

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

Select your cloud provider's tab for example cluster region names:

AWS

Azure

GCP

  * `US_EAST_1`

  * `US_WEST_2`

  * `EU_WEST_1`

For a complete list of supported AWS regions, see Amazon Web Services (AWS).  
  
providerSettings.volumeType

|

string

|

Conditional

|

Disk IOPS setting for AWS storage. Set only if you selected AWS as your cloud
service provider.

The API resource accepts **STANDARD** , the default, and **PROVISIONED**.

  *  **STANDARD** volume types can't exceed the default IOPS rate for the selected volume size.

  *  **PROVISIONED** volume types must fall within the allowable IOPS range for the selected volume size.

  
  
replicationFactor

|

number

|

Optional

|

## Important

### Use replicationSpecs

 **replicationFactor** is deprecated. Use **replicationSpecs**.

Number of replica set members. Each member keeps a copy of your databases,
providing high availability and data redundancy. Atlas accepts **3** , **5** ,
or **7**. The default value is **3**.

 _Don't_ specify this parameter when creating a multi-region cluster using the
**replicationSpec** object.

If your cluster is a sharded cluster, each shard is a replica set with the
specified replication factor.

Atlas ignores this value if you pass the **replicationSpec** object.  
  
replicationSpec

|

object

|

Optional

|

 _Deprecated_ : `replicationSpec` is deprecated. Use `replicationSpecs`.

Configuration of each region in a multi-region cluster. Each element in this
object represents a region where Atlas deploys your cluster.

For single-region clusters, you can either specify the
**providerSettings.regionName** and **replicationFactor** , _or_ you can use
the **replicationSpec** object to define a single region.

For multi-region clusters, omit the **providerSettings.regionName** parameter.

For Global Clusters, specify the **replicationSpecs** parameter rather than a
**replicationSpec** parameter.

## Important

If you use **replicationSpec** , you must specify a minimum of one
**replicationSpec. <region>** object.

Use the **replicationSpecs** parameter to modify a Global Cluster.

## Note

You cannot specify both the **replicationSpec** and **replicationSpecs**
parameters in the same request body.  
  
replicationSpec.<region>

|

object

|

Conditional

|

## Important

### Use replicationSpecs[n].<region>

 **replicationSpec. <region>** is deprecated. Use **replicationSpecs[n].
<region>**.

Physical location of the region. Replace **< region>** with the name of the
region. Each **< region>** object describes the region's priority in elections
and the number and type of MongoDB nodes Atlas deploys to the region.

## Important

If you use **replicationSpec** , you must specify a minimum of one
**replicationSpec. <region>** object.

Select your cloud service provider's tab for example cluster region names:

AWS

Azure

GCP

  * `US_EAST_1`

  * `US_WEST_2`

  * `EU_WEST_1`

For a complete list of supported AWS regions, see Amazon Web Services (AWS).

For each **< region>** object, you must specify the **analyticsNodes** ,
**electableNodes** , **priority** , and **readOnlyNodes** parameters.

## Tip

### See also:

Considerations.

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
  
replicationSpec.<region>.analyticsNodes

|

number

|

Optional

|

## Important

### Use replicationSpecs[n].<region>.analyticsNodes

 **replicationSpec. <region>.analyticsNodes** is deprecated. Use
**replicationSpecs[n]. <region>.analyticsNodes**.

Number of analytics nodes for Atlas to deploy to the region. Analytics nodes
are useful for handling analytic data such as reporting queries from BI
Connector for Atlas. Analytics nodes are read-only, and can never become the
primary.  
  
replicationSpec.<region>.electableNodes

|

number

|

Optional

|

## Important

### Use replicationSpecs[n].<region>.electableNodes

 **replicationSpec. <region>.electableNodes** is deprecated. Use
**replicationSpecs[n]. <region>.electableNodes**.

Number of electable nodes for Atlas to deploy to the region. Electable nodes
can become the primary and can facilitate local reads.

The total number of **electableNodes** across all **replicationSpec.
<region>** object must be **3** , **5** , or **7**.

Specify **0** if you do not want any electable nodes in the region.

You cannot create electable nodes if the **replicationSpec.
<region>.priority** is 0.  
  
replicationSpec.<region>.priority

|

number

|

Optional

|

## Important

### Use replicationSpecs[n].<region>.priority

 **replicationSpec. <region>.priority** is deprecated. Use
**replicationSpecs[n]. <region>.priority**.

Election priority of the region. For regions with only **replicationSpec.
<region>.readOnlyNodes**, set this value to **0**.

For regions where **replicationSpec. <region>.electableNodes** is at least
**1** , each **replicationSpec. <region>** must have a priority of exactly one
**(1)** less than the previous region. The first region **must** have a
priority of **7**. The lowest possible priority is **1**.

The priority **7** region identifies the **Preferred Region** of the cluster.
Atlas places the primary node in the **Preferred Region**. Priorities **1**
through **7** are exclusive: you can't assign a given priority to more than
one region per cluster.

## Example

If you have three regions, their priorities would be **7** , **6** , and **5**
respectively. If you added two more regions for supporting electable nodes,
the priorities of those regions would be **4** and **3** respectively.  
  
replicationSpec.<region>.readOnlyNodes

|

number

|

Optional

|

## Important

### Use replicationSpecs[n].<region>.readOnlyNodes

 **replicationSpec. <region>.readOnlyNodes** is deprecated. Use
**replicationSpecs[n]. <region>.readOnlyNodes**.

Number of read-only nodes for Atlas to deploy to the region. Read-only nodes
can never become the primary, but can facilitate local-reads.

Specify **0** if you do not want any read-only nodes in the region.  
  
replicationSpecs

|

array of objects

|

Conditional

|

Configuration for cluster regions.

## Note

### When should you use replicationSpecs?

|

Condition

|

Necessity

|

Values  
  
||  
  
You are deploying Global Clusters.

|

Required

|

Each object in the array represents a zone where Atlas deploys your cluster's
nodes.  
  
You are deploying non-Global replica sets and sharded clusters.

|

Optional

|

This array has one object representing where Atlas deploys your cluster's
nodes.  
  
You must specify all parameters in **replicationSpecs** object array.

## Tip

### What parameters depend on replicationSpecs?

If you set **replicationSpecs** , you must:

  * Set **clusterType**

  * Set **numShards**

  * Not set **replicationSpec**

  * Not use clusters with local NVMe SSDs

  * Not use Azure clusters

  
  
replicationSpecs[n].id

|

string

|

Conditional

|

Unique identifier of the replication object for a zone in a Global Cluster.
Must be exactly 24 hexadecimal digits in length.

|

Condition

|

Necessity  
  
|  
  
Existing zones included in a cluster modification request body.

|

Required  
  
Adding a new zone to an existing Global Cluster.

|

Optional  
  
## Warning

Atlas deletes any existing zones in a Global Cluster that are not included in
a cluster modification request.  
  
replicationSpecs[n].numShards

|

number

|

Required

|

Number of shards to deploy in each specified zone. The default value is **1**.  
  
replicationSpecs[n].regionsConfig

|

object

|

Optional

|

Configuration for a region. Each **regionsConfig** object describes the
region's priority in elections and the number and type of MongoDB nodes that
Atlas deploys to the region.

## Important

If you use **replicationSpecs** , you must specify a minimum of one
**replicationSpecs[n].regionsConfig. <region>** string.  
  
replicationSpecs[n].regionsConfig.<region>

|

object

|

Required

|

Physical location of the region. Replace **< region>** with the name of the
region. Each **< region>** object describes the region's priority in elections
and the number and type of MongoDB nodes Atlas deploys to the region.

Select your cloud service provider's tab for example cluster region names:

AWS

Azure

GCP

  * `US_EAST_1`

  * `US_WEST_2`

  * `EU_WEST_1`

For a complete list of supported AWS regions, see Amazon Web Services (AWS).

For each **< region>** object, you must specify the **analyticsNodes** ,
**electableNodes** , **priority** , and **readOnlyNodes** parameters.

## Tip

### See also:

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
  
replicationSpecs[n].regionsConfig.<region>.analyticsNodes

|

number

|

Optional

|

Number of analytics nodes for Atlas to deploy to the region. Analytics nodes
are useful for handling analytic data such as reporting queries from BI
Connector for Atlas. Analytics nodes are read-only, and can never become the
primary.  
  
replicationSpecs[n].regionsConfig.<region>.electableNodes

|

number

|

Optional

|

Number of electable nodes for Atlas to deploy to the region. Electable nodes
can become the primary and can facilitate local reads.

The total number of **electableNodes** across all
**replicationSpecs[n].regionsConfig. <region>** object must be **3** , **5** ,
or **7**.

Specify **0** if you do not want any electable nodes in the region.

You cannot create electable nodes if the **replicationSpecs[n].regionsConfig.
<region>.priority** is 0.  
  
replicationSpecs[n].regionsConfig.<region>.priority

|

number

|

Optional

|

Election priority of the region. For regions with only
**replicationSpecs[n].regionsConfig. <region>.readOnlyNodes**, set this value
to **0**.

For regions where **replicationSpecs[n].regionsConfig.
<region>.electableNodes** is at least **1** , each
**replicationSpecs[n].regionsConfig. <region>** must have a priority of
exactly one **(1)** less than the previous region. The first region **must**
have a priority of **7**. The lowest possible priority is **1**.

The priority **7** region identifies the **Preferred Region** of the cluster.
Atlas places the primary node in the **Preferred Region**. Priorities **1**
through **7** are exclusive: you can't assign a given priority to more than
one region per cluster.

## Example

If you have three regions, their priorities would be **7** , **6** , and **5**
respectively. If you added two more regions for supporting electable nodes,
the priorities of those regions would be **4** and **3** respectively.  
  
replicationSpecs[n].regionsConfig.<region>.readOnlyNodes

|

number

|

Optional

|

Number of read-only nodes for Atlas to deploy to the region. Read-only nodes
can never become the primary, but can facilitate local-reads.

Specify **0** if you do not want any read-only nodes in the region.  
  
replicationSpecs[n].zoneName

|

string

|

Optional

|

Name for the zone in a Global Cluster. Don't provide this value if
**clusterType** is not **GEOSHARDED**.  
  
rootCertType

|

string

|

Optional

|

## Important

### Feature unavailable in Free and Shared-Tier Clusters

This feature is not available for `M0` free clusters, `M2`, and `M5` clusters.
To learn more about which features are unavailable, see Atlas M0 (Free
Cluster), M2, and M5 Limitations.

Certificate Authority that MongoDB Atlas clusters use. You can specify
`ISRGROOTX1` (for ISRG Root X1).

## Note

Beginning on 1 May 2021, new TLS certificates that MongoDB Atlas creates use
ISRG instead of IdenTrust for their root Certificate Authority in line with
Let's Encrypt's announcement of this transition.  
  
versionReleaseSystem

|

string

|

Conditional

|

Release cadence that Atlas uses for this cluster. Atlas accepts:

  *  **CONTINUOUS** : Atlas automatically updates your cluster to the latest major and rapid MongoDB releases as they become available.

  *  **LTS** : Atlas automatically updates your cluster to subsequent patch releases of this MongoDB version. Atlas doesn't update your cluster to newer rapid or major MongoDB releases as they become available.

If you set this field to **CONTINUOUS** , you must omit the
**mongoDBMajorVersion** field.

You can change from **LTS** to **CONTINUOUS** only if your cluster runs the
most recent MongoDB major release.

You can change from **CONTINUOUS** to **LTS** only if the most recent MongoDB
release is a major version. For example, if the most recent MongoDB release is
5.0, you can switch from **CONTINUOUS** to **LTS**. If the most recent MongoDB
release is 5.1, you must wait until MongoDB 6.0 is released to switch from
**CONTINUOUS** to **LTS**.  
  
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

  * 4.0

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

Modify Single Region

Modify Multi-Region

Modify Global

    
    
    1| curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
    |  
    2|      --header "Content-Type: application/json" \  
    3|      --include \  
    4|      --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5356823b3794de37132bb7b/clusters/SingleRegionCluster" \  
    5|      --data '  
    6|        {  
    7|          "diskSizeGB": 320,  
    8|          "providerSettings": {  
    9|            "instanceSizeName": "M40",  
    10|            "providerName": "AWS"  
    11|          }  
    12|        }'  
  
## Example Response

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

Modify Single Region

Modify Multi-Region

Modify Global

    
    
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
    39|   "diskSizeGB":320,  
    40|   "encryptionAtRestProvider":"NONE",  
    41|   "groupId":"{GROUP-ID}",  
    42|   "id":"{CLUSTER-ID}",  
    43|   "labels":[  
    44|       
    45|   ],  
    46|   "mongoDBMajorVersion":"4.0",  
    47|   "mongoDBVersion":"4.0.13",  
    48|   "mongoURIUpdated":"2019-12-11T17:34:08Z",  
    49|   "name":"SingleRegionCluster",  
    50|   "numShards":1,  
    51|   "paused":false,  
    52|   "pitEnabled":false,  
    53|   "providerBackupEnabled":true,  
    54|   "providerSettings":{  
    55|     "providerName":"AWS",  
    56|     "autoScaling":{  
    57|       "compute":{  
    58|         "maxInstanceSize":null,  
    59|         "minInstanceSize":null  
    60|       }  
    61|     },  
    62|     "diskIOPS":2400,  
    63|     "encryptEBSVolume":true,  
    64|     "instanceSizeName":"M40",  
    65|     "regionName":"US_EAST_1",  
    66|     "volumeType":"STANDARD"  
    67|   },  
    68|   "replicationFactor":3,  
    69|   "replicationSpec":{  
    70|     "US_EAST_1":{  
    71|       "analyticsNodes":0,  
    72|       "electableNodes":3,  
    73|       "priority":7,  
    74|       "readOnlyNodes":0  
    75|     }  
    76|   },  
    77|   "replicationSpecs":[  
    78|     {  
    79|       "id":"{REPLICA-ID}",  
    80|       "numShards":1,  
    81|       "regionsConfig":{  
    82|         "US_EAST_1":{  
    83|           "analyticsNodes":0,  
    84|           "electableNodes":3,  
    85|           "priority":7,  
    86|           "readOnlyNodes":0  
    87|         }  
    88|       },  
    89|       "zoneName":"Zone 1"  
    90|     }  
    91|   ],  
    92|   "stateName":"UPDATING",  
    93|   "links":[]  
    94| }  
  
What is MongoDB Atlas? →

