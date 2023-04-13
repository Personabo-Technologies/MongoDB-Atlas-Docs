Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `AtlasDeployment` Custom Resource

Share Feedback

On this page

  * Examples
  * Status Example
  * Configuration Example
  * Advanced Options Example
  * Serverless Instance Example
  * Advanced Cluster Example
  * Multiple Cloud Service Providers Example
  * Parameters

The `AtlasDeployment` custom resource configures your MongoDB cluster or
serverless instance in Atlas. When you create the `AtlasDeployment` custom
resource, Atlas Kubernetes Operator tries to create or update a cluster or
serverless instance in Atlas.

## Important

### Custom Resources Definitions Take Priority

Atlas Kubernetes Operator uses custom resource configuration files to manage
your Atlas configuration. Each custom resource definition overrides settings
specified in other ways such as in the Atlas UI. If you delete a custom
resource, Atlas Kubernetes Operator deletes the object from Atlas unless you
use annotations to skip deletion. To learn more, see the Create and Update
Process and the Delete Process.

Atlas Kubernetes Operator does one of the following actions depending on the
values you specify in the `AtlasDeployment` custom resource:

  * If you specify values for fields under `spec.deploymentSpec`, Atlas Kubernetes Operator uses the Atlas Clusters API Resource and Advanced Clusters API Resource to create a new cluster or update an existing cluster.

  * If you specify values for fields under `spec.serverlessSpec`, Atlas Kubernetes Operator uses the Atlas Serverless Instance API Resource to create a new serverless instance or update an existing serverless instance.

Creating or updating a cluster or serverless instance can take up to 10
minutes. Atlas Kubernetes Operator monitors the update process.

You can run the following command to check on the status:

    
    
    kubectl get atlasdeployment -o yaml  
      
  
The following example shows the status section of a cluster that is
provisioning:

    
    
    status:  
      
      conditions:  
      - lastTransitionTime: "2021-03-18T16:32:43Z"  
        status: "False"  
        type: ClusterReady  
        reason: ClusterCreating  
        message: Cluster is provisioning  
  
The `ClusterReady` status will change to `True` when the cluster or serverless
instance is ready.

If you remove the `AtlasDeployment` resource from your Kubernetes cluster,
Atlas Kubernetes Operator removes the cluster or serverless instance from
Atlas.

## Examples

### Status Example

The following example shows the `AtlasDeployment` resource with a
`ClusterReady` status of `True`:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      namespace: default  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      deploymentSpec:  
        name: test-cluster  
        providerSettings:  
          instanceSizeName: M10  
          providerName: AWS  
          regionName: US_EAST_1  
        mongoDBMajorVersion: "4.4"  
    status:  
      conditions:  
      - lastTransitionTime: "2021-03-18T16:32:43Z"  
        status: "True"  
        type: Ready  
      - lastTransitionTime: "2021-03-18T16:32:43Z"  
        status: "True"  
        type: ClusterReady  
      connectionStrings:  
        standard: mongodb://test-cluster-shard-00-00.kpc8f.mongodb.net:27017,test-cluster-shard-00-01.kpc8f.mongodb.net:27017,test-cluster-shard-00-02.kpc8f.mongodb.net:27017/?ssl=true&authSource=admin&replicaSet=atlas-1gm1pv-shard-0  
        standardSrv: mongodb+srv://test-cluster.kpc8f.mongodb.net  
      mongoDBVersion: 4.4.4  
      mongoURIUpdated: "2021-03-12T12:21:41Z"  
      observedGeneration: 1  
      stateName: IDLE  
  
### Configuration Example

The following example shows an `AtlasDeployment` custom resource specification
configured for auto-scaling multi-region clusters:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
      name: test-cluster-name  
      namespace: mongodb-atlas-system  
    spec:  
      projectRef:  
        name: development  
      deploymentSpec:  
        autoScaling:  
          compute:  
            enabled: true  
            scaleDownEnabled: true  
        clusterType: REPLICASET  
        name: service-name  
        providerBackupEnabled: true  
        providerSettings:  
          autoScaling:  
            compute:  
              maxInstanceSize: M40  
              minInstanceSize: M30  
          instanceSizeName: M30  
          providerName: GCP  
        replicationSpecs:  
          - numShards: 1  
            regionsConfig:  
              EASTERN_US:  
                analyticsNodes: 0  
                electableNodes: 1  
                priority: 6  
                readOnlyNodes: 0  
              SOUTH_AMERICA_EAST_1:  
                analyticsNodes: 0  
                electableNodes: 2  
                priority: 7  
                readOnlyNodes: 0  
            zoneName: Zone 1  
  
