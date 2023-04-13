Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters indexes create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Create a rolling index for the specified cluster for your project.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Admin role.

## Syntax

    
    
    atlas clusters indexes create [indexName] [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
indexName

|

string

|

false

|

Name of the index.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--clusterName

|

string

|

true

|

Name of the cluster.  
  
\--collection

|

string

|

true

|

Name of the collection.  
  
\--db

|

string

|

true

|

Name of the database.  
  
-h, --help

|

|

false

|

help for create  
  
\--key

|

strings

|

true

|

Field to be indexed and the type of index in the following format: field:type.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--sparse

|

|

false

|

Flag that creates a sparse index. To learn more about sparse indexes, see
https://www.mongodb.com/docs/manual/core/index-sparse/  
  
## Inherited Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
-P, --profile

|

string

|

false

|

Human-readable label that identifies the profile to use from your
configuration file. To learn about profiles for the Atlas CLI, see
https://dochub.mongodb.org/core/atlas-cli-save-connection-settings. To learn
about profiles for MongoCLI, see https://dochub.mongodb.org/core/atlas-cli-
configuration-file.  
  
## Examples

    
    
    # Create an index named bedrooms_1 on the listings collection of the realestate database:  
      
    atlas clusters indexes create bedrooms_1 --clusterName Cluster0 --collection listings --db realestate --key bedrooms:1  
      
    
    # Create a compound index named property_room_bedrooms on the  
      
    listings collection of the realestate database:  
    atlas clusters indexes create property_room_bedrooms --clusterName Cluster0 --collection listings --db realestate --key property_type:1 --key room_type:1 --key bedrooms:1  
  
What is MongoDB Atlas? →

