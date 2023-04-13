Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Load File with `mongoimport`

Share Feedback

You can use `mongoimport` to import data from a `JSON` or a `CSV` file into
MongoDB Atlas cluster.

## Considerations

  * `mongoimport` uses strict mode representation for certain BSON types.

## Procedure

The following tutorial uses `mongoimport` to load data from a `JSON` file to
an Atlas cluster:

1

### Set up a database user in the target Atlas cluster.

To run `mongoimport` to write to Atlas cluster, you must specify a database
user that has readWrite privileges in the database into which to import data.
For example, a user with `Atlas admin` role provides these privileges.

If no such user exists, create the user:

  1. In the Security section of the left navigation, click Database Access. The Database Users tab displays.

  2. Click __ Add New Database User.

  3. Add an Atlas admin user.

2

### Open the connect dialog.

  1. Click Database in the top-left corner of Atlas.

  2. From the Database Deployments view, click Connect for the Atlas cluster into which you want to migrate data.

3

### Update IP Access List.

If the host where you will run `mongoimport` is not in the IP Access List,
update the list. You can specify either:

  * The public IP address of the server on which `mongoimport` will run, or

  * If set up for VPC peering, either the peer's VPC CIDR block (or a subnet) or the peer VPC's Security Group, if you chose AWS as your cloud provider.

4

### Copy the target cluster URI / host information.

You can connect to your Atlas cluster using its connection string URI. In the
connect dialog perform the following steps:

  1. Click Connect Your Application.

  2. Copy the connection string found in step 1.

  3. Replace **PASSWORD** with the password for the root user, and **DATABASE** with the name of the database to which you wish to connect.

## Important

You must escape any instances of the `@` character in the provided
`<PASSWORD>`. For example, `p@ssword` should be `p%40ssword`.

This connection string is specified to `mongoimport` in the `--uri` option.

When using `--host`, if the Atlas cluster is a replica set you must also
retrieve the replica set name. For example:

    
    
    myAtlasRS/atlas-host1:27017,atlas-host2:27017,atlas-host3:27017  
      
  
5

### Run mongoimport.

The following example imports data from the file
`/somedir/myFileToImport.json` into collection `myData` in the `testdb`
database. The operation includes the `--drop` option to drop the collection
first if the collection exists.

Using `--uri`:

    
    
    mongoimport --uri "mongodb://root:<PASSWORD>@atlas-host1:27017,atlas-host2:27017,atlas-host3:27017/<DATABASE>?ssl=true&replicaSet=myAtlasRS&authSource=admin" --collection myData --drop --file /somedir/myFileToImport.json  
      
  
Using `--host`:

    
    
    mongoimport --host myAtlasRS/atlas-host1:27017,atlas-host2:27017,atlas-host3:27017 --ssl -u myAtlasAdminUser -p 'myAtlasPassword' --authenticationDatabase admin  --db testdb --collection myData --drop --file /somedir/myFileToImport.json  
      
  
Add/edit the `mongoimport` command line options as appropriate for your
deployment. See `mongoimport` for more `mongoimport` options.

## Additional Information

For more information on `mongoimport`, including behavior, options, and
examples, see the `mongoimport reference page`.

← Seed with `mongorestore`Interact with Your Data →