### Advanced Options Example

The following example shows an `AtlasDeployment` custom resource specification
configured with advanced options.

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      deploymentSpec:  
        name: Test-cluster  
        providerSettings:  
          instanceSizeName: M10  
          providerName: AWS  
          regionName: US_EAST_1  
      processArgs:  
        javascriptEnabled: false  
  
### Serverless Instance Example

The following example shows an `AtlasDeployment` custom resource specification
configured for a serverless instance:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
    metadata:  
      name: test-cluster-name  
      namespace: mongodb-atlas-system  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: development  
      serverlessSpec:  
        name: serverless-instance  
        providerSettings:  
          providerName: AWS  
          regionName: US_EAST_1  
  
### Advanced Cluster Example

Advanced clusters can span regions and cloud service providers. To learn more,
see the Advanced Cluster Considerations.

## Note

While the Atlas Advanced Clusters API Resource send requests using the `v1.5`
Atlas API versions, the Atlas Kubernetes Operator `apiVersion` field uses
`v1`. In this case, `v1` refers to the version of the Kubernetes API.

The following example shows an advanced `AtlasDeployment` custom resource
specification configured for multi-region clusters:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      advancedDeploymentSpec:  
        clusterType: REPLICASET  
        name: tenantCluster  
        replicationSpecs:  
          - regionConfigs:  
            - electableSpecs:  
                instanceSize: M5  
              providerName: AWS  
              regionName: US_EAST_1  
  
### Multiple Cloud Service Providers Example

The following example shows an advanced `AtlasDeployment` custom resource
specification configured to span multiple cloud service providers:

    
    
    apiVersion: atlas.mongodb.com/v1  
      
    kind: AtlasDeployment  
    metadata:  
      name: my-atlas-cluster  
      labels:  
        app.kubernetes.io/version: 1.6.0  
    spec:  
      projectRef:  
        name: my-project  
      advancedDeploymentSpec:  
        clusterType: REPLICASET  
        name: tenantCluster  
        replicationSpecs:  
          - regionConfigs:  
            - electableSpecs:  
                instanceSize: M10  
                nodeCount: 3  
              providerName: AWS  
              regionName: US_EAST_1  
              priority: 7  
            - electableSpecs:  
                instanceSize: M10  
                nodeCount: 2  
              providerName: AZURE  
              regionName: US_EAST_2  
              priority: 6  
            - electableSpecs:  
                instanceSize: M10  
                nodeCount: 2  
              providerName: GCP  
              regionName: CENTRAL_US  
              priority: 5  
  
## Parameters

This section describes some of the key `AtlasDeployment` custom resource
parameters available. For a full list of available parameters for clusters,
see the Atlas Clusters API and Atlas Advanced Clusters API. For a full list of
available parameters for serverless instances, see the Atlas Serverless
Instances API.

Refer to these descriptions, the available examples, and the API documentation
to customize your specifications.

`spec.advancedDeploymentSpec`

    

 _Type_ : array

 _Conditional_

List that contains the advanced cluster parameters from the API. For a full
list of available parameters, see the Atlas Advanced Clusters API.

## Important

You must specify `spec.deploymentSpec`, `spec.advancedDeploymentSpec`, or
`spec.serverlessSpec` in your configuration.

`spec.advancedDeploymentSpec.customZoneMapping`

    

 _Type_ : array

 _Required_

List that contains Global Cluster parameters that map zones to geographic
regions. For a full list of available parameters, see the Atlas Global
Clusters API.

`spec.advancedDeploymentSpec.customZoneMapping.location`

    

 _Type_ : string

 _Required_

Code that represents a location that maps to a zone in your Global Cluster.

`spec.advancedDeploymentSpec.customZoneMapping.zone`

    

 _Type_ : string

 _Required_

Human-readable label that identifies the zone in your Global Cluster.

