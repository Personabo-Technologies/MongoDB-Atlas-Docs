Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Create an Atlas Search Index

Share Feedback

On this page

  * Prerequisites
  * Create an Atlas Search Index Using the Atlas UI
  * Create an Atlas Search Index Using the Atlas Search API
  * Create an Atlas Search Index Using the Atlas CLI
  * Node Status

Atlas Search index is a data structure that categorizes data in an easily
searchable format. It is a mapping between terms and the documents that
contain those terms. Atlas Search indexes enable faster retrieval of documents
using certain identifiers. You must configure an Atlas Search index to query
data in your Atlas cluster using Atlas Search.

You can create an Atlas Search index on a single field or on multiple fields.
We recommend that you index the fields that you regularly use to sort or
filter your data in order to quickly retrieve the documents that contain the
relevant data at query-time.

You can create an Atlas Search index for all collections except time series
collections on your Atlas cluster through the Atlas UI, API, Atlas CLI, and
Terraform.

## Important

If you use the $out aggregation stage to modify a collection with an Atlas
Search index, you must delete and re-create the search index. If possible,
consider using $merge instead of `$out`.

## Prerequisites

To create an Atlas Search index, you must have an Atlas cluster with:

  * MongoDB version `4.2` or higher

  * Collection to create the Atlas Search index for

The following table shows the modes of access each role supports.

Role

|

Action

|

Atlas UI

|

Atlas API

|

Atlas Search API

|

Atlas CLI  
  
|||||  
  
`Project Data Access Read Only` or higher role

|

To view Atlas Search analyzers and indexes.

|

✓

|

✓

|

|  
  
`Project Data Access Admin` or higher role

|

To create and manage Atlas Search analyzers and indexes, and assign the role
to your API Key.

|

✓

|

✓

|

✓

|

✓  
  
`Project Owner` role

|

To create and assign project access to API Keys.

|

|

|

✓

|

✓  
  
`Organization Owner` role

|

To create access list entries for your API Key and send the request from a
client that appears in the access list for your API Key.

|

|

|

✓

|

✓  
  
`Project Search Index Editor`

|

To create, view, edit, and delete Atlas Search indexes using the Atlas UI or
API.

|

✓

|

✓

|

✓

|  
  
## Note

You cannot create more than:

  * 3 indexes on `M0` clusters.

  * 5 indexes on `M2` clusters.

  * 10 indexes on `M5` clusters.

There are no limits to the number of indexes you can create on `M10+`
clusters.

## Create an Atlas Search Index Using the Atlas UI

When you create a new Atlas Search index, choose a configuration method.

click to enlarge

You can use either the default index definition or specify a custom definition
for the index. The default index definition is dynamic mapping of fields in
the documents and will work with any collection. If you wish to create a
custom index definition for static mapping, you can specify which fields to
index with which analyzer and as which data type.

The index name defaults to default. You can leave the default name in place or
choose one of your own.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

Index names must be unique within their namespace.

### Prefer to Learn by Watching?

Follow along with this video tutorial walk-through that demonstrates how to
create Atlas Search indexes of various complexity.

 _Duration: 15 Minutes_

### Procedure

To create an Atlas Search index from the Atlas UI:

1

#### Navigate to the Atlas Cluster Overview page.

Click Database in the top-left corner of Atlas to navigate to the Database
Deployments page for your project.

2

#### Click the cluster name to view cluster details.

3

#### Click the Search tab.

4

#### Create an index.

  * For your first index, click Create Search Index.

  * For subsequent indexes, click Create Index.

5

#### Select a Configuration Method and click Next.

  * For a guided experience, select Visual Editor.

## Note

The Visual Editor doesn't support custom analyzers.

  * To edit the raw index definition, select JSON Editor.

6

#### Enter the Index Name, and set the Database and Collection.

  1. In the Index Name field, enter a name for the index.

## Note

If you name your index `default`, you don't need to specify an `index`
parameter when using the $search pipeline stage. Otherwise, you must specify
the index name using the `index` parameter.

  2. In the Database and Collection section, find the database or collection, and select the collection name.

  3. If you use the Visual Editor, click Next.

7

#### Review the default Atlas Search index configuration settings in the Index
Configurations section.

