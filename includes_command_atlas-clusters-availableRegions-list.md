Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters availableRegions list

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

List available regions that Atlas supports for new deployments.

## Syntax

    
    
    atlas clusters availableRegions list [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
-h, --help

|

|

false

|

help for list  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--provider

|

string

|

false

|

Name of your cloud service provider. Valid values are AWS, AZURE, or GCP.  
  
\--tier

|

string

|

false

|

Tier for each data-bearing server in the cluster. To learn more about cluster
tiers, see https://www.mongodb.com/docs/atlas/manage-clusters/#select-cluster-
tier.  
  
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

    
    
    # List available regions for a given cloud provider and tier:  
      
    atlas cluster availableRegions --provider AWS --tier M50  
      
    
    # List available regions by tier for a given provider:  
      
    atlas cluster availableRegions --provider GCP  
  
What is MongoDB Atlas? →

