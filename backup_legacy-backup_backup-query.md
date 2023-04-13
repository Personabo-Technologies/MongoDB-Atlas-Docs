Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Query a Legacy Backup Snapshot

Share Feedback

On this page

  * Considerations
  * Query Backup (Use Tunnel to Connect)
  * Query Backup (Handle TLS and Authentication Manually)

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

Atlas supports querying a legacy backup snapshot. This functionality allows
you to query specific legacy backup snapshot. You can use the queryable
backups to:

  * Restore a subset of data within the MongoDB cluster.

  * Compare previous versions of data against the current data.

  * Identify the best point in time to restore a system by comparing data from multiple legacy backups.

## Note

You must have the `Project Owner` role for an Atlas project to query a
snapshot for a cluster in that project.

## Considerations

  * Atlas does not support querying Cloud Backups.

  * Atlas provisions these queryable snapshots as _read-only_ MongoDB instances.

## Important

### These instances are available for up to 24 hours.

  * Query restrictions:

    * You cannot run map-reduce operations.

    * You cannot run queries that requires disk usage, such as running aggregation with the `allowDiskUse` option to perform large sort operations.

  * Connections to these instances are over TLS/SSL and require a X.509 authentication. Atlas provides:

    * An executable to create a tunnel which handles the connection, including the TLS/SSL and the X.509 authentication.

    * X.509 certificates if you want to handle the connection details manually, including the TLS/SSL and the X.509 authentication.

## Query Backup (Use Tunnel to Connect)

## Note

The tunnel handles the security (TLS/SSL and X.509 authentication) for
connecting to the instance.

1

### Go to Backup view and click the Overview tab.

For the cluster whose backup you want to query, click the ellipsis button
under Options column and select Query.

You can also click the cluster to view its snapshots and click the Query
button under the Actions column.

2

### Follow the prompts to query a backup snapshot.

  1. Select the snapshot to query and click Next.

  2. Start the process to query a snapshot. If prompted for your password, enter your password to verify.

  3. Select Backup Tunnel as the connection method to the queryable snapshot.

  4. Select your Platform and download.

  5. Uncompress the downloaded file.

  6. Open a terminal or command prompt and go to the uncompressed <tunnel> directory. Run the executable to start the tunnel.

The default port for the tunnel is `27017`. To change the port, use the
`--local` flag, as in the following example:

    
        ./<tunnel executable> --local localhost:27020  
      
  
## Note

If you change the port, you must include the port information when connecting.

  7. Use the `mongo` shell or a MongoDB driver to connect to the backup via the tunnel.

    * If connecting locally from the same machine as where the tunnel is running, you do not need to specify a connection string or host information. Otherwise, specify a connection string or host information for the machine where the tunnel is running.

    * If you have changed the port that the tunnel is listening on, you must specify the port information when connecting.

## Tip

Once you have finished querying this snapshot, you can terminate the queryable
instance:

  1. Go to the Restores & Downloads tab and hover over the Status column for the cluster.

  2. Click Cancel.

## Query Backup (Handle TLS and Authentication Manually)

## Note

The X.509 certificates are valid for 24 hours.

1

### Go to Backup view and click the Overview tab.

For the cluster whose backup you want to query, click the ellipsis button
under Options column and select Query.

You can also click the cluster to view its snapshots and click the Query
button under the Actions column.

2

### Follow the prompts to query a backup snapshot.

  1. Select the snapshot to query and click Next.

  2. Start the process to query a snapshot. If prompted for your password, enter your password to verify.

  3. Select Connect Manually as the connection method to the queryable snapshot.

  4. Download the X.509 client PEM file.

  5. Download the Certificate Authority (CA) PEM file.

  6. Use `mongosh` or a MongoDB driver to connect to the queryable backup host. To connect, you must specify the hostname and port, the TLS/SSL option, and the X.509 certificates.

For example, if using `mongosh` to connect to the instance:s

    
        mongosh my-queryable-backup-host.mongodb.com:27217 --ssl --sslPEMKeyFile <client certificate> --sslCAFile mms-backup-ca.pem  
      
  

## Tip

Once you have finished querying this snapshot, you can terminate the queryable
instance:

  1. Go to the Restores & Downloads tab and hover over the Status column for the cluster.

  2. Click Cancel.

← Restore a Cluster from a Legacy Backup SnapshotRestore a Database from
Queryable Legacy Backup →

