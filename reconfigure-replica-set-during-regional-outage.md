Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Reconfigure a Replica Set During a Regional Outage

Share Feedback

On this page

  * Prerequisites
  * Procedure

During a regional outage, your cluster might not have a primary node if the
regional outage affects a majority of the cluster's electable nodes. You can
use the Atlas UI to restore your Atlas multi-region cluster by reconfiguring
your cluster.

If you reconfigure your cluster during an outage, your cluster might lose data
in the following circumstances:

  * If your MongoDB process didn't replicate write operations to the node that becomes primary after the reconfiguration in any cluster. Your replica set rolls back these writes when the unavailable members become available again. To learn more, see Rollbacks During Replica Set Failover.

  * In sharded clusters, if your MongoDB process didn't replicate chunk migrations. The data inconsistency might cause orphaned chunks.

## Note

If you force a reconfiguration for a sharded cluster, Atlas adds two new nodes
to the config server replica set in a region unaffected by the outage. When
you apply subsequent cluster changes after the sharded cluster becomes
healthy, Atlas removes the additional nodes.

## Prerequisites

Your cluster must be experiencing a total outage of nodes in one or more
regions with at least one electable node remaining in another region.

For assistance with other causes of node outages, contact support.

## Procedure

To restore your Atlas multi-region cluster from an outage, you must manually
reconfigure your replica set:

1

### For the cluster you want to recover, click the ... button.

2

### Click Edit Configuration.

3

### Click Cloud Provider & Region.

Under Electable nodes for high availability, you can add new nodes to:

  * An existing region by editing the number of nodes in the Nodes column

  * A new region by clicking \+ Add a provider/region

## Tip

We strongly advise not adding nodes to one of the regions with an outage.

4

### Click Review Changes.

Read the Considerations for force configuration, and check the box next to I
have reviewed these considerations for force configuration and agree to
proceed.

5

### Click Apply Changes.

← Convert a Shared Cluster to a Serverless InstanceUpgrade Major MongoDB
Version for a Cluster →

