Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Manage Customer Keys with Google Cloud KMS

Share Feedback

On this page

  * Enable Customer-Managed Keys with Google Cloud KMS
  * Rotate your GCP Key Version Resource ID
  * Related Topics

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

Atlas uses your Google Cloud Service Account Key to encrypt and decrypt your
MongoDB master keys. These MongoDB master keys are used to encrypt cluster
database files and cloud providers snapshots.

When you use your own cloud provider KMS, Atlas automatically rotates the
MongoDB master keys every 90 days. These keys are rotated on a rolling basis
and the process does not require the data to be rewritten.

Atlas encrypts your data at rest using encrypted storage media. Using keys you
manage with Google Cloud KMS, Atlas encrypts your data a second time when it
writes it to the MongoDB encrypted storage engine. You use your Google Cloud
SAK to encrypt the MongoDB master encryption keys.

This page covers configuring customer key management using Google Cloud on
your Atlas project.

You must configure customer key management for the Atlas project before
enabling it on clusters in that project.

## Enable Customer-Managed Keys with Google Cloud KMS

### Prerequisites

To enable customer-managed keys with Google Cloud KMS for a MongoDB project,
you must have:

  * Use an M10 or larger cluster.

  * Use Cloud Backups to encrypt your backup snapshots. Legacy Backups are not supported.

  * Your Google Cloud Service Account Key.

  * Your symmetric Encryption Key in Google Cloud KMS.

  * The Key Version Resource ID associated with your Google Cloud KMS Encryption Key.

  * A Google Cloud service account with credentials specified in your Service Account Key with sufficient permissions to:

    * Get the Google Cloud KMS Encryption Key version.

    * Encrypt data with the Google Cloud KMS Encryption Key version.

    * Decrypt data with the Google Cloud KMS Encryption Key.

## Note

The key, not the key version, handles decryption.

  * If your Google Cloud KMS configuration requires it, allow access from Atlas IP addresses and the public IP addresses or DNS hostnames of your cluster nodes so that Atlas can communicate with your KMS. If the node IP addresses change, you must update your configuration to avoid connectivity interruptions.

## Tip

### See also:

See the Google Cloud documentation to learn how to:

  * Create a service account key.

  * Obtain a key version resource ID.

  * Grant roles to service accounts.

### Enable Customer-Managed Keys for a Project

You must enable customer key management for a project before you can enable it
on a cluster in that project.

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Toggle the button next to Encryption at Rest using your Key Management to
On.

3

#### Select Google Cloud KMS.

4

#### Enter your Service Account Key.

Your Service Account Key should be formatted as a JSON object. It contains the
encryption credentials for your GCP service account.

5

#### Enter the Key Version Resource ID.

Your key version resource ID is the fully-qualified resource name for a
CryptoKeyVersion.

6

#### Click Save.

### Enable Customer Key Management for an Atlas Cluster

After you Enable Customer-Managed Keys for a Project, you must enable customer
key management for each Atlas cluster that contains data that you want to
encrypt.

## Note

You must have the `Project Owner` role to enable customer key management for
clusters in that project.

For new clusters, toggle the Manage your own encryption keys setting to Yes
when you create the cluster.

For existing clusters:

1

#### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

#### Modify the cluster's configuration.

For the cluster that contains data that you want to encrypt, click the
ellipses ..., then select Edit Configuration.

3

#### Enable cluster encryption.

  1. Expand the Additional Settings panel.

  2. Toggle the Manage your own encryption keys setting to Yes.

4

#### Review and apply your changes.

  1. Click Review Changes.

  2. Review your changes, then click Apply Changes to update your cluster.

### Alerts

Atlas automatically creates an `encryption key rotation alert` once you
configure customer key management for a project. You can reset this alert at
any time by rotating your GCP Key Version Resource ID.

## Rotate your GCP Key Version Resource ID

## Note

  * This feature is not available for `M0` free clusters, `M2`, and `M5` clusters. To learn more, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

  * This feature is not supported on Serverless instances at this time. To learn more, see Serverless Instance Limitations.

When you use your own cloud provider KMS, Atlas automatically rotates the
MongoDB master keys every 90 days. These keys are rotated on a rolling basis
and the process does not require the data to be rewritten.

Atlas does _not_ automatically rotate the Key Version Resource ID used for
Google Cloud key management.

Atlas automatically creates an `encryption key rotation alert` to remind you
to rotate your GCP Key Version Resource ID every 90 days by default when you
enable Encryption at Rest for an Atlas project.

### Prerequisites

You must create a new Service Account Key in the Google Cloud account
associated with your Atlas project.

### Procedure

The following procedure documents how to rotate your Atlas project Key
Identifier by specifying a new Key Version Resource ID in Atlas.

1

#### Navigate to the Advanced page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Click Advanced in the sidebar.

2

#### Click Rotate Keys __.

3

#### Update the GCP Key details.

  1. Click Google Cloud KMS if the Google Cloud KMS tab is not already active.

  2. Expand Encryption Key Credentials if the Encryption Key Credentials dialog is not already displayed.

  3. Enter the GCP Key Version Resource ID in the Key Identifier entry.

Include the fully-qualified resource name for a CryptoKeyVersion.

## Example

    
        projects/my-project-0/locations/us-east4/keyRings/my-key-ring-0/cryptoKeys/my-key-0/cryptoKeyVersions/1  
      
  
The encryption key **must** belong to the Google Cloud Service Account Key
configured for your Atlas project. Click the Service Account Key section to
view the currently configured Service Account Key for the project.

  4. Click Update Credentials.

Atlas displays a banner in the Atlas console during the Key Identifier
rotation process.

## Warning

Do not delete or disable the original Key Version Resource ID until your
changes have deployed.

If the cluster uses Back Up Your Database Deployment, do **not** delete or
disable the original Key Version Resource ID until you ensure that no
snapshots used that key for encryption.

### Alerts

Atlas resets the `encryption key rotation alert` timer at the completion of
this procedure.

## Related Topics

  * To enable Encryption at Rest using your Key Management when deploying an Atlas cluster, see Manage Your Own Encryption Keys.

  * To enable Encryption at Rest using your Key Management for an existing Atlas cluster, see Enable Encryption at Rest.

  * To learn more about Encryption at Rest using your Key Management in Atlas, see Encryption at Rest using Customer Key Management.

  * To learn more about MongoDB Encryption at Rest, see Encryption at Rest in the MongoDB server documentation.

  * To learn more about Encryption at Rest with Cloud Backups, see Storage Engine and Cloud Backup Encryption.

← Manage Customer Keys with Azure Key VaultSet Up Database Auditing →

