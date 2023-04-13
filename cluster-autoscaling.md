Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Auto-Scaling

Share Feedback

On this page

  * How Atlas Scales Cluster Tier
  * Scaling Up a Cluster Tier
  * Scaling Down a Cluster Tier
  * Scaling a Sharded Cluster
  * How Atlas Scales Cluster Storage
  * Cluster Tier and Cluster Storage Might Scale in Parallel
  * Oplog Considerations
  * Configure Auto-Scaling Options
  * Auto-Scaling Enabled by Default
  * Review the Cluster Tier Auto-Scaling Options
  * Opt Out of Cluster Tier and Storage Auto-Scaling
  * Acknowledge Auto-Scaling Events

## Note

### Feature Availability

Atlas enables Cluster Auto-Scaling for all cluster tiers (except the highest
cluster tier) under the General and the Low-CPU tier clusters.

You can configure the cluster tier ranges that Atlas uses to automatically
scale your cluster tier, storage capacity, or both in response to cluster
usage.

Cluster auto-scaling removes the need to write scripts or use consulting
services to make scaling decisions. To help control costs, you can specify a
range of maximum and minimum cluster sizes that your cluster can automatically
scale to.

Auto-scaling works on a rolling basis, meaning the process doesn't incur any
downtime.

## How Atlas Scales Cluster Tier

Atlas analyzes the following cluster metrics to determine when to scale a
cluster, and whether to scale the cluster tier up or down:

  * CPU utilization

  * Memory utilization

Atlas calculates memory utilization based on your available memory and total
memory as follows:

(`total system memory` \- (`free` \+ `buffer` \+ `cache`) - WiredTiger's
internal cache currently in use) / (`total system memory` \- WiredTiger's
internal cache currently in use) * 100

In the previous calculation, `free`, `buffer`, and `cache` are amounts of
available memory that Atlas can reclaim for other purposes. To learn more, see
System Memory in Review Available Metrics.

Atlas won't scale your cluster tier if any of the following are true:

  * New cluster tier would fall outside of your specified Minimum and Maximum Cluster Size range.

  * Memory utilization, including WiredTiger's internal cache, would exceed the available memory for the new cluster tier.

Atlas scales your cluster to another tier in the same class. For example,
Atlas scales General clusters to other General cluster tiers, but doesn't
scale General clusters to Low-CPU cluster tiers.

## Important

During a migration, if you restore a snapshot with a larger size than the
storage capacity of the destination cluster, the cluster does not
automatically scale.

### Scaling Up a Cluster Tier

## Note

### Tier Availability

Automatic scaling works on General and Low-CPU tier clusters, but _not_ on
Local NVMe SSD tier clusters.

If the next highest cluster tier is within your Maximum Cluster Size range,
Atlas scales the cluster up to the next tier if _one_ of the following
criteria is true for _any_ node in the cluster:

  * The Average CPU Utilization has exceeded 75% for the past hour.

  * The Memory Utilization has exceeded 75% for the past hour.

Atlas scales a cluster to the next tier when the cluster hasn't been scaled up
in the past hour.

## Important

### Sudden Workload Spikes

Scaling up to a greater cluster tier requires enough time to prepare backing
resources. Automatic scaling may not occur when a cluster receives a burst of
activity, such as a bulk insert. To reduce the risk of running out of
resources, plan to scale up clusters before bulk inserts and other workload
spikes.

### Scaling Down a Cluster Tier

If the next lowest cluster tier is within your Minimum Cluster Size range,
Atlas scales the cluster down to the next lowest tier if _both_ of the
following criteria are true for _all_ nodes in the cluster:

  * The average CPU Utilization and Memory Utilization over the past 24 hours is below 50%.

  * The cluster hasn't been scaled down (manually or automatically) in the past 24 hours.

## Note

`M10` and `M20` clusters use lower thresholds to account for caps on CPU usage
that cloud providers set after burst periods. These thresholds vary depending
on your cloud provider and cluster tier.

To learn more about downward auto-scaling behavior, see Considerations for
Downward Auto-Scaling of Cluster Tier and Storage.

