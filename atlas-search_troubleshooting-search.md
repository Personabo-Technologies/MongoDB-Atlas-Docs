Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Troubleshoot Atlas Search Errors

Share Feedback

On this page

  * Initial Sync in Progress
  * `mongot` Process Not Installed or Running
  * Empty Result Set

## Initial Sync in Progress

Atlas Search can't perform `$search` queries against an Atlas cluster during
an initial sync process. An initial sync process occurs when you create a new
cluster or perform certain upgrades on a cluster. The process includes the
following steps:

  1. The `mongod` performs an initial sync.

  2. The `mongot` performs an initial sync, which rebuilds the search indexes.

As a result, you may receive an error when running a `$search` query against a
node that you recently created or upgraded. Try your query again after the
initial syncs complete and `mongot` rebuilds the indexes. You can check the
status of the `mongot` initial sync using the following steps:

  1. Click the Search tab for your database deployment.

  2. In the index's `Status` column, click View Status Details.

  3. Check the state of the index for the node. During `mongot` initial sync, the status is `INITIAL SYNC`. When `mongot` finishes rebuilding the index, the status is `ACTIVE`.

## `mongot` Process Not Installed or Running

The following error is returned if you run `$search` queries when the Atlas
Search `mongot` process isn't installed or running:

    
    
    MongoError: Remote error from mongot :: caused by :: Error connecting to localhost:28000.  
      
  
The `mongot` process is installed only when the first Atlas Search index is
defined. If you don't have any Atlas Search index in your Atlas cluster,
create at least one Atlas Search index to resolve this error.

## Tip

### See also:

  * Review Atlas Search Index Syntax

  * Create an Atlas Search Index

## Empty Result Set

`mongot` doesn't return any errors, but returns an empty result set if your
`$search` query:

  * References an index that doesn't exist. If you don't specify an index by name in the query, Atlas Search defaults to an index named `default`. If you don't have an index named `default` or if the index that you specified doesn't exist, Atlas Search doesn't return an error and returns an empty result set. You can specify a valid index by its name using the `index` option. To learn more, see Atlas Search aggregation pipeline stage options.

  * Specifies a non-indexed field. If you run a query against a field that isn't indexed, Atlas Search doesn't return an error and returns an empty result set. You must specify only indexed fields as values for the `path` parameter. You can enable dynamic mapping in your index definition for the collection to ensure that all the dynamically indexable fields in the collection are automatically indexed. To learn more, see Static and Dynamic Mappings.

  * Specifies a field that is indexed as an incorrect data type. In this case, if you run a query, Atlas Search doesn't return an error and returns an empty result set. For example, to run facet queries against `string`, `number`, or `date` fields, create an index for the fields using the corresponding Atlas Search field type such as `stringFacet`, `numberFacet`, and `dateFacet` respectively. To learn more, see Supported and Unsupported Data Types.

← Run Atlas Search QueriesTune Atlas Search Performance →

