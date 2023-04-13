Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Oplog Access

Share Feedback

On this page

  * Add a User with Oplog Access
  * Access the Oplog

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

The oplog, a special capped collection, records operations that modify the
data stored in your databases.

## Add a User with Oplog Access

To access the oplog, a database user must have read access on the `local`
database. To create a user with read access on `local`:

  1. In the Security section of the left navigation, click Database Access.

  2. Click the Database Users tab.

  3. Click __ Add New Database User and enter a user name such as `oploguser`.

  4. Click Grant Specific Privileges and select the `read` role and the `local` database. This restricts the user to read operations on the `local` database.

  5. Enter a password and click Add User.

## Access the Oplog

  1. Connect to your cluster with the `mongosh`, using the credentials of the new database user with access to the `local` database.

  2. Switch to the `local` database.
    
        > use local  
      
  
  3. The oplog collection is named `oplog.rs`. Database write operations are recorded in date order, with a timestamp field and a wall clock field.

The timestamp field contains an integer with seconds since epoch.

## Note

  * To increase the size of an oplog for a cluster, see Set Oplog Size.

  * You cannot use the MongoDB command replSetResizeOplog to resize the oplog.

← Commands Available Only in Free ClustersHost Metrics →