Visual Editor

JSON Editor

Field Name

|

Description

|

Necessity  
  
||  
  
Index Analyzer

|

Specify the analyzer to use for indexing the collection data. By default,
Atlas Search uses the standard analyzer (`"lucene.standard"`).

Corresponds to the `analyzer` JSON setting.

|

Optional  
  
Query Analyzer

|

Specify the analyzer to use when parsing data for the Atlas Search queries. By
default, Atlas Search uses the standard analyzer (`"lucene.standard"`).

Corresponds to the `searchAnalyzer` JSON setting.

|

Optional  
  
Dynamic Mapping

|

Specify dynamic or static mapping of fields. To disable dynamic mapping, set
`"dynamic":` to `Off`. By default, dynamic mapping is enabled. If you disable
dynamic mapping, you must specify the fields to index. To learn more about
dynamic and static mappings, see Review Atlas Search Index Syntax.

Corresponds to the `mappings.dynamic` JSON setting.

|

Required  
  
If you are satisfied with the default configuration, skip to step 10. If you
wish to refine your Atlas Search index, proceed to the next step.

8

#### Refine your Atlas Search index to configure additional settings.

Visual Editor

JSON Editor

## Note

The Visual Index Builder doesn't support Custom Analyzers.

If you are using the Visual Editor:

  1. Click Refine Your Index to make changes to any of the following settings.

Field Name

|

Description

|

Necessity  
  
||  
  
Field Mappings

|

Required if Dynamic Mapping in the Index Configurations section is disabled.

## Note

Defining your own field mappings is recommended for advanced users only.

Specify the fields to index. To add the fields, you must do the following:

    1. Click Add Field to open the Add Field Mapping window.

    2. Specify the following information about the field:

      * Field name \- Name of the field to index.

      * Data Type Configuration \- Field data type. To learn more about the supported data types and their options, see Data Types and Data Types.

      * Enable Dynamic Mapping \- Static or dynamic mapping to use for fields of types How to Index Fields in Objects and Documents and How to Index Fields in Arrays of Objects and Documents. If you disable dynamic mapping, the data in the field isn't automatically indexed.

    3. Click Add to add the field.

You can, optionally, click the ellipses (...) icon for the field in the
Actions column to do the following:

      * Modify the settings for the field by clicking Edit.

      * Configure additional data types for the field by clicking Add Data Type.

      * Remove the field from the index by clicking Delete.

## Note

Unlike compound indexes, the order of fields in the Atlas Search index
definition is not important. Fields can be defined in any order.

Corresponds to the `mappings.fields` JSON setting.

|

Conditional  
  
Stored Source Fields

|

Specify the fields to store on Atlas Search. You can choose one of the
following:

    * None \- (Default) If selected, Atlas Search doesn't store any field.

    * All \- If selected, Atlas Search stores all the fields in the documents.

    * Specified \- If selected, Atlas Search stores `_id` and the fields you specify. You can specify the fields by doing the following:

      1. Select the field to store on Atlas Search from the dropdown in the Field Name column.

      2. Click Add to add the field to the list of fields to store.

      3. Click Add Field and repeat steps **a** and **b** for each field to add to the list.

      4. (Optional) Click one of the following:

        *  __ Edit to select a different field.

        *  __ Delete to remove the field from the list of fields to store.

    * All Except Specified \- If selected, Atlas Search excludes specific fields from storage on Atlas Search.

      1. Select the field to exclude from the dropdown in the Field Name column.

      2. Click Add to add the field to the list of fields to exclude.

      3. Click Add Field, and repeat steps **a** and **b** for each field to exclude from the list.

      4. (Optional) Click one of the following:

        *  __ Edit to select a different field.

        *  __ Delete to remove the field from the list of fields to exclude.

To learn more about storing fields, see Define Stored Source Fields in Your
Atlas Search Index.

Corresponds to the `storedSource` JSON setting.

|

Optional  
  
Synonyms Mappings

|

Specify synonym mappings to use in your index. To learn more, see Define
Synonym Mappings in Your Atlas Search Index.

