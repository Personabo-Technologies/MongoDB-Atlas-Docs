Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Troubleshoot Live Migration (Pull)

Share Feedback

On this page

  * Common Live Migration (Pull) Validation Errors
  * Common Post-Validation Errors

Before the live migration (pull) process begins, Atlas performs a validation
check to ensure that all the necessary form fields and parameters are
functional and correct. If any parameters are invalid, Atlas returns an error
and live migration does not proceed.

This section describes common live migration (pull) validation errors and
provides suggestions for what to check if you encounter them.

## Common Live Migration (Pull) Validation Errors

Error

|

Remediation  
  
|  
  
Could not reach specified source

|

  * Ensure that you added the correct subnet ranges to the IP access list on the source cluster. You can find the four required subnet ranges in the live migration modal window.

  * Confirm that the hostname that you specified resolves to a public IP address. At a command prompt, use one of the following commands:
    
        | nslookup <hostname>  
      
    ping <hostname>  
  
  * Ensure that you are not using a VPC Peering Connection, which is not compatible with pull live migration. If a VPC Peering Connection is your only option, use mongomirror instead.

  
  
Could not resolve hostname

|

No IP address was found for the given hostname. Confirm that the given
hostname is correct and publicly accessible.  
  
Invalid SSL options provided

|

If you are using SSL:

  * Confirm that your SSL certificate is complete and correctly copied to the live migration (pull) modal window.

  * Confirm that the Is SSL enabled? toggle switch is in the `Yes` position.

If you are not using SSL:

  * Check your connection string and confirm that the `ssl` query parameter is not present. If `--ssl` is part of your connection string, your cluster requires an SSL connection.

  * Confirm that the Is SSL enabled? toggle switch is in the `No` position.

  
  
The username or password is not correct

|

Confirm your credentials in `mongosh` with the following commands:

    
    
    | use admin  
      
    db.getUser("<username>");  
  
If the issue persists, update the MongoDB user's password.  
  
User not authorized to execute command

|

To run the live migration (pull) process, the MongoDB user must have
sufficient system privileges. To learn more, see Source Cluster Security.  
  
Disk storage info unavailable

|

To run the live migration (pull) process, the MongoDB user must have
permissions on the source cluster's MongoBD instance. To learn more, see
Source Cluster Security.  
  
Source disk usage is too large for destination

|

Different Atlas service tiers have different amounts of disk space available.
Ensure that your Atlas cluster has enough disk space for all the data on your
source cluster. To learn more about cluster sizings, see Create a New Cluster.  
  
Source appears to be a standalone

|

Your source deployment must be a MongoDB replica set. If your source
deployment is currently a standalone node, convert it to a single-node replica
set before running live migration (pull).  
  
Unable to process the provided CA file

|

Confirm that your CA file is complete and correctly pasted into the live
migration (pull) modal window.  
  
## Common Post-Validation Errors

Error

|

Remediation  
  
|  
  
Could not retrieve the latest oplog entry from the source: not found

|

  * If the source is a replica set, make sure you have read access on the local database.

  * If the source is a standalone instance, convert it to a replica set before proceeding with the migration.

  * Confirm that the source cluster has a readable oplog. On some hosted services, such as Compose.io, the oplog is a feature which must be enabled.

  * If you still cannot access the oplog, use mongorestore instead to import your data into Atlas.

  
  
Could not determine if --host is a replica set: error connecting to db server:
no reachable servers

|

  * Ensure that you added every IP address the live migration (pull) service requires to the IP access list for your source cluster.

  * Confirm that the IP address or DNS hostname you provided resolves to an IP address that is publicly accessible.

  
  
Error applying oplog entries during initial sync: renameCollection command
encountered during initial sync. Please restart `mongomirror`.

|

Renaming a collection on the source cluster during live migration (pull) may
trigger this error.

  * Ensure that no users or applications rename any collections while the live migration (pull) is taking place.

  * Aggregation operations which use $out may trigger this error. Ensure that no `$out` operations occur during the live migration (pull) procedure.

  
  
Unsupported index error

|

Certain types and configurations of indexes which were allowable in earlier
versions of MongoDB are no longer supported in more recent versions. Check the
release notes for the MongoDB version on your destination cluster for possible
conflicts. If necessary, drop any indexes which cause errors and rebuild them
after the live migration process is complete.  
  
Error while tailing the oplog on the source: Checkpoint not available in oplog

|

Live migration (pull) uses the source oplog to sync operations which occur on
the source cluster during the pull live migration procedure. If the source
cluster oplog size is too small, it might not be able to record all the
operations that occur on the source cluster during the sync, and live
migration (pull) falls too far behind to catch up.

If you see this error:

  * Check the size of the source cluster oplog using the rs.printReplicationInfo() command. The server that is hosting `mongomirror` must have enough available disk space to contain the oplog data generated during the migration process.

  * If required, increase the size of the source oplog to support a replication window that is long enough to complete the live migration procedure.

  * If the error occurs when running `mongomirror` directly, restart `mongomirror` using `--oplogPath` to buffer oplog data to disk during the migration.