`spec.advancedDeploymentSpec.diskSizeGB`

    

 _Type_ : number

 _Optional_

Capacity, in gigabytes, that indicates the host's root volume. Increase this
number to add capacity, up to a maximum possible value of `4096` (i.e., 4 TB).
You must specify a positive number for this value.

You can't set this value with clusters with local NVMe SSDs.

## Note

If you have autoscaling enabled for `diskGB` in any region, you can't edit
this option. To learn more, see
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.diskGB.enabled`.

The minimum disk size for dedicated clusters is 10 GB for AWS and Google
Cloud. If you specify this setting with a lower disk size, Atlas defaults to
the minimum disk size value.

If your database deployment includes Azure nodes, this value must correspond
to an existing Azure disk type (8, 16, 32, 64, 128, 256, 512, 1024, 2048, or
4096).

Atlas calculates storage charges differently depending on whether you choose
the default value or a custom value.

Atlas has disk capacity limits on single replica sets, scaling up to 4 TB for
higher cluster tiers. To expand the total cluster storage beyond default
limits, you can enable extended storage in the Project Settings. To
accommodate further scaling in the future, we recommend that you enable
sharding for long-term expansion.

If your database deployment spans cloud service providers, this value defaults
to the minimum default of the providers involved.

To learn more, see Storage Capacity.

`spec.advancedDeploymentSpec.managedNamespaces`

    

 _Type_ : array

 _Required_

List that contains information to create a managed namespace in a specified
Global Cluster to create. For a full list of available parameters, see the
Atlas Global Clusters API.

`spec.advancedDeploymentSpec.managedNamespaces.collection`

    

 _Type_ : string

 _Required_

Human-readable label of the collection to manage in this Global Cluster.

`spec.advancedDeploymentSpec.managedNamespaces.db`

    

 _Type_ : string

 _Required_

Human-readable label of the database to manage in this Global Cluster.

`spec.advancedDeploymentSpec.managedNamespaces.isCustomShardKeyHashed`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether to hash the custom shard key for the specified
collection. This parameter defaults to `false`.

  * Set to `true` to enable a custom shard key for the collection.

  * Set to `false` to disable a custom shard key for the collection. If diabled, MongoDB uses ranged sharding.

To learn more, see Hashed Shard Keys.

`spec.advancedDeploymentSpec.managedNamespaces.isCustomShardKeyUnique`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether the custom shard key for the specified collection
is unique. This parameter defaults to `false`.

  * Set to `true` to enable a unique custom shard key for the collection.

  * Set to `false` to disable a unique custom shard key for the collection.

`spec.advancedDeploymentSpec.managedNamespaces.numInitialChunks`

    

 _Type_ : integer

 _Optional_

Minimum number of chunks to initially create when sharding an empty collection
with a hashed shard key.

To learn more, see Shard a Global Collection.

`spec.advancedDeploymentSpec.managedNamespaces.presplitHashedZones`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether MongoDB Cloud should create and distribute initial
chunks for an empty or non-existing collection. This parameter defaults to
`false`.

  * Set to `true` to have MongoDB Cloud create and distribute initial chunks for an empty or non-existing collection.

  * Set to `false` to not have MongoDB Cloud create and distribute initial chunks for an empty or non-existing collection..

`spec.advancedDeploymentSpec.pitEnabled`

    

 _Type_ : boolean

 _Conditional_

Configuration that enables continuous cloud backup for advanced clusters. To
enable continuous cloud backup, you must specify this setting with a value of
`true`. For standard clusters see `spec.deploymentSpec.pitEnabled`.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs`

    

 _Type_ : array

 _Required_

Hardware specifications for nodes set for a given region. Each `regionConfigs`
object describes the region's priority in elections and the number and type of
MongoDB nodes that Atlas deploys to the region.

Each `regionConfigs` object must have either an `analyticsSpecs` object,
`electableSpecs` object, or `readOnlySpecs` object.

  * `M0`, `M2`, or `M5` clusters require only ``electableSpecs`.

  * Dedicated clusters can specify any of these specifications, but must have at least one `electableSpecs` object within a `replicationSpec`.

  * Every hardware specification must use the same `instanceSize`.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.analyticsSpecs`

    

 _Type_ : object

 _Optional_

