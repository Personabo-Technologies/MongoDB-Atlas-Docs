Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Edit an Atlas Search Index

Share Feedback

On this page

  * Permissions required
  * Edit an Atlas Search Index Using the Atlas UI
  * Edit an Atlas Search Index Using the Atlas Search API
  * Edit an Atlas Search Index Using the Atlas CLI

You can change the index definition of an existing Atlas Search index. You
cannot rename an index; if you need to change an index's name, you must create
a new index and delete the old one.

## Permissions required

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
  
## Edit an Atlas Search Index Using the Atlas UI

1

### Navigate to the Atlas Cluster Overview page.

Click Database in the top-left corner of Atlas to navigate to the Database
Deployments page for your project.

2

### Click the cluster name to view cluster details.

3

### Click the Search tab.

4

### Click __and choose one of the following from the dropdown.

  * Edit with Visual Editor for a guided experience.

## Note

The Visual Editor doesn't support custom analyzers or synonym mapping
definitions.

  * Edit with JSON Editor to edit the raw index definition.

5

### Review current configuration settings and edit them as needed.

  * If you are using the Visual Editor, configure the following settings:

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
  
  * If you are using the JSON Editor, configure the following settings:

Field Name

|

Description

|

Necessity  
  
||  
  
`analyzer`

|

Specify the analyzer to use for indexing the collection data. By default,
Atlas Search uses the standard analyzer (`"lucene.standard"`).

|

Optional  
  
`searchAnalyzer`

|

Specify the analyzer to use when parsing data for the Atlas Search queries. By
default, Atlas Search uses the standard analyzer (`"lucene.standard"`).

|

Optional  
  
`mappings.dynamic`

|

Specify dynamic or static mapping of fields. To disable dynamic mapping, set
`"dynamic":` to `false`. By default, dynamic mapping is enabled. If you
disable dynamic mapping, you must specify the fields to index. To learn more
about dynamic and static mappings, see Review Atlas Search Index Syntax.

|

Required  
  

6

### Click Save to apply the changes.

The index's status changes from Active to Building. In this state, you can
continue to use the old index because Atlas Search does not delete the old
index until the updated index is ready for use. Once the status returns to
Active, the modified index is ready to use.

## Edit an Atlas Search Index Using the Atlas Search API

To edit an Atlas Search index through the API, send a `PATCH` request with the
`ID` of the Atlas Search index that you wish to modity to the `fts/indexes/`
endpoint. To learn more about the syntax and parameters for this endpoint, see
Update One.

## Edit an Atlas Search Index Using the Atlas CLI

To update a search index for a cluster using the Atlas CLI, run the following
command:

    
    
    atlas clusters search indexes update <indexId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters search indexes update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← View an Atlas Search IndexDelete an Atlas Search Index →

