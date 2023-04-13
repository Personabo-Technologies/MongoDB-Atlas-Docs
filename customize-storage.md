Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Customize Cluster Storage

Share Feedback

On this page

  * Cluster Class
  * Low CPU Class
  * NVMe Storage
  * Storage Capacity
  * Oplog Scaling Behavior
  * Change Storage Capacity or IOPS on AWS
  * Change Storage Capacity on Azure
  * Change Storage Capacity on Google Cloud
  * Change Storage Capacity for Multi-Cloud Provider Clusters
  * IOPS (AWS Only)
  * Provisioned IOPS vs Standard IOPS in AWS
  * Configure the IOPS Rate
  * Minimum Disk Capacity to RAM Ratios
  * Auto-Scale Cluster Tier and Storage Capacity

Each cluster tier comes with a default set of resources. `M10+` clusters
provide the ability to customize your storage capacity.

Atlas provides the following storage configuration options, depending on the
selected cloud provider and cluster tier.

## Cluster Class

`M40+` clusters offer multiple options, including:

  * Low CPU

  * General

  * Local NVMe SSD

All production environments can use the General option.

Select the Class box with your preferred speed. Changes to cluster class
affect cost.

### Low CPU Class

The Low CPU option offers a lower-cost alternative for applications that
require more memory and fewer CPUs. This option includes half the vCPUs of an
instance with the General option. For example, a General `M40` instance
includes 4 vCPUs, while a Low CPU `M40` instance includes 2 vCPUs. Depending
on the cluster tier, this option may also include fewer max connections. To
learn more, see Connection Limits and Cluster Tier.

### NVMe Storage

You can select the Local NVMe SSD storage option for some dedicated clusters
that run on AWS or Azure. Locally attached ephemeral NVMe SSDs offer the
highest level of speed and performance.

## Note

Atlas doesn't support NVMe clusters on Google Cloud.

## Storage Capacity

To change the server data volume size, do one of the following tasks:

  * Specify the exact disk size in the text box.

  * Move the slide bar until the text box displays your preferred disk size.

For Azure-specific instructions, see Change Storage Capacity on Azure.

Changes to storage capacity affect cost.

## Note

MongoDB uses a small portion of your specified storage capacity for buffer
files, journal files, and log files to ensure proper cluster operation. In no-
overwrite storage engines like the WiredTiger storage engine, you should
expect to use approximately 20% more disk space than your compressed data
occupies.

### Oplog Scaling Behavior

When you increase the storage capacity of a cluster, Atlas increases the
cluster's oplog size. Atlas scales the oplog to 5% of the cluster capacity,
not to exceed 50 GB. NVMe storage requires an oplog which is 10% of the
storage capacity. Atlas doesn't change the oplog size if it exceeds 5% of the
new storage capacity (10% in the case of NVMe storage).

As cluster storage capacity decreases, Atlas doesn't change the oplog size
unless it exceeds a certain maximum determined according to MongoDB best
practices.

### Change Storage Capacity or IOPS on AWS

Atlas handles changes differently based on whether you want to increase or
decrease storage capacity or storage throughput (IOPS) on AWS.

#### Increase Capacity or Throughput

AWS allows you to increase storage capacity or IOPS every six hours as long as
previous changes have completed. Atlas supports more changes within that six-
hour window.

How Atlas handles additional changes within a six-hour window depends on the
size of your hosts' data volumes and the time when you make the change in the
six-hour window.

  * For the first change, Atlas modifies data volumes in place without downtime.

  * For later changes:

Data Volume Size

|

Time Since Last Storage Change

|

Action Atlas Takes  
  
||  
  
Less than 1TB

|

Less than 5h30m

|

Atlas provisions new volumes and syncs the data from the old volumes. If Atlas
provisions new volumes, you can access your cluster. You can't access _nodes_
that AWS modifies until AWS attaches the new volume.  
  
Less than 1TB

|

More than 5h30m

|

Atlas waits until the six-hour window closes, then modifies the hosts' data
volumes in place without downtime.  
  
More than 1TB

|

Any

|

Atlas waits until the six-hour window closes, then modifies the hosts' data
volumes in place without downtime. This takes less time than provisioning new
volumes and syncing data from the old to the new volumes.  
  

Before you apply your storage capacity or IOPS increases, the Review Changes
page describes how Atlas approaches the increase.

The Database Deployments page displays a banner if Atlas waits until a six-
hour window closes before modifying your cluster's storage capacity or IOPS.

These behaviors apply when Atlas changes capacity during auto-scaling.

To learn more about AWS's limitations, see the AWS documentation.

#### Decrease Capacity or Throughput

  * AWS doesn't allow you to reduce storage _capacity_ in place.

Atlas _can_ reduce storage capacity in place. Atlas provisions new volumes
then syncs data from the old to the new volumes. This works around the AWS
limitation.

  * AWS _does_ allow you to reduce IOPS without migrating data.

### Change Storage Capacity on Azure

For clusters deployed on Azure, you can change storage capacity in preset
amounts only. To change server data volume size:

  * Specify your preferred disk size in the text box.

  * Move the slide bar until the text box displays your preferred disk size.

## Note

Atlas rounds the disk size to the nearest preset amount.

When you change a cluster's storage capacity, Atlas modifies the size of the
servers' data volumes in a rolling manner with zero downtime. Atlas increases
the storage capacity in place without copying data or performing an initial
sync.