Hardware specifications for analytics nodes needed in the region. Analytics
nodes handle analytic data such as reporting queries from BI Connector for
Atlas. Analytics nodes are read-only and can never become the primary.

If you don't specify this parameter, Atlas deploys no analytics to this
region.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.diskGB.enabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether this database deployment enables disk auto-
scaling. This parameter defaults to `true`.

  * Set to `true` to enable disk auto-scaling.

  * Set to `false` to disable disk auto-scaling.

The maximum amount of RAM for the selected cluster tier and the oplog size can
limit storage auto-scaling. To learn more, see Customize Your Storage.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.enabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether instance size auto-scaling is enabled. This
parameter defaults to `false`.

  * Set to `true` to enable instance size auto-scaling. If enabled, you must specify a value for `spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.maxInstanceSize`.

  * Set to `false` to disable instance size auto-scaling.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.maxInstanceSize`

    

 _Type_ : string

 _Conditional_

String that indicates the maximum instance size to which your database
deployment can automatically scale (such as `M40`). You must specify this
parameter if you set
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.enabled`
to `true`.

## Note

If you set a maximum instance size smaller than the database deployment's
current instance size with autoscaling enabled, Atlas automatically scales the
current instance size to the maximum value you specify.

For example, if the database deployment's current instance size is `M40` and
you set the maximum instance size to `M30`, Atlas automatically scales the
current instance size to `M30`.

If Atlas changes the current instance size and you don't change the
`spec.deploymentSpec.providerSettings.instanceSizeName` in Atlas Kubernetes
Operator to match the new instance size, Atlas Kubernetes Operator displays a
warning in the logs but doesn't prevent autoscaling.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.minInstanceSize`

    

 _Type_ : string

 _Conditional_

String that indicates the minimum instance size to which your database
deployment can automatically scale (such as `M10`). You must specify this
parameter if you set
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.enabled`
to `true`.

## Note

If you set a minimum instance size larger than the database deployment's
current instance size with autoscaling enabled, Atlas automatically scales the
current instance size to the minimum value you specify.

For example, if the database deployment's current instance size is `M10` and
you set the minimum instance size to `M30`, Atlas automatically scales the
current instance size to `M30`.

If Atlas changes the current instance size and you don't change the
`spec.deploymentSpec.providerSettings.instanceSizeName` in Atlas Kubernetes
Operator to match the new instance size, Atlas Kubernetes Operator displays a
warning in the logs but doesn't prevent autoscaling.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.electableSpecs`

    

 _Type_ : object

 _Optional_

Hardware specifications for electable nodes in the region. Electable nodes can
become the primary and can enable local reads.

