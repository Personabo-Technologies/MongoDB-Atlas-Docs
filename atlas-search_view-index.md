Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# View an Atlas Search Index

Share Feedback

On this page

  * Prerequisites
  * View an Atlas Search Index in the Atlas UI
  * Retrieve Atlas Search Indexes Using the Atlas Search API
  * Retrieve Atlas Search Indexes Using the Atlas CLI

## Important

If you use the $out aggregation stage to modify a collection with an Atlas
Search index, you must delete and re-create the search index. If possible,
consider using $merge instead of `$out`.

You can view an Atlas Search index definition in the Index Overview page. For
each index, the Index Overview page shows the following:

  * Namespace for the index.

  * Index and search analyzers specified in the index definition.

  * Dynamic or static mapping.

  * Field mappings in the index definition, if any, including field name, data type, and whether dynamic mapping is enabled for the individual field.

This page describes how to view your index definition in the Index Overview
page. You can also Edit an Atlas Search Index with the visual or JSON editor
in the Index Overview page.

## Prerequisites

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
  
## View an Atlas Search Index in the Atlas UI

1

### Navigate to the Atlas Cluster Overview page.

2

### Click the cluster name to view cluster details.

3

### Click the Search tab.

4

### Click the name of the index that you wish to view.

## Retrieve Atlas Search Indexes Using the Atlas Search API

To retrieve an Atlas Search index through the API, send a `GET` request with
the `ID` of the Atlas Search index that you wish to retrieve to the
`fts/indexes/` endpoint. To learn more about the syntax and parameters for
this endpoint, see Get All. To retrieve all Atlas Search indexes for a
collection, send a `GET` request to the `fts/indexes/` endpoint with the
namespace of the collection whose indexes you want to retrieve.

## Retrieve Atlas Search Indexes Using the Atlas CLI

To list all search indexes for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters search indexes list [options]  
      
  
To return the details for the search index you specify using the Atlas CLI,
run the following command:

    
    
    atlas clusters search indexes describe <indexId> [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas clusters search indexes list and atlas
clusters search indexes describe.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Resume or Delete an Atlas Search Index DraftEdit an Atlas Search Index →