#### Considerations for Downward Auto-Scaling of Cluster Tier and Storage

  * When Atlas downscales the storage capacity of your cluster, this can take longer than expanding storage capacity due to the mechanics of the scaling process.

  * When Atlas downscales your cluster to a lower cluster tier, it uses the value in the Minimum Cluster Size. Estimate your deployment's range of workloads and then set the Minimum Cluster Size value to the cluster tier that has enough capacity to handle your deployment's workload. Account for any possible spikes or dips in cluster activity.

  * You can't scale to a cluster smaller than `M10`.

  * When Atlas downscales your cluster, it checks that your minimum cluster tier bound supports the current disk configuration of your cluster. If your selected minimum cluster tier can't support your current disk configuration, Atlas adjusts your minimum tier to the next lowest tier that can support your configuration.

## Example

You have set your auto-scaling bounds to `M10`-`M60` and your current cluster
tier is `M40`. Atlas triggers a downward auto-scaling event because the
average CPU Utilization and Memory Utilization on your current cluster has
been under 50% for the past 24 hours.

    1. Atlas attempts to auto-scale your cluster down to `M30`. `M30` supports your current disk configuration, so the auto-scaling operation succeeds.

    2. Atlas checks your minimum cluster bound (`M10`) and determines that `M10` can't support your current disk configuration.

    3. Atlas determines that `M20` is the lowest cluster tier that can support your current disk configuration, and sets your minimum cluster tier to `M20`.

### Scaling a Sharded Cluster

Atlas auto-scales the cluster tier for sharded clusters using the same
criteria as replica sets. Atlas applies the following rules:

  * Auto-scaling applies to all shards in the sharded cluster. You can't apply auto-scaling for some shards and not for others within the same cluster.

  * If _any_ shard meets the criteria to auto-scale its cluster tier up, all shards will scale their cluster tier up.

  *  _All_ shards in the cluster must meet the criteria before Atlas will auto-scale the cluster tier down.

  * The Config server replica set doesn't auto-scale.

## How Atlas Scales Cluster Storage

Atlas enables cluster storage auto-scaling by default. For clusters with
analytic nodes, if you select a different cluster class, such as General or
Low-CPU, for the Base Tier and the Analytics Tier, Atlas disables disk auto-
scaling with the following error message:

    
    
    Disk auto-scaling is not yet available for clusters with mixed instance classes.  
      
  
Atlas automatically increases cluster storage when disk space used reaches 90%
for _any_ node in the cluster.

## Important

### High-Speed Write Activity

Scaling up to greater storage capacity requires sufficient time to prepare and
copy data to new disks. Automatic scaling might not occur when a cluster
receives a burst of high-speed write activity, such as a bulk insert. To
reduce the risk of running out of disk storage, cluster managers should plan
to scale up clusters in advance of bulk inserts and other instances of high-
speed write activity.

The scaling behavior differs by cloud provider:

  * On AWS and GCP clusters, Atlas increases cluster storage capacity to achieve 70% disk space used. To learn more about AWS storage change limitations and how Atlas works around them, see Change Storage Capacity or IOPS on AWS.

  * On Azure clusters, Atlas doubles the current amount of cluster storage.

## Important

Atlas automatically scales cluster storage only up, and never automatically
scales cluster storage down. You can manually reduce your cluster storage from
the Edit Cluster page.

### Cluster Tier and Cluster Storage Might Scale in Parallel

When Atlas attempts to automatically scale your cluster storage capacity, it
might need to scale your storage outside of the bounds supported that your
current cluster tier supports. To help ensure that your cluster doesn't
experience any downtime, Atlas will scale your cluster tier (in addition to
cluster storage) to accommodate the new storage capacity.

## Example

The maximum storage capacity for an `M30` cluster is 480 GB. If you have an
`M30` cluster with the maximum storage allocated and your disk space used
reaches 90%, a storage auto-scaling event requires raising your storage
capacity to 600 GB. In this case, Atlas scales your cluster tier up to `M40`
because this is the lowest cluster tier that can support the new required
storage capacity.

In the event that your specified maximum cluster tier can't support the new
storage capacity, Atlas:

  1. Raises your maximum cluster tier to the next lowest tier that can accommodate the new storage capacity.

  2. Scales your cluster tier to that new maximum tier.

## Note

When Atlas overrides your maximum cluster tier, it also disables your cluster
from automatically scaling down. To re-enable downward auto-scaling, configure
it in Cluster Settings. See also Considerations for Downward Auto-Scaling of
Cluster Tier and Storage.