If you don't specify this option, Atlas deploys no electable nodes to the
region.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.electableSpecs.instanceSize`

    

 _Type_ : string

 _Conditional_

Hardware specification for the instance sizes in this region. Each instance
size has a default storage and memory capacity. The instance size you select
applies to all the data-bearing hosts in your instance size. To learn more,
see the AWS, GCP, and Azure custom storage sizes.

If you deploy a sharded cluster, or global cluster, you must choose an
instance size of `M30` or greater.

## Note

If you have autoscaling enabled for the compute field, you can't edit this
option. To learn more, see
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.enabled`.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.electableSpecs.nodeCount`

    

 _Type_ : integer

 _Conditional_

Number of electable nodes for Atlas to deploy to the region. Electable nodes
can become the primary and can enable local reads.

The combined `electableSpecs.nodeCount` across all
`replicationSpecs.regionConfigs` objects must total `3`, `5`, or `7`.

You can't create electable nodes if
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.priority` is `0`.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.priority`

    

 _Type_ : integer

 _Required_

Precedence is given to this region when a primary election occurs.

If your `regionConfigs` has only `readOnlySpecs`, `analyticsSpecs`, or both,
set this value to `0`.

If you have multiple `regionConfigs` objects (your cluster is multi-region or
multi-cloud), they must have priorities in descending order. The highest
priority is `7`.

## Example

Set your highest priority region to `7`, your second-highest priority to `6`,
and your third-priority region to `5`. If you have no electable nodes, set
this value to `0`.

If your region has set `electableSpecs.nodeCount` to `1` or higher, it must
have a priority of exactly one less than another region in the
`replicationSpecs.regionConfigs` array unless it is the primary. The highest-
priority region **must** have a priority of `7`. The lowest possible priority
is `1`.

The priority `7` region identifies the **Preferred Region** of the cluster.
Atlas places the primary node in the **Preferred Region**. Priorities `1`
through `7` are exclusive: you can't assign a given priority to more than one
region per cluster.

## Example

If you have three regions, their priorities would be `7`, `6`, and `5`
respectively. If you added two more regions for supporting electable nodes,
the priorities of those regions would be `4` and `3` respectively.

`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.readOnlySpecs`

    

 _Type_ : object

 _Optional_

Hardware specifications for read-only nodes in the region. Read-only nodes can
never become the primary member, but can enable local reads.

If you don't specify this parameter, Atlas deploys no read-only nodes to the
region.

`spec.backupRef`

    

 _Type_ : object

 _Optional_

List that contains the details for the `AtlasBackupSchedule` Custom Resource
that you want to apply. You can specify one backup schedule per cluster.

`spec.backupRef.name`

    

 _Type_ : string

 _Optional_

`metadata.name` value within the `AtlasBackupSchedule` Custom Resource for the
backup schedule that you want to apply. You can specify only one backup
schedule per cluster, but you can use the same backup schedule for multiple
clusters.

If you don't specify this parameter, Atlas doesn't apply your backup
configuration to this cluster.

`spec.backupRef.namespace`

    

 _Type_ : string

 _Optional_

String that indicates the namespace that contains the `AtlasBackupSchedule`
Custom Resource for the backup schedule that you want to apply.

`spec.deploymentSpec`

    

 _Type_ : array

 _Conditional_

List that contains the cluster parameters from the API. For a full list of
available parameters, see the Atlas Clusters API.

## Important

You must specify `spec.deploymentSpec`, `spec.advancedDeploymentSpec`, or
`spec.serverlessSpec` in your configuration.

`spec.deploymentSpec.clusterType`

    

 _Type_ : string

 _Conditional_

Human-readable label that identifies cluster type to create.

 **When should you use this parameter?**

Condition

|

Necessity  
  
|  
  
You set `spec.deploymentSpec.replicationSpecs`.

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
  
`spec.deploymentSpec.customZoneMapping`

    

 _Type_ : array

 _Required_

List that contains Global Cluster parameters that map zones to geographic
regions. For a full list of available parameters, see the Atlas Global
Clusters API.

`spec.deploymentSpec.customZoneMapping.location`

    

 _Type_ : string

 _Required_

Code that represents a location that maps to a zone in your Global Cluster.

`spec.deploymentSpec.customZoneMapping.zone`

    

 _Type_ : string

 _Required_

Human-readable label that identifies the zone in your Global Cluster.

`spec.deploymentSpec.encryptionAtRestProvider`

    

 _Type_ : string

 _Optional_

Cloud service provider that manages the customer key for this cluster. You
must set this value to enable encryption at rest using customer-managed keys
for this cluster, which provides an additional layer of encryption.

To learn more, see Encrypt Data Using a Key Management Service.

Atlas accepts the following values:

Value

|

Cloud Provider  
  
|  
  
AWS

|

Amazon AWS  
  
GCP

|

Google Cloud  
  
AZURE

|

Microsoft Azure  
  
NONE

|

No provider; the cluster doesn't encrypt data using customer-managed keys.  
  
`spec.deploymentSpec.managedNamespaces`

    

 _Type_ : array

 _Required_

List that contains information to create a managed namespace in a specified
Global Cluster to create. For a full list of available parameters, see the
Atlas Global Clusters API.

`spec.deploymentSpec.managedNamespaces.collection`

    

 _Type_ : string

 _Required_

Human-readable label of the collection to manage in this Global Cluster.

`spec.deploymentSpec.managedNamespaces.db`

    

 _Type_ : string

 _Required_

Human-readable label of the database to manage in this Global Cluster.

`spec.deploymentSpec.managedNamespaces.isCustomShardKeyHashed`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether to hash the custom shard key for the specified
collection. This parameter defaults to `false`.

  * Set to `true` to enable a custom shard key for the collection.

  * Set to `false` to disable a custom shard key for the collection. If diabled, MongoDB uses ranged sharding.

To learn more, see Hashed Shard Keys.

`spec.deploymentSpec.managedNamespaces.isCustomShardKeyUnique`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether the custom shard key for the specified collection
is unique. This parameter defaults to `false`.

  * Set to `true` to enable a unique custom shard key for the collection.

  * Set to `false` to disable a unique custom shard key for the collection.

`spec.deploymentSpec.managedNamespaces.numInitialChunks`

    

 _Type_ : integer

 _Optional_

Minimum number of chunks to initially create when sharding an empty collection
with a hashed shard key.

To learn more, see Shard a Global Collection.

`spec.deploymentSpec.managedNamespaces.presplitHashedZones`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether MongoDB Cloud should create and distribute initial
chunks for an empty or non-existing collection. This parameter defaults to
`false`.

  * Set to `true` to have MongoDB Cloud create and distribute initial chunks for an empty or non-existing collection.

  * Set to `false` to not have MongoDB Cloud create and distribute initial chunks for an empty or non-existing collection..

`spec.deploymentSpec.mongoDBMajorVersion`

    

 _Type_ : string

 _Optional_

Version of the cluster to deploy. Atlas supports the following MongoDB
versions for `M10+` clusters:

  * 4.2

  * 4.4

  * 5.0

The following conditions produce the following results:

Condition

|

Result  
  
|  
  
You omit this parameter and you omit the
`spec.deploymentSpec.versionReleaseSystem` parameter.

|

Atlas deploys a cluster that runs MongoDB 5.0.  
  
You omit this parameter and you set the
`spec.deploymentSpec.versionReleaseSystem` parameter to `LTS`.

|

Atlas deploys a cluster that runs MongoDB 5.0.  
  
You set the `spec.deploymentSpec.providerSettings.instanceSizeName` parameter
to `M0`, `M2`, or `M5`.

|

You must deploy MongoDB 5.0.  
  
You specify this parameter.

|

Atlas always deploys the cluster with the latest stable patch release of the
specified version.  
  
You set the `spec.deploymentSpec.versionReleaseSystem` parameter to
`CONTINUOUS`.

|

You must omit this parameter.  
  
`spec.deploymentSpec.pitEnabled`

    

 _Type_ : boolean

 _Conditional_

Configuration that enables continuous cloud backup. To enable continuous cloud
backup, you must specify this setting with a value of `true`. For advanced
clusters see `spec.advancedDeploymentSpec.pitEnabled`.

`spec.deploymentSpec.providerSettings`

    

 _Type_ : Object

 _Conditional_

Configuration that specifies the settings for the provisioned hosts on which
MongoDB runs. The available options are specific to the cloud service
provider. To learn more, see the AWS, GCP, and Azure cluster configuration
options.

If you want to create or update a cluster, you must specify this setting.

`spec.deploymentSpec.providerSettings.providerName`

    

 _Type_ : string

 _Conditional_

Cloud service provider on which Atlas provisions the hosts.

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
  
`spec.deploymentSpec.providerSettings.instanceSizeName`

    

 _Type_ : string

 _Required_

Atlas provides different cluster tiers, each with a default storage capacity
and RAM size. The cluster you select is used for all the data-bearing servers
in your cluster. To learn more, see the AWS, GCP, and Azure custom storage
sizes.

If you change the instance size name after you deploy your cluster, Atlas
changes the database deployment to the instance size you specify unless it
falls outside the range you specify in
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.minInstanceSize`
and
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.maxInstanceSize`
with autoscaling enabled. To learn more, see
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.minInstanceSize`
and
`spec.advancedDeploymentSpec.replicationSpecs.regionConfigs.autoScaling.compute.maxInstanceSize`.

