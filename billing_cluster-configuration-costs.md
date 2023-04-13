Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Cluster Configuration Costs

Share Feedback

On this page

  * Cloud Service Provider and Region
  * Cluster Tier
  * Backup
  * BI Connector for Atlas
  * Number of Nodes

## Cloud Service Provider and Region

Atlas supports deploying clusters onto Amazon Web Services, the Google Cloud
Platform, and Microsoft Azure. The choice of cloud service provider and region
or regions for the Atlas project affects the cost of running a Atlas cluster.

Multi-region cluster costs depend on the number of and location of additional
regions selected. When creating a cluster, Atlas displays the cluster tier
cost based on only the Preferred Region of the cluster. You can see the total
cost of running the cluster in the Cluster Overview.

To learn more about configuring your cloud provider and region, see Cloud
Providers and Regions.

## Cluster Tier

Atlas provides different cluster tiers. Each cluster tier has a default RAM
capacity, storage capacity, and maximum storage speed. The cluster's per-hour
charge includes these default values. Atlas uses the selected cluster when
deploying all the data-bearing [1] servers in your cluster.

Depending on the choice of cloud service provider, Atlas provides
customization options for cluster storage capacity and the speed of that
storage. If you add capacity or speed, you incur additional costs on top of
the base cost. For multi-region clusters, the per-cluster cost, including any
selected customizations, is relative to the Preferred Region. The Cluster
Overview box shows your overall charges.

### Storage Capacity

Atlas charges for storage capacity differently depending on whether you use
the cluster default or specify a custom storage capacity.

  * If you use the default storage capacity, Atlas includes its cost in the cluster's per-hour cost.

  * If you customize the amount of storage capacity, Atlas charges for the full amount of storage. Atlas doesn't deduct the cost of the default storage capacity. This change can be a disk upgrade or a instance family change such as changing from general CPU to low-CPU.

## Example

A new `M10` cluster defaults to 10 GB of storage. You can increase this amount
up to 120 GB of storage using this cluster tier.

If you increase the storage capacity to 50 GB, your monthly Atlas cost
includes 50 GB of storage, not the cost of the additional 40 GB.

## Note

Increasing storage capacity can change the maximum IOPS available with each
Custom Storage Speed.

### Custom Storage Speed

Atlas measures storage speed as maximum IOPS. Each Atlas cluster tier offers a
default storage speed that is included in the cluster's per-hour cost. The
choice of cloud service provider and cluster affects the available storage
speed customization options, as well as the cost of selecting a custom storage
speed.

AWS

Azure

GCP

For most cluster types, you can increase storage speed from Standard to Fast
or Fastest, which affects costs. Selecting a custom speed changes both IOPS
and the type of storage used. The storage type changes from a general-purpose
SSD to a provisioned-IOPS SSD. To learn more about storage types, see Amazon
EBS Volume Types.

### Cluster Auto-Scaling

To help minimize cluster costs while retaining the flexibility to easily scale
your cluster, you can enable Cluster Auto-Scaling. With auto-scaling, your
cluster automatically scales its tier, storage capacity, or both in response
to cluster usage. Auto-scaling reduces the need to manually optimize your
cluster to adapt to your current workload.

## Backup

The Atlas Back Up, Restore, and Archive Data supports Legacy Backups
(Deprecated) and Back Up Your Database Deployment. Each backup method has its
own cost calculations and considerations.

Atlas charges for each replica set in a cluster.

  * For a replica set deployment, the backup costs are the cost to backup data for the replica set.

  * For a sharded cluster deployment, Atlas sums the cost to backup the data for each shard replica set _and_ the config server replica set.

Atlas charges for the network transfer costs of restoring a snapshot. To learn
how Atlas charges for network data, see Data Transfer.

### Legacy Backups

The backup cost for legacy backups is calculated per GB per month. The monthly
rate is annualized and then divided by 365 to arrive at a Daily Backup Rate
per GB. The first 1 GB of backup data is free.

Monthly backup costs are primarily based on the size per-gigabyte of the data
to back up. This size is roughly equivalent to the uncompressed size of all
documents and all indexes for all the databases backed up.

To retrieve the size in gigabyte of the documents and indexes for a given
database, you can issue the db.stats() method and sum the `dataSize` and
`indexSize` fields.

    
    
    db.stats(1024*1024*1024).dataSize + db.stats(1024*1024*1024).indexSize  
      
  
