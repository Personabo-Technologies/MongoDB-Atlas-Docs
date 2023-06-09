Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters create

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Create a cluster for your project.

To get started quickly, specify a name for your cluster, a cloud provider, and
a region to deploy a three-member replica set with the latest MongoDB server
version. For full control of your deployment, or to create multi-cloud
clusters, provide a JSON configuration file with the --file flag.

To use this command, you must authenticate with a user account or an API key
that has the Project Owner role.

## Syntax

    
    
    atlas clusters create [name] [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
name

|

string

|

false

|

Name of the cluster. The cluster name cannot be changed after the cluster is
created. Cluster name can contain ASCII letters, numbers, and hyphens.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--backup

|

|

false

|

Flag that enables Continuous Cloud Backup for your deployment. This option is
unavailable for clusters smaller than M10.  
  
\--biConnector

|

|

false

|

Flag that enables BI Connector for Atlas on the deployment.  
  
\--diskSizeGB

|

float

|

false

|

Capacity, in gigabytes, of the host's root volume. This value defaults to 2.  
  
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

help for create  
  
\--mdbVersion

|

string

|

false

|

Major MongoDB version of the cluster.  
  
-m, --members

|

int

|

false

|

Number of members in the replica set. This value defaults to 3.  
  
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
  
-s, --shards

|

int

|

false

|

Number of shards in the cluster. This value defaults to 1.  
  
\--tier

|

string

|

false

|

Tier for each data-bearing server in the cluster. To learn more about cluster
tiers, see https://www.mongodb.com/docs/atlas/manage-clusters/#select-cluster-
tier. This value defaults to "M2".  
  
\--type

|

string

|

false

|

Type of the cluster that you want to create. Valid values are REPLICASET or
SHARDED. This value defaults to "REPLICASET".  
  
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

    
    
    Deploying cluster '<Name>'.  
      
  
## Examples

    
    
    # Deploy a free cluster named myCluster for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster create myCluster --projectId 5e2211c17a3e5a48f5497de3 --provider AWS --region US_EAST_1 --tier M0  
      
    
    # Deploy a three-member replica set named myRS in AWS for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster create myRS --projectId 5e2211c17a3e5a48f5497de3 --provider AWS --region US_EAST_1 --members 3 --tier M10 --mdbVersion 5.0 --diskSizeGB 10  
      
    
    # Deploy a three-member replica set named myRS in AZURE for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster create myRS --projectId 5e2211c17a3e5a48f5497de3 --provider AZURE --region US_EAST_2 --members 3 --tier M10  --mdbVersion 5.0 --diskSizeGB 10  
      
    
    # Deploy a three-member replica set named myRS in GCP for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster create myRS --projectId 5e2211c17a3e5a48f5497de3 --provider GCP --region EASTERN_US --members 3 --tier M10  --mdbVersion 5.0 --diskSizeGB 10  
      
    
    # Deploy a cluster or a multi-cloud cluster from a JSON configuration file named myfile.json for the project with the ID 5e2211c17a3e5a48f5497de3:  
      
    atlas cluster create --projectId <projectId> --file myfile.json  
  
What is MongoDB Atlas? →