## Note

You can change this setting to upgrade an `M0`, `M2`, or `M5` cluster to an
`M10+` cluster. However, you can't upgrade an `M0`, `M2`, or `M5` cluster to
another free or shared cluster. For example, you can't upgrade an `M0` cluster
to an `M5` cluster.

`spec.deploymentSpec.providerSettings.regionName`

    

 _Type_ : string

 _Conditional_

Physical location of your MongoDB cluster. The region you choose can affect
network latency for clients accessing your databases.

For a complete list of region name values, refer to the cloud provider
reference pages:

  * AWS

  * GCP

  * Azure

For multi-region clusters, see `spec.deploymentSpec.replicationSpecs`. You
must set either `spec.deploymentSpec.providerSettings.regionName` or
`spec.deploymentSpec.replicationSpecs`.

`spec.deploymentSpec.replicationSpecs`

    

 _Type_ : array of objects

 _Conditional_

List that contains the configurations for your cluster regions. Use this
parameter for multi-region clusters. You must set either
`spec.deploymentSpec.providerSettings.regionName` or
`spec.deploymentSpec.replicationSpecs`.

 **When should you use this parameter?**

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
  
If you specify this parameter, you must also specify
`spec.deploymentSpec.clusterType` and
`spec.deploymentSpec.replicationSpecs.numShards`.