The rate is based on your having 28 snapshots at steady state:

  * The six-hour snapshots are kept for two days;

  * The daily snapshots for one week,

  * The weekly snapshots for one month,

  * The monthly for one year.

Adding that up, you get 8 + 5 + 3 + 12 = 28 snapshots. We adjust the backup
rate daily based on the following formula:

    
    
    backupRatePerMonth = $1.25 + snapshotAtSteadyState/28 × $1.25  
      
  
Changing the snapshot frequency or retention period affects the base rate per
GB. See Snapshot Schedule for more information.

## Example

  * For a three-member replica set with 30GB of data, Atlas charges US$72.50 each month (using the default backup rate).

`(30 GB - 1 GB) × US$2.50 = US$72.50`

  * A sharded cluster with 3 shards contains 90GB of data, with each shard containing 30GB of data each. The config server replica set contains 5GB of data.

For this sharded cluster, Atlas charges US$227.50 per month (using the default
backup rate).

`((30 GB - 1 GB) × US$2.50) × 3) + ((5 GB - 1 GB) × US$2.50) = US$227.50`

### Cloud Backups

## Important

If you enabled Continuous Cloud Backups, Atlas bills you using the rates given
for Continuous Cloud Backups.

Atlas takes 31 snapshots for Cloud Backup each month by default. You can
change the backup policy if needed. In most cases, a new snapshot saves only
the data that changed after your most recent snapshot.

Atlas takes one snapshot per shard. It takes the first snapshot in full and
takes incremental snapshots afterward. Atlas can take more than one full
snapshot per shard in certain cases. These cases include when:

  * Snapshot taken on a different node from the previous one due to failover.

  * Storage volume of a node changes.

  * Region priority changes for a multi-region cluster. This would set a different node as the one that creates snapshots. If Atlas deems the selected node as unhealthy, it tries to snapshot the next node that it favors.

The backup cost for Cloud Backups is calculated per GB per month. Rates vary
between cloud providers and between regions within a given cloud provider.

Cloud Provider

|

Cost per GB  
  
|  
  
AWS

|

$0.14 to $0.19  
  
Azure

|

$0.34 to $0.65  
  
Google Cloud

|

$0.08 to $0.12  
  
Atlas can bill backup as high as the total storage capacity of the volume.
This depends upon how the cloud provider stores the volume snapshots.

## Example

A storage volume on the cloud provider has a capacity of 4 TB. The cloud
provider informs Atlas that the snapshots occupy the full volume capacity even
though your backups only occupy 500 GB. Due to this reporting, Atlas bills you
for 4 TB in backup storage.

Cluster Type

|

Backup Billing Basis  
  
|  
  
Single-Region

|

Region where Atlas takes and stores the snapshot.

Atlas selects the lowest priority node of the cluster _at the time the
snapshot is taken_. Atlas stores snapshots in the same cloud region as the
cluster.  
  
Multi-Region

|

Region with the highest priority.

Atlas selects the lowest priority cluster node in the highest priority region
to take Backup snapshots and store them.  
  
If the existing snapshot storage volume becomes invalid, Atlas creates a new
snapshot storage volume in the same region as the cluster's current backup
node and takes a full-copy snapshot. Atlas continues using that backup node
and its cloud provider region for snapshots and snapshot storage. This may
result in a higher invoice for the few days required to re-establish
incremental snapshots.

To learn more about how Atlas manages snapshot storage, see Back Up Your
Database Deployment.

When restoring a cluster using a manual download via HTTPS, Atlas also charges
for:

  * Each hour that the download link remains active ( _Atlas Backup Download VM_ charge), and

  * The total storage capacity of the restore virtual machine data volume ( _Atlas Backup Restore Storage_ charge).

## Note

You can't download Backup snapshots that you encrypted using KMS.

If you have questions on Cloud Backup backup sizing and pricing, please
contact Atlas support by clicking Support from the left-hand navigation of the
Atlas UI.

### Continuous Cloud Backups

Cluster owners may enable Continuous Cloud Backup restores from Cloud Backups.
PIT backups are billed based on the disk space occupied by an internal oplog,
combined with the cloud backup snapshot size.

You can configure PIT backups to cover a window of time that you specify.
Longer backup windows result in larger oplogs and higher backup costs.

