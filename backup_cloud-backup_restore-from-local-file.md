Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore from a Locally-Downloaded Snapshot

Share Feedback

On this page

  * Restore Considerations
  * Procedure
  * Considerations
  * Click Legacy Backup in the left navigation.
  * Chose the cluster you want to download a backup snapshot of.
  * Select the snapshot you want to download, then click Next.
  * Click Download.
  * Click Download or copy the download link.
  * Use your preferred archive utility to extract the archive and access the data files.
  * Restore a Cloud Manager Snapshot to Atlas

Atlas provides a mechanism for downloading dedicated cluster, shared cluster,
and legacy backup snapshots as compressed files.

## Restore Considerations

  * You must have the `Project Owner` role for the Atlas projects that contain the source and target database deployments to restore data from one Atlas database deployment to another.

  * If the `DefaultRWConcern` value on the source snapshot differs from the `DefaultRWConcern` value on the target database deployment, Atlas overrides the value on the source snapshot with the value on the target database deployment. If there is no value configured for the `DefaultRWConcern` on the target database deployment, Atlas keeps the value of `DefaultRWConcern` from the snapshot without explicit configuration. This may differ from the default value for that MongoDB version.

  * This feature is unavailable for `M0` clusters and for serverless instances.

  * The downloaded files consist of the raw files copied from the `data` directory. `mongorestore` is incompatible with these files. To access the data files, use the following procedure to start a `mongod` instance and point it to the extract directory.

## Procedure

## Important

Atlas deletes all existing data on the target database deployment prior to the
restore. The cluster will be **unavailable** for the duration of the restore.

Cloud Backups

Legacy Backup

To learn more about this backup type, see Back Up Your Database Deployment.

### Considerations

When you manually download a cloud backup snapshot, your download might get
interrupted for some reason. Atlas keeps the request alive and allows you to
restart it as long as the most recent download failure occurred no more than
one hour ago.

1

#### Request your snapshot.

  1. Click Database.

  2. Click the name of your Atlas Cluster.

  3. Click the Backup tab.

  4. Click the Snapshots sub-tab.

  5. Click Download.

Atlas generates a one-time use download link that expires within 1 hour after
its creation.

The amount of time to create this link increases with the size of the Atlas
cluster.

Once the download is ready, Atlas:

  * Emails you an alert that your snapshot download is ready.

  * Displays the download link in the Restores & Downloads tab.

## Note

### Available via API

As another option, you can request a restore snapshot using the API.

2

#### Add the IP or CIDR address of the client to your Atlas project IP access
list.

If the current project IP access list ranges do not cover the target client IP
or CIDR address, click Add or Modify your IP Addresses to make changes to your
Atlas project IP access list.

3

#### Retrieve your snapshot.

  1. Click Database.

  2. Click the name of your Atlas Cluster.

  3. Click the Backup tab.

  4. Click the Restores & Downloads sub-tab.

  5. Navigate to the restore snapshot you created.

  6. Click Download.

4

#### Use your preferred archive utility to extract the archive and access the
data files.

Atlas compresses the snapshot into a `.tar.gz` file. This archive includes the
snapshot and the `mongod` logs.

  1. Extract the files in the archive.

## Example

The following command uses the `tar` utility to extract a `tar``archive with
``gzip` compression.

    
        tar -xvzf ~/Downloads/mongodb-snapshots/my-cluster-snapshot.tar.gz  
      
  
  2. Access the data files by starting a `mongod` instance on the host and pointing it at the extract directory using the `--dbpath` option.

## Example

The following command starts a `mongod` instance using the extracted data file
directory:

    
        mongod --dbpath ~/Downloads/mongodb-snapshots/my-cluster-snapshot/  
      
  

## Restore a Cloud Manager Snapshot to Atlas

You can automatically restore a backup for a Cloud Manager deployment to an
Atlas deployment. Before you restore a snapshot from a Cloud Manager
deployment to an Atlas deployment, ensure that the hosts for your Atlas
deployment have sufficient storage space for the restored databases, plus
additional space for dataset growth. Use db.stats() to find the current
database size.

The MongoDB server version must be one of the following:

  * The same on both deployments.

  * One version higher on the Atlas deployment.

Also, the instance types of the nodes in the Atlas deployment should have at
least as much memory and throughput capacity as the nodes in the Cloud Manager
deployment.

To learn more, see Restoring a Deployment to MongoDB Atlas.

← Restore from Continuous Cloud BackupRestore from a Snapshot Using Encryption
at Rest →