`spec.deploymentSpec.replicationSpecs.numShards`

    

 _Type_ : integer

 _Conditional_

Positive integer that specifies the number of shards to deploy for a sharded
cluster.

If you use the `spec.deploymentSpec.replicationSpecs` parameter, you must set
this parameter.

Atlas accepts `1` through `50`, inclusive. The default value is `1`.

  * If you specify a value of `1` and you set `spec.deploymentSpec.clusterType` to `SHARDED`, Atlas deploys a single-shard sharded cluster.

  * If you specify `1` and you set `spec.deploymentSpec.clusterType` to `REPLICASET`, Atlas deploys a replica set.

Don't create a sharded cluster with a single shard for production
environments. Single-shard sharded clusters don't provide the same benefits as
multi-shard configurations.

## Tip

### See also:

    * Sharding

    * Number of Nodes

`spec.deploymentSpec.replicationSpecs.zoneName`

    

 _Type_ : string

 _Optional_

Human-readable label that identifies the zone in a Global Cluster. Provide
this value only if you set `spec.deploymentSpec.clusterType` to `GEOSHARDED`.

`spec.deploymentSpec.versionReleaseSystem`

    

 _Type_ : string

 _Conditional_

Release cadence that Atlas uses for this cluster. Atlas accepts:

  * `CONTINUOUS`: Atlas creates your cluster using the most recent MongoDB release. Atlas automatically updates your cluster to the latest major and rapid MongoDB releases as they become available.

  * `LTS`: Atlas creates your cluster using the latest patch release of the MongoDB version that you specify in the `spec.deploymentSpec.mongoDBMajorVersion` parameter. Atlas automatically updates your cluster to subsequent patch releases of this MongoDB version. Atlas doesn't update your cluster to newer rapid or major MongoDB releases as they become available.

If omitted, defaults to `LTS`.

If you set this parameter to `CONTINUOUS`, you must omit the
`spec.deploymentSpec.mongoDBMajorVersion` parameter.

`spec.processArgs`

    

 _Type_ : object

 _Optional_

Object that contains the advanced configuration options for your cluster.

`spec.processArgs.defaultReadConcern`

    

 _Type_ : string

 _Optional_

String that indicates the default level of acknowledgment requested from
MongoDB for read operations set for this cluster.

MongoDB 4.4 clusters default to available.

MongoDB 5.0 clusters default to local /reference/read-concern-local.

`spec.processArgs.defaultWriteConcern`

    

 _Type_ : string

 _Optional_

String that indicates the default level of acknowledgment requested from
MongoDB for write operations set for this cluster.

MongoDB 4.4 clusters default to 1.

MongoDB 5.0 clusters default to majority.

`spec.processArgs.failIndexKeyTooLong`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether to fail the operation and return an error when you
insert or update documents where all indexed entries exceed 1024 bytes. If you
set this to `false`, `mongod` writes documents that exceed this limit, but
_doesn't_ index them.

This option corresponds to the `failIndexKeyTooLong` `mongod` parameter.

