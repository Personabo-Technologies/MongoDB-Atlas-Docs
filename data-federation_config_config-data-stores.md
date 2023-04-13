Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Define Data Stores for a Federated Database Instance

Share Feedback

On this page

  * Data Federation Access
  * Privilege Actions
  * Set or Update Federated Database Instance Configuration
  * Validate Federated Database Instance Configuration
  * Generate Federated Database Instance Configuration
  * Retrieve Federated Database Instance Configuration
  * Generate Wildcard Collections

Creating a federated database instance starts with creating a storage
configuration in JSON format. The storage configuration defines your data
stores and maps those data stores to collections you can query.

Atlas Data Federation supports S3 buckets, Atlas clusters, and publicly
accessible URLs as data stores. You must define mappings in your federated
database instance to your S3 bucket, Atlas cluster, and HTTP data stores to
run queries against your data.

## Important

Information in your storage configuration is visible internally at MongoDB and
stored as operational data to monitor and improve the performance of Atlas
Data Federation. We recommend that you don't use PII in your configurations.

This page describes the administration commands you can use to set, update,
and retrieve federated database instance storage configuration. Other pages in
this section describe the settings you can define in your federated database
instance storage configuration for your various data stores:

  * AWS S3 Bucket

  * Atlas Cluster

  * HTTP URL

## Data Federation Access

When you create a federated database instance, you grant Atlas either read
only or read and write access to S3 buckets in your AWS account. To access
your Atlas clusters, Atlas uses your existing Role Based Access Controls. You
can view and edit the data storage configuration that maps data from your S3
buckets and Atlas clusters to federated database instances and virtual
collections.

## Privilege Actions

Privilege actions define the operations that you can perform on your federated
database instance. You can grant the following Atlas Data Federation
privileges:

  * When you create or modify custom roles from the Atlas User Interface

  * In the `actions.action` request body parameter when you create or update a custom role from the Atlas API

`sqlGetSchema`

    

Retrieve the schema stored for a collection or view using the `sqlGetSchema`
command.

`sqlSetSchema`

    

Set or delete the schema for a collection or view using the `sqlSetSchema`
command.

`viewAllHistory`

    

Retrieve details about the queries that were run in the past using
$queryHistory.

`outToS3`

    

Write data from any one of the supported federated database instance stores or
multiple supported federated database instance stores to your S3 bucket using
`$out`.

`storageGetConfig`

    

Retrieve your federated database instance storage configuration using the
storageGetConfig command.

`storageSetConfig`

    

Set or update your federated database instance storage configuration using the
storageSetConfig command.

## Set or Update Federated Database Instance Configuration

Once connected to the federated database instance, you can use the following
database commands to set or update the federated database instance
configuration:

    
    
    use admin  
      
    db.runCommand( { "storageSetConfig" : <config> } )  
  
Replace `<config>` with the configuration for the federated database instance.
You can validate your configuration before setting or updating the federated
database instance configuration by running the storageValidateConfig command.

To set or update the storage configuration through the Atlas UI:

1

### Log in to MongoDB Atlas.

2

### Select the Data Federation option on the left-hand navigation.

3

### Click Configuration for the federated database instance and choose the
configuration method:

  * For a guided experience, click Visual Editor.

  * To edit the raw JSON, click JSON Editor.

4

### Make necessary changes to the federated database instance storage
configuration.

Visual Editor

JSON Editor

To manage data stores in the storage configuration:

  * Click Add Data Store to add a new data store. To add an:

    * S3 data store, complete step 5 in Create From the UI.

    * Atlas data store, follow steps 5 to 7 in Create From the UI.

    * HTTP data store, follow steps 5 to 7 in Create From the UI.

    * Atlas Data Lake dataset, follow steps 5 and 6 in Create From the UI.

Corresponds to `stores` JSON configuration setting.

  * Click the __for the store to edit the data store name.

Corresponds to `stores.[n].name` JSON configuration setting.

  * Click __associated with the data store to remove the data store.

To manage databases in the storage configuration:

  * Click Create Database to add databases and collections.

Corresponds to `databases` JSON configuration setting.

  * Click the __for the database to edit the database name.

Corresponds to `databases.[n].name` JSON configuration setting.

  * Click __associated with the database to remove the database.

To manage collections and views in the storage configuration:

  * Click the __for the:

    * Collection to edit the collection name.

Corresponds to `databases.[n].collections.[n].name` JSON configuration
setting.

    * View to edit the view name and pipeline.

Corresponds to `databases.[n].views.[n].name` and
`databases.[n].views.[n].pipeline` JSON configuration settings respectively.

  * Click __associated with the:

    * Database to add collections to the database.

Corresponds to `databases.[n].collections` JSON configuration setting.

    * Collection to add views on the collection. To create a view, you must specify:

      * The name of the view.

      * The pipeline to apply to the view.

Corresponds to `databases.[n].views` JSON configuration setting.

  * Click __associated with the collection or view to remove the collection or view.

5

### Click Save.

You can also set and manage the storage configuration using the Manage a
Federated Database Instance.

## Validate Federated Database Instance Configuration

You can run the following command to validate your federated database instance
configuration.

    
    
    use admin  
      
    db.runCommand( { "storageValidateConfig" : <config> } )  
  
Replace `<config>` with the configuration for the federated database instance.

The command returns the following if your federated database instance
configuration is valid:

    
    
    { "ok" : 1 }  
      
  
The command returns the list of errors in the `errs` field if your federated
database instance storage configuration is invalid:

    
    
    {  
      
           "ok" : 1,  
           "errs" : [  
                   "<error>",  
                   "<error>",  
                   ...  
           ]  
    }  
  
## Generate Federated Database Instance Configuration

You can run the `storageGenerateConfig` command to regenerate a federated
database instance configuration. The command returns an automatically
generated configuration, which you can then modify and upload. In the
automatically generated configuration, Federated Database Instance regenerates
a database for each store:

  * The `databases.[n].name` will be the same as the `stores.[n].name` that it maps to.

  * Each database will contain up to 3 collections and a wildcard (`*`) collection.

As a result, the databases array in the generated configuration might be
different from the databases array in your existing configuration.

## Note

You must have the `storageSetConfig` privilege to run the
`storageGenerateConfig` command. The atlasAdmin role has the
`storageSetConfig` privilege by default.

To generate a configuration for a federated database instance, connect to the
federated database instance and run the following database commands:

    
    
    use admin  
      
    db.runCommand( { "storageGenerateConfig" : 1 } )  
  
## Retrieve Federated Database Instance Configuration

Once connected to the federated database instance, you can use the following
database commands to retrieve the federated database instance configuration:

    
    
    use admin  
      
    db.runCommand( { "storageGetConfig" : 1 } )  
  
The command returns the current federated database instance configuration.

## Generate Wildcard Collections

You can dynamically generate collection names that map to data in your S3
bucket or Atlas cluster. To dynamically generate collection names, specify the
wildcard, `*`, as the value for the collection name setting in your federated
database instance storage configuration. You can't dynamically generate
collection names in your federated database instance storage configuration
that map to data in your HTTP or HTTPS data store.

You can use the storageSetConfig command to configure the settings for
generating wildcard (`*`) collections.

To learn more about the configuration settings for generating wildcard
collections, see:

  * Generate wildcard collections for data in AWS S3 buckets

  * Generate wildcard collections for data in Atlas cluster

← Run Queries Against Your Federated Database InstanceAWS S3 Bucket →

