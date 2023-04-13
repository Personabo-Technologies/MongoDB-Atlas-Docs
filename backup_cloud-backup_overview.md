Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Back Up Your Database Deployment

Share Feedback

## Note

### Feature Unavailable in Free-Tier Clusters

This feature is not available for `M0` free clusters. To learn more about
which features are unavailable, see Atlas M0 (Free Cluster), M2, and M5
Limitations.

Atlas Cloud Backups provide localized backup storage using the native snapshot
functionality of the cluster's cloud service provider.

## Note

You must have the `Project Owner` role for an Atlas project to manage backup
for the clusters in that project.

Atlas supports cloud backup for clusters served on:

  * Microsoft Azure

  * Amazon Web Services (AWS)

  * Google Cloud Platform (GCP)

You can enable cloud backup during the cluster creation or during the
modification of an existing cluster. From the cluster configuration modal,
toggle Turn on Cloud Backup to Yes.

If you have strict data protection requirements, you can enable a Backup
Compliance Policy to protect your backup data.

If you need to retain any legacy backup snapshots for archival purposes,
download them before you switch to Cloud Backup from legacy backups. To learn
how to download a snapshot, see Restore a Cluster from a Legacy Backup
Snapshot.

When you change from Legacy Backups to Cloud Backups, Atlas retains your
Legacy Backup snapshots in accordance with your legacy backup retention
policy.

## Important

### Limitations of Cloud Backup

Cloud Backups:

  * Can support sharded clusters running MongoDB version 4.0 or later.

  * Cannot restore an existing snapshot to a cluster after you add or remove a shard from it. You may restore an existing snapshot to another cluster with a matching topology.

## Note

### Sharded Cluster Balancer, FCV 4.0 databases and Cloud Backup

With databases running `FCV` 4.0 or earlier, Cloud Backup automatically
disables the balancer for snapshots if it's running. This ensures an inactive
balancer during the backup operation. When the snapshot completes, Cloud
Backup returns the balancer to its previous state.

← Back Up, Restore, and Archive DataDedicated Cluster Backups →

