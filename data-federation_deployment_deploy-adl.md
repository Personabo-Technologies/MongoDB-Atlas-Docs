Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create From the UI

Share Feedback

On this page

  * Prerequisites
  * Procedure

This page describes how to deploy a federated database instance for accessing
data in an Atlas Data Lake dataset.

## Prerequisites

Before you begin, you will need:

  * An Atlas Data Lake dataset in the same project where you intend to create the federated database instance.

  * `Project Owner` role for the project where you want to create the federated database instance.

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

### Specify your Data Lake data store and configure virtual databases and
virtual collections that map to your data store.

Visual Editor

JSON Editor

  1. (Optional) Click the __for the:

    * Federated Database to specify a name for your federated database instance. Defaults to `Federated Database[n]`.

    * Database to edit the database name. Defaults to `Database[n]`.

Corresponds to `databases.[n].name` JSON configuration setting.

    * Collection to edit the collection name. Defaults to `Collection[n]`.

Corresponds to `databases.[n].collections.[n].name` JSON configuration
setting.

    * View to edit the view name.

You can click:

    * Add Database to add databases and collections.

    *  __associated with the database to add collections to the database.

    *  __associated with the collection to add views on the collection. To create a view, you must specify:

      * The name of the view.

      * The pipeline to apply to the view.

## Note

The view definition pipeline can't include the `$out` or the `$merge` stage.
If the view definition includes nested pipeline stages such as `$lookup` or
`$facet`, this restriction applies to those nested pipelines as well.

To learn more about views, see:

        * Views

        * db.createView

      *  __associated with the database, collection, or view to remove it.

  2. Drag and drop the Data Lake Dataset to map with the collection.

Corresponds to `databases.[n].collections.[n].dataSources` JSON configuration
setting.

6

### Click Save to create the federated database instance with virtual
databases, collections, and views mapped to your Data Lake dataset.

← Atlas Data Lake DatasetsAdminister Federated Database Instances →

