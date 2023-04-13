Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Encryption at Rest using Customer Key Management

Share Feedback

On this page

  * Configure Atlas with Customer Key Management
  * Enable Customer Key Management for an Atlas Cluster
  * Validate your KMS Configuration
  * Restore a Deleted Key
  * Encrypted Backups

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

Atlas encrypts all cluster storage and snapshot volumes at rest by default.
You can add another layer of security by using your cloud provider's KMS
together with the MongoDB encrypted storage engine.

Configuring Encryption at Rest using your Key Management incurs additional
charges for the Atlas project. To learn more, see Advanced Security.

Atlas `Project Owners` can use one or more of the following customer key
management providers when configuring Encryption at Rest for the Atlas
project:

  * Amazon Web Services Key Management Service

  * Azure Key Vault

  * Google Cloud Platform Key Management Service

After configuring at least one key management provider for the Atlas project,
`Project Owners` can enable customer key management for each Atlas cluster for
which they require encryption. The key management provider does not have to
match the cluster cloud service provider.

Atlas cannot rotate customer-managed encryption keys. Refer to your key
management provider’s documentation for guidance on key rotation. When you set
customer key management in a project, Atlas creates a 90-day key rotation
alert.

If your KMS provider becomes unavailable, this doesn't disable your cluster
while it still runs. If you decide to restart your cluster, the lack of a KMS
provider disables your cluster.

## Configure Atlas with Customer Key Management

Encryption at Rest using Key Management requires valid key management provider
credentials and an encryption key. To provide these details and enable
Customer Key Management:

1

### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

### Toggle the button next to Encryption at Rest using your Key Management to
On.

3

### Enter your key management provider account credentials and provide an
encryption key.

4

### Click Save.

## Enable Customer Key Management for an Atlas Cluster

After you Configure Atlas with Customer Key Management, you must enable
customer key management for each Atlas cluster that contains data that you
want to encrypt.

## Note

You must have the `Project Owner` role to enable customer key management for
clusters in that project.

For new clusters, toggle the Manage your own encryption keys setting to Yes
when you create the cluster.

For existing clusters:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Modify the cluster's configuration.

For the cluster that contains data that you want to encrypt, click the
ellipses ..., then select Edit Configuration.

3

### Enable cluster encryption.

  1. Expand the Additional Settings panel.

  2. Toggle the Manage your own encryption keys setting to Yes.

4

### Review and apply your changes.

  1. Click Review Changes.

  2. Review your changes, then click Apply Changes to update your cluster.

## Validate your KMS Configuration

Atlas validates your KMS configuration:

  * When you add or update credentials.

  * Every 15 minutes.

  * On-demand with the Encryption at Rest API endpoint.

Atlas shuts down all `mongod` and `mongos` processes on the next scheduled
validity check if one of the following conditions exist:

  * your key management provider credentials become invalid

  * someone deletes or disables your encryption key

If Atlas _can't connect_ to your key management provider, Atlas doesn't shut
down your processes.

If Atlas shuts down your clusters, the following events occur:

  * Atlas sends an email to the `Project Owner` listing all affected clusters.

  * The Database Deployments page reflects that Atlas disabled your clusters due to invalid Encryption at Rest settings.

You can't read or write data on disabled clusters. You _can_ submit updates to
disabled clusters, such as disk and instance size changes. Atlas processes
these changes once someone restores your encryption key. Atlas continues to
perform maintenance and apply security patches. Disabled clusters retain all
your data, so billing continues.

## Note

### Virtual Machine Power

While a cluster is disabled, Atlas does not stop the Virtual Machine (VM) the
cluster is running on. Atlas may perform patches that reboot the server, but
VM power is not cycled.

To regain access to your data:

  * Update your credentials if they have changed since configuring Atlas with Customer Key Management.

  * Restore your key if it has been disabled or deleted.

click to enlarge

After updating your configuration, click Try Again to validate it. If you
don't, Atlas validates on its next scheduled check. All `mongod` and `mongos`
processes restart after Atlas determines your configuration to be valid.

## Warning

If your key was deleted, restore that key to regain access to your clusters.
You cannot change a key or disable Encryption at Rest using Customer Key
Management without a valid key.

## Restore a Deleted Key

To restore a deleted key, see your key management provider's documentation:

  *  **AWS KMS:** Deleting Customer Master Keys

  *  **Azure Key Vault:** Recover Deleted Key

  *  **GCP KMS:** Destroying and restoring key versions

## Encrypted Backups

Atlas encrypts all snapshot volumes. This secures your cluster data on disk.
Using your cloud provider's KMS, you can:

  * Encrypt your snapshot storage volumes where you store your backups.

  * Encrypt the data files in your snapshots.

  * Restore snapshots with the key that was active at the time the snapshot was taken.

  * Encrypt PIT restore oplog data.

You cannot restore snapshots encrypted with keys that have become invalid.

You cannot enable Legacy Backups (Deprecated) on clusters encrypted with keys
that you manage. You _can_ specify a base snapshot schedule that backs up
every 6 hours.

To learn more about customer key management and Cloud Backups, see Storage
Engine and Cloud Backup Encryption and Restore from a Snapshot Using
Encryption at Rest.

← Set Up Self-Managed X.509 AuthenticationManage Customer Keys with AWS KMS →

