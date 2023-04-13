Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Storage Engine and Cloud Backup Encryption

Share Feedback

Atlas encrypts all snapshots using your cloud provider's standard storage
encryption method, ensuring the security of cluster data at rest. Your cloud
provider manages the encryption keys. For projects and clusters using
Encryption at Rest using Customer Key Management, Atlas applies an additional
layer of encryption to your snapshots using the Key Management Service (KMS)
provider configured for the cluster.

AWS Identity and Access Management (IAM)

Azure Key Vault

Google Cloud KMS

For clusters using AWS IAM as their Key Management Service, Atlas uses the
project's customer master key (CMK) and AWS IAM user or role credentials at
the time of the snapshot to automatically encrypt the snapshot data files.
This is an additional layer of encryption on the existing encryption applied
to all Atlas storage and snapshot volumes. Oplog data collected for PIT
restores is also encrypted with the customer's CMK.

Atlas stores the unique ID of the CMK and the AWS IAM user credentials or
roles used to access the CMK. Atlas uses this information when restoring the
snapshot. For complete documentation on restoring an encrypted snapshot, see
Restore from a Snapshot Using Encryption at Rest.

To view the key used to encrypt a snapshot:

  1. Click Database in the top-left corner of the {atlas-ui+}.

  2. From the Database Deployments view of the Atlas UI, click the cluster name.

  3. Click the Backup tab, then click Snapshots.

  4. Note the Encryption Key ID for each snapshot in the cluster. Atlas lists the Key Identifier used to encrypt the snapshot. Unencrypted snapshots display Not enabled.

## Important

Atlas requires access to the encryption key associated to the snapshot's
Encryption Key ID to successfully restore that snapshot.

Before deleting an Encryption Key ID used with Atlas Encryption at Rest using
your Key Management, check **every** backup-enabled cluster in the project for
any snapshots still using that Encryption Key ID. Once you delete an
encryption key, all snapshots encrypted with that key become inaccessible and
unrecoverable.

Atlas automatically deletes backups in accordance to the Backup Scheduling,
Retention, and On-Demand Snapshots. Once Atlas deletes all snapshots depending
on a given Encryption Key ID, you can delete the key safely.

If disabling a Encryption Key ID, you must re-enable the key before restoring
a snapshot encrypted with that key.

For complete documentation on configuring Encryption at Rest using your Key
Management for an Atlas project, see Encryption at Rest using Customer Key
Management. You can then either deploy a new cluster or enable an existing
cluster with Encryption at Rest using your Key Management.

← Configure a Backup Compliance PolicyExport Cloud Backup Snapshot →

