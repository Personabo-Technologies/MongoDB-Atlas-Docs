Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete an Atlas Search Index

Share Feedback

On this page

  * Delete an Atlas Search Index Using the Atlas UI
  * Delete an Atlas Search Index Using the Atlas Search API
  * Delete an Atlas Search Index Using the Atlas CLI

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
  
## Delete an Atlas Search Index Using the Atlas UI

1

### Navigate to the Atlas Cluster Overview page.

Click Database in the top-left corner of Atlas to navigate to the Database
Deployments page for your project.

2

### Click the cluster name to view cluster details.

3

### Click the Search tab.

4

### Click the ... button.

The ellipsis button is located on the right side of the panel. Click the
button beside your desired index and select Delete Index.

5

### Click the Delete Index button.

## Delete an Atlas Search Index Using the Atlas Search API

To delete an Atlas Search index through the API, send a `DELETE` request with
the `ID` of the Atlas Search index that you wish to delete to the
`fts/indexes/` endpoint. To learn more about the syntax and parameters for
this endpoint, see Delete One.

## Delete an Atlas Search Index Using the Atlas CLI

To delete a search index from a cluster using the Atlas CLI, run the following
command:

    
    
    atlas clusters search indexes delete <indexId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters search indexes delete.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

← Edit an Atlas Search IndexCreate and Run Atlas Search Queries →

