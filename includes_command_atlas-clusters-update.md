Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Modify the settings of the specified cluster.

You can specify modifications in a JSON configuration file with the --file
flag.

You can't change the name of the cluster or downgrade the MongoDB version of
your cluster.

To use this command, you must authenticate with a user account or an API key
that has the Project Cluster Manager role.

## Syntax

    
    
    atlas clusters update [clusterName] [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
clusterName

|

string

|

false

|

Name of the cluster to update.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--disableTerminationProtection

|

|

false

|

Disables termination protection for your cluster. You can delete a cluster
with termination protection disabled.  
  
\--diskSizeGB

|

float

|

false

|

Capacity, in gigabytes, of the host's root volume.  
  
\--enableTerminationProtection

|

|

false

|

Enables termination protection for your cluster. You can't delete a cluster
with termination protection enabled.  
  
-f, --file

|

string

|

false

|

Path to an optional JSON configuration file that defines cluster settings. To
learn more about configuration files for the Atlas CLI, see
https://www.mongodb.com/docs/atlas/cli/stable/cluster-config-file/. To learn
more about configuration files for MongoCLI, see
https://www.mongodb.com/docs/mongocli/stable/reference/mms-cluster-settings-
file/.  
  
-h, --help

|

|

false

|

help for update  
  
\--mdbVersion

|

string

|

false

|

Major MongoDB version of the cluster.  
  
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
  
## Output

If the command succeeds, the CLI returns output similar to the following
sample. Values in brackets represent your values.

    
    
    Updating cluster '<Name>'.  
      
  
## Examples

    
    
    # Update the tier for a cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster update myCluster --projectId 5e2211c17a3e5a48f5497de3 --tier M50  
      
    
    # Update the disk size for a cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster update myCluster --projectId 5e2211c17a3e5a48f5497de3 --diskSizeGB 20  
      
    
    # Update the MongoDB version for a cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster update myCluster --projectId 5e2211c17a3e5a48f5497de3 --mdbVersion 5.0  
      
    
    # Use a configuration file named cluster-config.json to update a cluster named myCluster for the project with ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster update myCluster --projectId 5e2211c17a3e5a48f5497de3 --file cluster-config.json --output json  
  
What is MongoDB Atlas? →

