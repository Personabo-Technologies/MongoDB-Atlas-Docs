Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Resume or Delete an Atlas Search Index Draft

Share Feedback

On this page

  * Procedure

If you saved your Atlas Search index definition as a draft, you can resume
editing your index definition.

## Important

You can't create a new index when you have a pending index draft.

## Procedure

1

### Navigate to the Atlas Cluster Overview page.

Click Database in the top-left corner of Atlas to navigate to the Database
Deployments page for your project.

2

### Click the cluster name to view cluster details.

3

### Click the Search tab.

4

### Click Resume Index Creation.

5

### Optional: Save or delete your index definition draft.

  1. Click Cancel.

  2. Click Save Draft or Delete Draft.

6

### Customize your Atlas Search index configuration settings.

Click Refine Your Index to make changes to any of the following settings and
click Save Changes.

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
  
7

### Click Create Search Index.

8

### Close the You're All Set! Modal Window.

A modal window appears to let you know your index is building. Click the Close
button.

9

### Check the status.

The newly created index appears on the Search tab. While the index is
building, the Status field reads Build in Progress. When the index is finished
building, the Status field reads Active.

## Note

Larger collections take longer to index. You will receive an email
notification when your index is finished building.

← Review Atlas Search Index SyntaxView an Atlas Search Index →

