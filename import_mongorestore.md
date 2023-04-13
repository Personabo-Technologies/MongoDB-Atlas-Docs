Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Seed with `mongorestore`

Share Feedback

You can use `mongodump` and `mongorestore` to seed MongoDB Atlas cluster with
data from an existing MongoDB standalone or replica set. For guidance on
seeding data from an existing MongoDB sharded cluster, contact Atlas support
by clicking Support in the left-hand navigation of the Atlas UI.

While you can scale an `M0` Free Tier cluster to an `M10+` paid cluster using
the Atlas UI, you can also use `mongodump` and `mongorestore` procedures in
this section to copy data from an `M0` Free Tier cluster to an `M10+` cluster.

## Considerations

### Recommended `mongodump` and `mongorestore` Version

Use the latest stable release version of `mongodump` and `mongorestore` for
this procedure.

### Downtime Required

To ensure an up-to-date migration, schedule a maintenance window where you can
stop all writes to your source cluster. Any write operations issued to the
source cluster after the `mongodump` portion of the procedure completes are
not migrated to the target cluster.

After `mongorestore` completes data restoration, you must cut-over your
applications to the target Atlas cluster before resuming write operations. To
connect to an Atlas cluster, see Connect to a Database Deployment.

The total amount of required downtime depends on factors such as the size of
data being migrated and the network connection between your source cluster and
Atlas. If you have questions or concerns about extended downtime, contact
Atlas support by clicking Support from the left-hand navigation of the Atlas
UI.

For a guided minimal-downtime migration procedure, see Replica Set Live
Migration or Sharded Cluster Live Migration.

### Cluster Security

Atlas manages database user creation. If the source cluster enforces
authentication:

  * Allow read access to the primary.

  * If you want to use `mongorestore` with the `--oplogReplay` option, you must delete the `admin` and `config` directories from the `dump` directory that `mongodump` creates. The `admin` and `config` directories contain database user information that you can't add to an Atlas cluster with `mongorestore`. Use the `mongorestore` `--nsExclude` to exclude the `admin.system.*` namespace.

You can't migrate any existing user or role information to Atlas. For the
target Atlas cluster, create the appropriate database users for supporting
your application's usage patterns. Update your applications as part of the
cut-over procedure to use the new database users. To learn more, see Configure
Database Users.

### Performance

This procedure requires running `mongodump` and `mongorestore` on a host in
the source cluster. These programs use system resources such as CPU and
memory, and may impact the performance of the host.

Run this procedure during non-peak system usage, or during a scheduled
maintenance window. If the source is a replica set, you can run this procedure
from the host of a secondary member. After stopping writes to the cluster,
allow the secondary to catch up to the primary before starting this procedure.

### Pipe Behavior

This procedure uses linux pipes to stream the output of `mongodump` to
`mongorestore`. If the `mongorestore` process can't keep up with the
`mongodump` process, you may see broken pipe errors.

For guidance on addressing persistent broken pipe errors, contact Atlas
support by clicking Support from the left-hand navigation of the Atlas UI.

## Procedure

The following tutorial uses `mongodump` and `mongorestore` to upload data from
an existing MongoDB cluster to an Atlas cluster:

1

### Optional: Create a database user in the source replica set.

## Important

### Optional

If your source cluster _doesn't_ enforce authentication, skip this step.

If the source deployment enforces authentication, you must provide a database
user with privileges to read any database as part of this procedure. To learn
more about database user privileges, see MongoDB Role-Based Access Control.

If no such user exists, create a user in your source MongoDB replica set with
the backup role on the `admin` database.

## Example

Run the following command in `mongosh` to create the `mySourceUser` on the
`admin` database and assign it the `backup` role. For replica sets, you must
run this command against the primary.

    
    
    use admin  
      
    db.createUser(  
      {  
         user: "<mySourceUser>",  
         pwd: "<mySourcePassword>",  
         roles: [ "backup" ]  
      }  
    )  
  
2

### Assemble the `mongodump` command.

Based on the type of connection string you use, copy one of the following
templates to into your preferred text editor:

## Note

To connect to Atlas clusters, we recommend you connect with a DNS seed list
connection string using the `--uri` option.