Atlas takes 51 snapshots for Continuous Cloud Backup each month by default.
You can change the backup policy if needed. In most cases, a new snapshot
saves only the data that changed after your most recent snapshot.

Continuous Cloud Backups support incremental snapshots, where a new snapshot
saves only the data that changed after your most recent snapshot. For example,
a cluster with 10 GB of data and 3 snapshots may require less than 30 GB of
total snapshot storage depending on how data changed between snapshots.

To compute the cost for Continuous Cloud Backups, Atlas obtains the raw metric
data from the cloud providers and calculates the _total_ size of all
snapshots. It then applies a cost per GB determined by:

  * The cloud provider

  * The region in which the snapshots are stored

  * The usage tier

Cloud Provider

|

0-5 GB Storage Used

|

5-100 GB Storage Used

|

100-250 GB Storage Used

|

250-500 GB Storage Used

|

>500 GB Storage Used  
  
|||||  
  
AWS

|

|

$1.00 to $1.55

|

$0.75 to $1.20

|

$0.50 to $0.80

|

$0.25 to $0.40  
  
Azure

|

|

$1.00 to $3.95

|

$0.75 to $2.95

|

$0.50 to $2.00

|

$0.25 to $1.00  
  
Google Cloud

|

|

$0.60 to $0.95

|

$0.45 to $0.70

|

$0.30 to $0.50

|

$0.15 to $0.25  
  
## Example

A cluster on AWS in the `US_EAST_1` region has a combined total snapshot and
oplog size of 115 GB. The first 5 GB are free. The remaining 110 GB are billed
at $1.00 from 5 to 100 GB, and at $0.75 from 100 GB to 115 GB:

(95 × $1.00) + (15 × $0.75) = $106.25 per month

### Snapshot Distribution Costs

If you enable Additional Backup Copies for your cluster, you incur charges for
additional storage in other regions. For example, if you copy all of your
backups to one additional region, you pay for approximately twice the storage:
an amount for your standard backup, and approximately the same amount for your
copies stored in the other region (storage costs vary by region).

## Important

### Google Cloud Platform

In Google Cloud regions, the incrementality of your backups is not preserved.
Each copy stored in Google Cloud is a full copy. Because of this, Google Cloud
backup copies might incur higher costs than the original incremental backup
copies.

In AWS and Azure regions, the incrementality of your backups is preserved
during the copy process.

### Lowering the Monthly Rate

#### Legacy Backups (Deprecated)

Lowering snapshot frequency or lowering snapshot retention lowers the cost per
gigabyte. Increasing the snapshot frequency or the snapshot retention
increases the cost per gigabyte. To modify the snapshot frequency or retention
for a cluster, see Snapshot Schedule.

#### Back Up Your Database Deployment

The cost of backups is dependent on the region of the replica set member
targeted for snapshots. Modifying the region configuration for your cluster
may reduce the cost per gigabyte for snapshot storage. To change regions, see
scaling the cluster.

## BI Connector for Atlas

Excluding MongoDB Atlas Enterprise and MongoDB Atlas Platinum customers, if BI
Connector for Atlas is enabled for your cluster:

  * The billing rate for the BI Connector for Atlas is described in the cluster console as a daily uplift on the cost of the associated cluster. You can view the rate when deploying your cluster or by modifying your cluster.

  * BI Connector for Atlas has a sustained-usage pricing. That is, the daily rate is charged only up to a maximum for the month.

## Number of Nodes

Atlas charges the cluster cost and data storage cost for each data-bearing
node [1] in your cluster.

  * For a replica set, the number of data-bearing nodes equals the replication factor.

  * For a sharded cluster, the number of data-bearing nodes equals the replication factor multiplied by the number of shards.

If you enable sharding, Atlas also runs three config servers in addition to
your data-bearing nodes. Your selections for cluster tier and data storage do
not affect the costs of the config nodes. Config servers are charged at a
separate rate. Their cost is reflected in the cost of the cluster.

[1]|  _(1, 2)_ For replica sets, the data-bearing servers are the servers
hosting the replica set nodes. For sharded clusters, the data-bearing servers
are the servers hosting the shards. For sharded clusters, Atlas also deploys
servers for the config servers; these are charged at a rate separate from the
cluster costs.  
|  
  
← Manage SubscriptionsServerless Instance Costs →

