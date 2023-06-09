Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas quickstart

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Create, configure, and connect to an Atlas cluster for your project.

This command creates a new cluster, adds your public IP to the Atlas access
list, creates a database user to access your new MongoDB instance, loads
sample data, and connects to the new cluster using Mongosh.

## Syntax

    
    
    atlas quickstart [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--accessListIp

|

strings

|

false

|

IP address to be allowed to access the deployment.  
  
\--clusterName

|

string

|

false

|

Name of the cluster.  
  
\--currentIp

|

|

false

|

Flag that adds the IP address from the host that is currently executing the
command to the access list.  
  
-Y, --default

|

|

false

|

Flag that runs the Quickstart command with all default and auto-generated
values to deploy and access an Atlas cluster.  
  
\--enableTerminationProtection

|

|

false

|

Enables termination protection for your cluster. You can't delete a cluster
with termination protection enabled.  
  
\--force

|

|

false

|

If specified, skips asking for input and creates a cluster with default
settings for any options you don't specify.  
  
-h, --help

|

|

false

|

help for quickstart  
  
\--password

|

string

|

false

|

Password for the database user.  
  
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
  
-r, --region

|

string

|

false

|

Physical location of your MongoDB cluster. For a complete list of supported
AWS regions, see: https://www.mongodb.com/docs/atlas/reference/amazon-aws/.
For a complete list of supported Azure regions, see:
https://www.mongodb.com/docs/atlas/reference/microsoft-azure/#microsoft-azure.
For a complete list of supported GCP regions, see:
https://www.mongodb.com/docs/atlas/reference/google-gcp/..  
  
\--skipMongosh

|

|

false

|

Indicates whether to skip accessing your deployment with MongoDB Shell.  
  
\--skipSampleData

|

|

false

|

Indicates whether to skip loading sample data into your Atlas cluster.  
  
\--tier

|

string

|

false

|

Tier for each data-bearing server in the cluster. To learn more about cluster
tiers, see https://www.mongodb.com/docs/atlas/manage-clusters/#select-cluster-
tier. This value defaults to "M0".  
  
\--username

|

string

|

false

|

Username for authenticating to MongoDB.  
  
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

    
    
    # Create a Google Cloud cluster named Test with a database user named dbuserTest, add your current IP address to the access list, load sample data, and connect using Mongosh:  
      
    atlas quickstart --clusterName Test --provider GCP --username dbuserTest --currentIp  
      
    
    # Create a cluster with the default provider and settings, randomly generate the cluster name and database username, load sample data, and connect using Mongosh:  
      
    atlas quickstart --force  
  
What is MongoDB Atlas? →