However, Azure doesn't allow in-place storage capacity downgrades. If you
downgrade the storage capacity of a cluster, Atlas replaces each node and
performs an initial sync for each node in the cluster.

## Note

An initial sync copies data across the network and rebuilds all indexes.

During this time, you can still access your cluster, but each node that Azure
modifies remains unavailable until the initial sync for that node completes.

## Important

For large clusters, initial syncs for each node might take several hours to
complete.

Before you apply your storage capacity changes, the Review Changes page
notifies you that Atlas triggers a rolling restart of your cluster when you
make this change.

### Change Storage Capacity on Google Cloud

When you change a cluster's storage capacity, Atlas modifies the size of the
servers' data volumes in a rolling manner with zero downtime.

Atlas increases the storage capacity in place without copying data or
performing an initial sync. However, Google Cloud doesn't allow in-place
storage capacity downgrades.

If you downgrade the storage capacity of a cluster, Atlas provisions new
volumes, and then syncs data from the old to the new volumes.

Before you apply your storage capacity changes, the Review Changes page
notifies you that Atlas triggers a rolling restart of your cluster when you
make this change.

### Change Storage Capacity for Multi-Cloud Provider Clusters

Atlas selects the lowest common denominator across the three cloud providers.
This ensures consistency across the multi-cloud deployment.

The following limitations might apply:

  * You can't adjust the IOPS for your multi-cloud cluster.

  * If your multi-cloud cluster includes Azure, you can change storage capacity in preset amounts only. See Change Storage Capacity on Azure.

## IOPS (AWS Only)

AWS-backed `M30+` clusters offer the option to provision IOPS.

### Provisioned IOPS vs Standard IOPS in AWS

Provisioned IOPS let you customize the maximum IOPS rate for your cluster.
They also:

  * Deliver their configured IOPS rate more consistently when compared to standard IOPS.

  * Lower your cluster's p90 latency (measurement of the server's response time). 90 percent of server requests have responses faster than the p90 latency value, so a lower p90 latency value means a generally faster response time.

To learn more about the merits of using provisioned vs standard IOPS, see
Amazon EBS-optimized instances. See the following summary:

  * General Purpose SSD volumes are designed to deliver their baseline performance 99% of the time.

  * Provisioned IOPS SSD volumes are designed to deliver their provisioned performance 99.9% of the time.

## Note

Changes to IOPS provisioning affects characteristics, performance, and cost.
When you select Provision IOPS, the storage changes from **General Purpose
SSD** volumes to **Provisioned IOPS SSD** volumes.

### Configure the IOPS Rate

#### Standard IOPS

If you do not select the Provision IOPS option when you create your `M30+`
tier cluster, the cluster uses standard IOPS. The default standard IOPS rate
changes as the cluster's storage capacity changes. If you want to provision an
exact IOPS value, enable provisioning.

The minimum standard IOPS for `M30+` tier clusters is 3000. The standard IOPS
value remains at 3000 unless you set the cluster storage size to 1TB or more.
If the storage for your `M30+` cluster meets or exceeds 1TB, Atlas increases
the standard IOPS rate using an IOPS to storage ratio of 3:1.

Local NVMe SSD class clusters must use standard IOPS.

#### Provisioned IOPS

To provision IOPS for your `M30+` tier cluster, select Provision IOPS and
either:

  * Specify the exact IOPS rate in the text box, _or_

  * Move the slide bar until the text box displays your preferred IOPS rate.

## Note

The available provisioned IOPS range for a cluster relates to disk storage
capacity. Changing your cluster's storage capacity changes the range of
available provisioned IOPS.

### Minimum Disk Capacity to RAM Ratios

Atlas enforces the following minimum ratios for given cluster tiers. This
keeps cluster performance consistent with large datasets.

Instance sizes **M10** to **M40** have a ratio of disk capacity to system
memory of 60:1. Instance sizes greater than **M40** have a ratio of 120:1.

## Example

To support 3 TB (or 3,072 GB) of disk capacity, select a cluster tier with a
minimum of 32 GB of RAM. This would be **M50** or greater.

Atlas has disk capacity limits on single replica sets, scaling up to 4 TB for
higher cluster tiers. To expand the total cluster storage beyond default
limits, you can enable extended storage in the Project Settings. To
accommodate further scaling in the future, we recommend that you enable
sharding for long-term expansion.

## Tip

### See also:

To learn more about the default resources and available configuration options
for each cloud service provider, see:

  * AWS Configuration Options

  * GCP Configuration Options

  * Azure Configuration Options.

## Auto-Scale Cluster Tier and Storage Capacity

## Note

### Feature Availability

Atlas enables Cluster Auto-Scaling for all cluster tiers (except the highest
cluster tier) under the General and the Low-CPU tier clusters.

For new clusters, Atlas automatically enables cluster tier auto-scaling and
storage auto-scaling.

Use Auto-scale options to configure your cluster to automatically scale your
{+cluster tier+}, storage capacity, or both in response to cluster usage.

## Important

During a migration, if you restore a snapshot with a larger size than the
storage capacity of the destination cluster, the cluster does not
automatically scale.

You can opt out of cluster tier and storage autoscaling. To learn more, see
How Atlas Scales Cluster Tier and How Atlas Scales Cluster Storage.

## Tip

### See also:

  * Configure Auto-Scaling

  * Connection Limits and Cluster Tier

← Manage ClustersConfigure Auto-Scaling →

