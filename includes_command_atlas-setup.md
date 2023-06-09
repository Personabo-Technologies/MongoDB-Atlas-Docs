Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas setup

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Examples

Register, authenticate, create, and access an Atlas cluster.

This command takes you through registration, login, default profile creation,
creating your first free tier cluster and connecting to it using MongoDB
Shell.

## Syntax

    
    
    atlas setup [options]  
      
  
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

Flag that indicates whether to skip the confirmation prompt before proceeding
with the requested action.  
  
\--gov

|

|

false

|

Register with Atlas for Government.  
  
-h, --help

|

|

false

|

help for setup  
  
\--noBrowser

|

|

false

|

Don't try to open a browser session.  
  
\--password

|

string

|

false

|

Password for the user.  
  
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

    
    
    # Override default cluster settings like name, provider, or database username by using the command options  
      
    atlas setup --clusterName Test --provider GCP --username dbuserTest  
  
What is MongoDB Atlas? →

