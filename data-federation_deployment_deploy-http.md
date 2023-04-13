Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create From the UI

Share Feedback

On this page

  * Prerequisites
  * Procedure

This page describes how to deploy a federated database instance for accessing
data in an HTTP data store.

## Note

### Beta

The support for HTTP data stores is available as a Beta feature. The feature
and the corresponding documentation may change at any time during the Beta
stage.

## Prerequisites

Before you begin, you will need to:

  * Create a MongoDB Atlas account, if you do not have one already.

  * Format your data store using one of the supported data formats.

## Note

If your file format is `CSV` or `TSV`, you must include a header row in your
data. See CSV and TSV for more information.

  * Make your data store accessible over the public internet.

## Important

  * If your HTTP data store is not accessible over HTTPS, you must use the JSON Editor to configure your data store. In your JSON configuration, you must set the `stores.[n].allowInsecure` setting to `true`.

  * Atlas Data Federation does not support HTTP data store URLs that require authentication.

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

  2. Click HTTP(S) to configure a federated database instance for data in an HTTP data store.

Corresponds to `stores.[n].provider` JSON configuration setting.

  3. Enter a name for your HTTP data store into the HTTP(S) Store Name field.

## Note

The data store's name must be unique within your federated database instance.

Corresponds to `stores.[n].name` JSON configuration setting.

  4. Enter the publicly accessible URL of the file where data is stored.

## Tip

Click Use Sample URL to add a sample HTTP data store.

For each additional HTTP data store that you want to add, click Add Another
URL, then enter the HTTP data store URLs.

Corresponds to `stores.[n].urls` JSON configuration setting.

  5. Click Next.

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

← HTTP URLAtlas Data Lake Datasets →