Connect with a standard connection string

Connect with a DNS seed list connection string

    
    
    mongodump --uri "mongodb://username:password@mongodb0.example.com:<Port>,mongodb1.example.com:<Port1>,mongodb2.example.com:<Port2>/?replicaSet=<ReplicaSetName>&authSource=admin" \  
      
              --archive  
  
Replace the host examples with the information for your replica set members.
Replace `<ReplicaSetName>` with the name of the source replica set.

For standalone deployments, exclude `replicaSet=<ReplicaSetName>` and specify
the hostname of the standalone deployment only. For example, `--uri
"mongodb://standalone-mongod.example.net:27017"`

## Note

If your password contains special characters, it must be percent-encoded.

Do not run this command yet. Proceed to the next step once you have modified
the template.

3

### Set up database user in the target Atlas cluster.

To run `mongorestore` against an Atlas cluster, you must specify a database
user in the Atlas cluster that has the `Atlas admin` role.

If no such user exists, create the user:

  1. If it is not already displayed, select your desired organization from the __ Organizations menu in the navigation bar.

  2. Click Access Manager in the sidebar, or click Access Manager in the navigation bar, then click your organization.

  3. Click __ Add New Database User.

  4. Add an Atlas admin user.

To learn more about user management, see Configure Database Users.

4

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

5

### Choose Command Line Tools for your desired cluster.

From the __menu for the cluster, click Command Line Tools.

6

### Retrieve and modify the `mongorestore` connection template.

The Binary Import and Export Tools section of the Command Line Tools tab
displays a copyable template with the minimum required options for connecting
`mongorestore` to your Atlas cluster.

The template includes placeholder values for certain options. Copy and paste
the template into your preferred text editor and make the following
modifications:

  * `password`: replace this with the password for the user specified in `username`. The template includes a database user for the project as the `username`. If you want to authenticate as a different user, replace the value of `username` and specify the password for that user in `password`.

  * Add `--nsExclude` and set its value to `"admin.system.*"`.

  * Add `--archive`.

Based on the type of connection string you use, your template should resemble
one of the following commands:

Connect with a standard connection string

Connect with a DNS seed list connection string

    
    
    mongorestore --uri "mongodb://username:password@00.foo.mongodb.net:27017,01.foo.mongodb.net:27017,02.foo.mongodb.net:27017/?replicaSet=myRepl&authSource=admin" \  
      
                 --archive \  
                 --ssl \  
                 --nsExclude "admin.system.*"  
  
7

### Run `mongodump` and `mongorestore`.

## Important

Ensure that the host where you are running `mongodump` and `mongorestore` is
in the project IP Access List.

To review your project IP access list, click Network Access in the Security
section of the sidebar. The IP Access List tab displays.

## Tip

### See also:

IP Access List

In your preferred text editor, use the pipe `|` operator to separate the
`mongodump` and `mongorestore` commands. Based on the type of connection
string you use, the final command should resemble one of the following:

Connect with a standard connection string

Connect with a DNS seed list connection string

    
    
    mongodump --uri "mongodb://username:password@mongodb0.example.com:27017,mongodb1.example.com:27017,mongodb2.example.com:27017/?replicaSet=sourceRS&authSource=admin" \  
      
              --archive \  
    | \  
    mongorestore --uri "mongodb://username:password@00.foo.mongodb.net:27017,01.foo.mongodb.net:27017,02.foo.mongodb.net:27017/?replicaSet=myAtlasRS&authSource=admin" \  
                 --archive \  
                 --ssl \  
                 --nsExclude "admin.system.*"  
  
Run the completed command from a terminal or shell connected to a host machine
on your source cluster.

Upon successful completion of the procedure, connect to your Atlas cluster
using `mongosh` and verify the result of the procedure. To learn how, see
Connect via `mongosh`.

You must update your applications to point to the Atlas cluster before
resuming write operations. To learn how to connect applications to Atlas, see
Connect via Your Application.

## Tip

### See also:

  * `mongodump reference page`

  * `mongorestore reference page`

← mongomirror Previous VersionsLoad File with `mongoimport` →