To add synonym mappings, you must specify the following settings for each
synonym:

    * Synonym mapping name \- Label that identifies the synonym mapping to refer to at query time. You must specify a unique value. You can't specify an empty string value.

    * Synonym source collection \- Label that identifies the MongoDB collection in the same database as the Atlas Search index. Documents in this collection use the format described in the Synonyms Source Collection Documents. You can also add an empty collection or load a sample collection.

    * Analyzer \- Label that identifies the analyzer to use with this synonym mapping.

## Note

You can use a synonym mapping to query only fields analyzed with the same
analyzer. By default, Atlas Search uses the standard analyzer
(`"lucene.standard"`).

You can specify any Atlas Search analyzer except the following:

      * Language analyzers:

        * `lucene.kuromoji`

        * `lucene.cjk`

      * Custom analyzer tokenizers:

        * nGram Tokenizer

        * edgeGram Tokenizer

      * Custom analyzer token filters:

        * daitchMokotoffSoundex Token Filter

        * nGram Token Filter

        * edgeGram Token Filter

        * shingle Token Filter

Corresponds to the `synonyms` JSON setting.

|

Optional.  
  
  2. Click Save Changes.

9

#### Optional: If you use the Visual Editor, you can save or delete your index
definition draft.

## Note

If you use the Visual Editor and your index definition contains static
mappings, you can save an index definition as a draft. You can't save the
default index definition as a draft. You can save only a custom index
definition as a draft.

  1. Click Cancel.

  2. Click Save Draft or Delete Draft.

## Important

You can't create a new index when you have a pending index draft.

To learn more about creating an index using an index draft, see Resume or
Delete an Atlas Search Index Draft.

10

#### Click Create Search Index.

11

#### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

12

#### Check the status.

The newly created index appears on the Search tab. While the index is
building, the Status field reads Build in Progress. When the index is finished
building, the Status field reads Active.

## Note

Larger collections take longer to index. You will receive an email
notification when your index is finished building.

## Create an Atlas Search Index Using the Atlas Search API

To create an Atlas Search index, send a `POST` request to the `fts/indexes`
endpoint. To learn more about the syntax and parameters for this endpoint, see
Create One.

## Note

Atlas doesn't create the index if the collection doesn't exist, but it still
returns a `200` status.

## Create an Atlas Search Index Using the Atlas CLI

To create a search index for a cluster using the Atlas CLI, run the following
command:

    
    
    atlas clusters search indexes create [indexName] [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters search indexes create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Node Status

When you create the Atlas Search index, the Atlas Search Indexes tab in the
right-side panel of the Atlas UI displays information about Atlas Search
indexes for the selected namespace. The Status column shows the current state
of the index on the primary node of the cluster. Click the View status details
link below the status to view the state of the index on all the nodes of the
cluster.

click to enlarge

When the Status column reads Active, the index is ready to use. In other
states, queries against the index may return incomplete results.

Status

|

Description  
  
|  
  
Not Started

|

Atlas has not yet started building the index.  
  
Initial Sync

|

Atlas is building the index or re-building the index after an edit. When the
index is in this state:

  * For a new index, Atlas Search doesn't serve queries until the index build is complete.

  * For an existing index, you can continue to use the old index for existing and new queries until the index rebuild is complete.

  
  
Active

|

Index is ready to use.  
  
Recovering

|

Replication encountered an error. This state commonly occurs when the current
replication point is no longer available on the `mongod` oplog. You can still
query the existing index until it updates and its status changes to Active.
Use the error in the View status details modal window to troubleshoot the
issue. To learn more, see Fix Atlas Search Issues.  
  
Failed

|

Atlas could not build the index. Use the error in the View status details
modal window to troubleshoot the issue. To learn more, see Fix Atlas Search
Issues.  
  
Delete in Progress

|

Atlas is deleting the index from the cluster nodes.  
  
While Atlas builds the index and after the build completes, the Documents
column shows the percentage and number of documents indexed. The column also
shows the total number of documents in the collection.

## Note

If you run `sh.shardCollection()` on an unsharded collection with Atlas Search
indexes, the Atlas Search indexes might enter an invalid state after sharding.
To mitigate this issue, you can create a new index on the collection after
sharding, or contact support to restart the `mongot` processes on the nodes.

← Create and Manage Atlas Search IndexesProcess Data with Analyzers →

