Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Move a Cluster to a Different Region

Share Feedback

On this page

  * Considerations
  * Move a Single-Region Cluster
  * Move a Multi-Region Cluster

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

## Considerations

### Support by Cluster Tier

Atlas supports changing a cluster's region and cloud provider:

  * When you increase the cluster tier of an `M0`, `M2`, or `M5` cluster.

  * Anytime on an `M10+` multi-region cluster.

### Preferred and Electable Nodes

Each node in the preferred and electable regions can:

  * Participate in replica set elections

  * Become the primary if the majority of replica set nodes are available.

Electable nodes in the cluster must total 3, 5, or 7.

### Migration, Downtime and Performance Impact

Depending on the amount of data to migrate, migrations can take a significant
amount of time. To maximize availability for a replica set, Atlas migrates one
member at a time, starting with the secondary members first and then the
primary.

Migration can affect performance if your primary is already reaching
operational capacity: each newly migrated replica set member must perform an
initial sync from the primary, adding to the operational load. Migrations can
also affect performance if read preferences are set to read from secondaries:
the replica set is down one secondary during the migration.

### VPC Peering (AWS Only)

If you move a cluster out of a region that has a VPC (Virtual Private Cloud)
peering connection, the moved cluster can no longer use that peering
connection to communicate with servers in the VPC. Any other clusters with
nodes remaining in the original region can continue to use the VPC peering
connection.

You can create multiple VPC connections for each region, including a new VPC
peering connection with the region that you moved a cluster to.

## Note

Cluster nodes removed from a region can't inherit access rules from an AWS
security group or allowed VPC CIDR blocks configured for the VPC peering
connection. You must Configure IP Access List Entries for all the virtual
servers residing in the VPC. Cluster nodes remaining in the region are
unaffected.

### Billing

If you change your cluster's highest priority region or if MongoDB migrates
oplog data to a different region, you will be billed for storage in both the
old and new regions for the days following the region change. You must disable
continuous cloud backup and reenable it to prevent billing in both the
regions.

## Note

If you disable continuous cloud backup, Atlas will delete the continuous cloud
backup history.

## Move a Single-Region Cluster

Use the following procedure to move nodes to a single-region cluster.

1

### Go to the Database Deployments view.

Click Database in the top-left corner of Atlas. Click the ellipses ... icon
for the cluster that you want to move, then select Edit Configuration.

Alternatively, if you are already viewing the specific cluster, click
Configuration.

2

### In the Cloud Provider & Region view, select the desired new region for the
new cluster.

For `M0`, `M2`, and `M5` clusters:

  * You must also select a higher cluster tier. Atlas supports moving `M0`, `M2`, or `M5` clusters only when you increase the cluster tier.

  * The available regions are a subset of the total supported regions for any given cloud service provider.

3

### Click Review Changes.

4

### Click Apply Changes or Apply Changes and Checkout to configure the billing
information.

## Move a Multi-Region Cluster

Use the following procedure to move nodes to one or more regions in an `M10`
or larger multi-region cluster:

1

### Select the database deployment and open the configuration menu.

  1. Click Database in the top-left corner of Atlas.

  2. Click the ellipses ... icon for the cluster that you want to move, then select Edit Configuration.

Alternatively, if you are already viewing the specific cluster, click
Configuration.

2

### In the Cloud Provider & Region view, review the current multi-region
configuration options.

For a given region, click the currently selected Region and pick a new region
from the drop-down list. If you modify the Preferred region, the Atlas cluster
calls for one or more elections to select a new primary in the selected
region. See Test Primary Failover for instructions on testing your application
response to a replica set election before changing the Preferred cluster.

To change the number of nodes Atlas deploys to a given region, increase or
decrease the Number of Nodes value. the total number of nodes across the
Preferred region and all Electable regions must be an odd number.

3

### Click Confirm & Deploy.

← Shard a Global CollectionMonitor Your Database Deployments →