If Atlas attempts to scale your cluster tier down and the target tier can't
support your current disk capacity, provisioned IOPS, or both, Atlas doesn't
scale your cluster down. In this scenario, Atlas updates your auto-scaling
settings based on the relationship between your current cluster tier and the
configured maximum cluster tier:

  * If the cluster is currently at the configured maximum cluster tier, Atlas disables the cluster from automatically scaling down because all smaller tiers wouldn't be able to accommodate the necessary storage settings. If you want to re-enable downward auto-scaling, you must do so manually from your Cluster Settings.

  * If the cluster isn't currently at the configured maximum cluster tier, Atlas raises the minimum cluster tier to the current cluster tier. In this case, Atlas doesn't disable downward auto-scaling.

This auto-scaling logic is designed to reduce the downtime incurred by your
storage settings not matching your workload.

When an auto-scaling event modifies your configured minimum or maximum cluster
tier, Atlas sends an email to all project owners about the new cluster tier
and any modified minimum or maximum tier bounds.

### Oplog Considerations

When you increase the storage capacity of a cluster, Atlas increases the
cluster's oplog size. Atlas scales the oplog to 5% of the cluster capacity,
not to exceed 50 GB. NVMe storage requires an oplog which is 10% of the
storage capacity. Atlas doesn't change the oplog size if it exceeds 5% of the
new storage capacity (10% in the case of NVMe storage).

As cluster storage capacity decreases, Atlas doesn't change the oplog size
unless it exceeds a certain maximum determined according to MongoDB best
practices.

## Configure Auto-Scaling Options

You can configure auto-scaling options when you create or modify a cluster.
For new clusters, Atlas automatically enables cluster tier auto-scaling and
storage auto-scaling. You can review and adjust the upper and lower cluster
tiers that Atlas should use when auto-scaling your cluster, or you can opt
out.

Atlas displays auto-scaling options in the Auto-scale section of the cluster
builder for General and Low-CPU tier clusters.

### Auto-Scaling Enabled by Default

When you create a new cluster, Atlas enables auto-scaling for cluster tier and
cluster storage. You don't need to explicitly enable auto-scaling. If you
prefer, you can opt out for cluster tier and cluster storage.

## Note

Atlas enables cluster tier auto-scaling by default when you create clusters in
the Atlas UI. If you create clusters with the API, Atlas disables cluster tier
auto-scaling by default.

With auto-scaling enabled, your cluster can automatically:

  * Scale up to increase capability with a higher cluster tier.

  * Decrease the current cluster tier to a lower cluster tier.

In the Cluster tier section of the Auto-scale options, you can specify the
Maximum Cluster Size and Minimum Cluster Size values that your cluster can
automatically scale to. Atlas sets these values as follows:

  * The Maximum Cluster Size is set to one tier above your current cluster tier.

  * The Minimum Cluster Size is set to the current cluster tier.

### Review the Cluster Tier Auto-Scaling Options

To review the enabled auto-scaling options for cluster tier and storage:

  1. In the selected Auto-Scale checkbox, review the Maximum Cluster Size and Minimum Cluster Size values, and adjust them if needed.

  2. Review the Allow cluster to be scaled down option that is checked by default when you create a new cluster.

  3. Review the options under the Storage Scaling checkbox that is checked by default.

### Opt Out of Cluster Tier and Storage Auto-Scaling

To opt out of cluster auto-scaling (increasing the cluster tier), when
creating a new cluster, navigate to the Cluster Tier menu, and un-check the
Cluster Tier Scaling checkbox in the Auto-scale section.

To opt out of cluster auto-scaling (decreasing the cluster tier), when
creating a new cluster, navigate to Cluster Tier menu, and un-check the Allow
cluster to be scaled down checkbox in the Auto-scale section.

To opt out of cluster storage scaling, un-check the Storage Scaling checkbox
in the Auto-scale section.

## Acknowledge Auto-Scaling Events

When an auto-scaling event occurs:

  * Atlas logs the event in the project Activity Feed. To learn more about the Activity Feed, see View All Activity.

  * Atlas sends an email to all project owners about the original cluster tier and the new cluster tier after auto-scaling has occurred.

← Customize Cluster StorageConfigure Additional Settings →

