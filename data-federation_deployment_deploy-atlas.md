Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create From the UI

Share Feedback

On this page

  * Prerequisites
  * Procedure

This page describes how to deploy a federated database instance for accessing
data in an Atlas cluster.

## Prerequisites

Before you begin, you will need to:

  * Create a MongoDB Atlas account, if you do not have one already.

  * Create an Atlas Cluster, if you do not have one already. Atlas Data Federation supports Atlas clusters deployed to AWS, Azure, or Google Cloud.

## Note

To use your Atlas cluster as a data store, you must deploy it to the same
project as your federated database instance.

  * Add data to at least one collection on your Atlas cluster if you have not already.

## Procedure

1

### Log in to MongoDB Atlas.

2

### Select the Data Federation option on the left-hand navigation.

3

### Create a federated database instance.

  * For your first federated database instance, click Create a Federated Database.

  * For subsequent federated database instances, click Create Federated Database.

4

### Select the configuration method.

  * For a guided experience, click Visual Editor.

  * To edit the raw JSON, click JSON Editor.

5

### Specify your data store.

Visual Editor

JSON Editor

If you are using the Visual Editor:

  1. Click Add Data Sources in the Datasets section to choose your data store.

  2. Click Atlas Cluster to configure a federated database instance for data in an Atlas cluster.

Corresponds to `stores.[n].provider` JSON configuration setting.

  3. Specify the Atlas cluster that you want to use as a data store in the Provide Namespaces in this project section. To specify, select the cluster from the dropdown.

Corresponds to `stores.[n].clusterName` JSON configuration setting.

  4. Expand the databases and select the collections that you want to add to your federated database instance.

## Tip

To filter the databases and collections, enter text into the Search database
or collection field. The dialog displays only databases and collections with
names that match your search criteria.

Corresponds to the `databases.[n].collections.[n].dataSources.[n].database`
and `databases.[n].collections.[n].dataSources.[n].collection` JSON
configuration settings.

  5.  _Optional_. Specify the Cluster Read Preference settings by expanding the section.

Corresponds to `stores.[n].readPreference`.

Field Name

|

Description  
  
|  
  
Read Preference Mode

|

Specifies the replica set member to which you want to route the read requests.
You can choose one of the following from the dropdown:

    * `primary` \- to route all read requests to the replica set primary

    * `primaryPreferred` \- to route all read requests the replica set primary and to secondary members only if `primary` is unavailable

    * `secondary` \- to route all read requests to the secondary members of the replica set

    * `secondaryPreferred` \- to route all read requests to the secondary members of the replica set and the primary on sharded clusters only if `secondary` members are unavailable

    * `nearest` \- to route all read requests to random eligible replica set member, irrespective of whether that member is a primary or secondary

If you add an Atlas cluster as a store, the value default value is
`secondary`.

If you don't set anything in your federated database instance storage
configuration, the default value is `nearest`. To learn more, see Read
preference mode.

Corresponds to `stores.[n].readPreference.mode`.  
  
TagSets

|

Specifies the list of tags or tag specification documents that contain name
and value pairs for the replica set member to which you want to route read
requests. To learn more, see Read Preference Tag Sets.

Corresponds to `stores.[n].readPreference.tagSets`.  
  
Maxstaleness Seconds

|

Specifies the maximum replication lag, or “staleness”, for reads from
secondaries. To learn more, see Read Preference maxStalenessSeconds.

Corresponds to `stores.[n].readPreference.maxStalenessSeconds`.  
  
  6. Click Next.

6

### Create the virtual databases, collections, and views and map the
databases, collections, and views to your data store.

  1. (Optional) Click the __for the:

    * Data Lake to specify a name for your federated database instance. Defaults to `Data Lake[n]`.

    * Database to edit the database name. Defaults to `Database[n]`.

Corresponds to `databases.[n].name` JSON configuration setting.

    * Collection to edit the collection name. Defaults to `Collection[n]`.

Corresponds to `databases.[n].collections.[n].name` JSON configuration
setting.

    * View to edit the view name.

You can click:

    * Create Database to add databases and collections.

    *  __associated with the database to add collections to the database.

    *  __associated with the collection to add views on the collection. To create a view, you must specify:

      * The name of the view.

      * The pipeline to apply to the view.

## Note

The view definition pipeline cannot include the `$out` or the `$merge` stage.
If the view definition includes nested pipeline stages such as `$lookup` or
`$facet`, this restriction applies to those nested pipelines as well.

To learn more about views, see:

      * Views

      * db.createView

    *  __associated with the database, collection, or view to remove it.

  2. Select External from the dropdown in the Datasets section.

  3. Drag and drop the data store to map with the collection.

Corresponds to `databases.[n].collections.[n].dataSources` JSON configuration
setting.

7

### Click Save.

← Atlas ClusterGenerate Wildcard Collections →

