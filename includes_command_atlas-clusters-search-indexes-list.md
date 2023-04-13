Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters search indexes list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

List all Atlas Search indexes for a cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Data Access Read/Write role.

## Syntax

    
    
    atlas clusters search indexes list [options]  
      
  
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

help for list  
  
\--limit

|

int

|

false

|

Number of items per results page. This value defaults to 100.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--page

|

int

|

false

|

Page number that specifies a page of results. This value defaults to 1.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
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

    
    
    # Return the JSON-formatted list of Atlas search indexes on the sample_mflix.movies database in the cluster named myCluster:  
      
    atlas clusters search indexes list --clusterName myCluster --db sample_mflix --collection movies --output json  
  
What is MongoDB Atlas? →