`spec.processArgs.javascriptEnabled`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether the cluster allows execution of operations that
perform server-side executions of JavaScript.

  * If your cluster runs a MongoDB version less than 4.4, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` in the cluster.

  * If your cluster runs MongoDB version 4.4 or greater, this option corresponds to modifying the `security.javascriptEnabled` configuration file option for each `mongod` and `mongos` in the cluster.

`spec.processArgs.minimumEnabledTlsProtocol`

    

 _Type_ : integer

 _Optional_

String that indicates the minimum TLS version that the cluster accepts for
incoming connections. Clusters using TLS 1.0 or 1.1 should consider setting
TLS 1.2 as the minimum TLS protocol version.

To learn more, see What versions of TLS does Atlas support?.

This option corresponds to the `net.ssl.disabledProtocols` `mongod`
configuration file option.

`spec.processArgs.noTableScan`

    

 _Type_ : boolean

 _Optional_

Flag that indicates whether the cluster disables executing any query that
requires a collection scan to return results.

This option corresponds to the `notablescan` `mongod` parameter.

`spec.processArgs.oplogSizeMB`

    

 _Type_ : integer

 _Optional_

Number that indicates the storage limit of a cluster's oplog expressed in
megabytes. A value of `null` indicates that the cluster uses the default oplog
size that Atlas calculates.

This option corresponds to the `replication.oplogSizeMB` `mongod`
configuration file option.

`spec.processArgs.sampleRefreshIntervalBIConnector`

    

 _Type_ : integer

 _Optional_

Number that indicates the documents per database to sample when gathering
schema information.

This parameter corresponds to the sampleSize mongosqld option.

`spec.processArgs.sampleSizeBIConnector`

    

 _Type_ : integer

 _Optional_

Number that indicates the interval in seconds at which the mongosqld process
re-samples data to create its relational schema.

This parameter corresponds to the sampleRefreshIntervalSecs mongosqld option.

`spec.projectRef.name`

    

 _Type_ : string

 _Required_

Name of the project where the cluster belongs. You must specify an existing
`AtlasProject` Custom Resource.

`spec.serverlessSpec`

    

 _Type_ : array

 _Conditional_

List that contains the serverless instance parameters from the API. For a full
list of available parameters, see the Atlas Serverless Instances API.

## Important

You must specify `spec.deploymentSpec`, `spec.advancedDeploymentSpec`, or
`spec.serverlessSpec` in your configuration.

`spec.serverlessSpec.privateEndpoints`

    

 _Type_ : array

 _Optional_

List that contains the private endpoint configurations for the serverless
instance.

`spec.serverlessSpec.providerSettings`

    

 _Type_ : Object

 _Conditional_

Configuration that specifies the settings for the provisioned hosts on which
MongoDB runs. The available options are specific to the cloud service
provider. To learn more, see the AWS, GCP, and Azure serverless instance
configuration options.

If you want to create or update a serverless instance, you must specify this
setting.

`spec.serverlessSpec.providerSettings.providerName`

    

 _Type_ : string

 _Conditional_

Cloud service provider on which Atlas provisions the host for a serverless
instance.

Atlas accepts the following values:

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
  
`spec.serverlessSpec.providerSettings.regionName`

    

 **Type** : string

 **Conditional**

Physical location of your MongoDB serverless instance. The region you choose
can affect network latency for clients accessing your databases.

For a complete list of region name values, refer to the cloud provider
reference pages:

  * AWS

  * GCP

  * Azure

`status.connectionStrings`

    

 _Type_ : array

 _Required_

List that contains the connection URLs for accessing the cluster. This
parameter appears after you create or update a cluster.

## Note

You can't use a connection URL directly. Atlas clusters require
authentication. You must create at least one `AtlasDatabaseUser` Custom
Resource before the application in your Kubernetes cluster can connect to the
Atlas cluster. Atlas Kubernetes Operator creates a special secret for each
cluster and database user combination in the project. The application in your
Kubernetes cluster can use this secret to connect to the Atlas cluster. The
`spec.scopes` parameter in the `AtlasDatabaseUser` custom resource restricts
the clusters that create the database user.

For the configuration parameters available for a cluster and advanced cluster
from the API, see the Atlas Clusters API, and Advanced Clusters API.

## Note

The following parameters are deprecated in the Atlas API and Atlas Kubernetes
Operator does not support them:

  * `replicationSpec`

  * `replicationFactor`

← `AtlasProject` Custom Resource`AtlasDatabaseUser` Custom Resource →

