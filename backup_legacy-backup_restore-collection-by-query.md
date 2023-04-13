Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Restore a Collection from Queryable Legacy Backup

Share Feedback

On this page

  * Prerequisites
  * Procedure

## Important

### Legacy Backup Deprecated

Effective 23 March 2020, all new clusters can _only_ use Cloud Backups.

When you upgrade to 4.2, your backup system upgrades to cloud backup if it is
currently set to legacy backup. After this upgrade:

  * All your existing legacy backup snapshots remain available. They expire over time in accordance with your retention policy.

  * Your backup policy resets to the default schedule. If you had a custom backup policy in place with legacy backups, you must re-create it with the procedure outlined in the Cloud Backup documentation.

Atlas supports restoring a collection by querying a legacy backup snapshot.

## Important

Atlas doesn't support querying Cloud Backups.

You can use a queryable backup snapshot to export data for a collection and
restore to the target deployment. The following procedure connects to the
queryable backup instance via an Atlas-provided tunnel.

## Note

You must have the `Project Owner` role for the Atlas projects that contain the
source and target clusters to restore data from one Atlas cluster to another.

## Prerequisites

### Client Operations during Restoration

You must ensure that the target Atlas cluster doesn't receive client requests
during restoration. The following use cases apply:

  * If you plan to restore to the same database, you must stop the client operations during restoration.

  * If you plan to restore to a different database, you don't need to stop the client applications. In this case, you can restore to a new Atlas cluster and reconfigure your application to use that new cluster once the new deployment is running.

## Procedure

1

### Navigate to the Legacy Backup page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Project menu in the navigation bar.

  3. Click Legacy Backup in the sidebar.

2

### Select the snapshot to query.

The Overview tab on the Legacy Backup page lists the project's clusters.

  * If backup is enabled for the cluster, the Status is Active.

  * If backup is disabled for the cluster, the Status is Inactive.

For the deployment whose backup you want to query, click the ellipsis in the
Options column and select Query.

You can also click View All Snapshots to view its snapshots and click Query
under the Actions column for the desired snapshot.

3

### Open a Backup Tunnel to the Queryable Snapshot.

  1. Select the snapshot to query and click Next.

  2. Start the process to query a snapshot. You will be prompted to enter your Atlas password.

  3. Select Backup Tunnel as the connection method to the queryable snapshot.

  4. Select your Platform.

  5. Click Download Backup Tunnel.

  6. Uncompress the downloaded file.

  7. Open a terminal or command prompt and go to the uncompressed <tunnel> directory. Run the executable to start the tunnel.

The default port for the tunnel is `27017`. To change the port, use the
`--local` flag, as in the following example:

    
        ./<tunnel executable> --local localhost:27020  
      
  
## Note

If you change the port, you must include the port information when connecting.

4

### Use `mongodump` to export a single collection from the queryable backup.

To export the data for a collection:

    

Include the following options to connect to the tunnel:

  * `--port` set to the port for the tunnel.

  * `--db` set to the name of the database to export.

  * `--collection` set to the name of the collection to export.

  * `--out` set to an empty directory to output the data dump.

## Important

Ensure that the user running `mongodump` can write to the specified directory.

    
    
    mongodump --port <port for tunnel> --db <single-database> --collection <collection-name> --out <data-dump-path>  
      
  
For example, to connect to a tunnel running on port `27020` to dump out data
from the `restaurants` collection from `test` database to
`/mydata/restoredata/` directory:

    
    
    mongodump --port 27020 --db test --collection restaurants --out /mydata/restoredata/  
      
  
`mongodump` outputs the `restaurants` collection data into the
`/mydata/restoredata/test/restaurants.bson` file.

5

### Use `mongorestore` to restore the single collection.

To restore a single collection:

    

Include the following `mongorestore` options:

## Note

To restore to an Atlas cluster, we recommend you connect with a DNS seed list
using the `--uri` option.

  * `--uri` set to the connection string for the destination cluster.

  * `--db` set to the name of the destination database.

  * `--collection` set to the name of the destination collection.

Optionally, you can include the `--drop` option to drop the collection in the
destination cluster if the collection already exists.

    
    
    mongorestore --uri "mongodb+srv://username:password@cluster0.example.mongodb.net" --db <destination-database> --collection <destination-collection> <data-dump-path/dbname/collection.bson> --drop  
      
  
For example, to restore from the `/mydata/restoredata/test/restaurants.bson`
data file to a new collection `rest2` in the `test2` database:

    
    
    mongorestore --uri "mongodb+srv://username:password@cluster0.example.mongodb.net" --db test2 --collection rest2 /mydata/restoredata/test/restaurants.bson --drop  
      
  
6

### Terminate the queryable instance.

Once you have finished, you can terminate the queryable instance:

  1. Click Backup in the left navigation pane and click the Restores & Downloads tab.

  2. Hover over the Status column for the target deployment item and click Cancel.

  3. Click Cancel Restore Job.

7

### Restart your appplication.

Restart your application and ensure it uses the new target cluster.

← Restore a Database from Queryable Legacy BackupManage Database Deployments →

