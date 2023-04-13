Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas clusters advancedSettings update

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Output
  * Examples

Update advanced configuration settings for one cluster.

## Syntax

    
    
    atlas clusters advancedSettings update <clusterName> [options]  
      
  
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

true

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
  
\--disableFailIndexKeyTooLong

|

|

false

|

Flag that disables the mongod to writes documents that exceed 1024 bytes but
doesn't index them.  
  
\--disableJavascript

|

|

false

|

Flag that disables the execution of operations that perform server-side
executions of JavaScript.  
  
\--disableTableScan

|

|

false

|

Flag that disables executing any query that requires a collection scan to
return results.  
  
\--enableFailIndexKeyTooLong

|

|

false

|

Flag that enables the mongod to write documents that exceed 1024 bytes limit
but doesn't index them.  
  
\--enableJavascript

|

|

false

|

Flag that enables the execution of operations that perform server-side
executions of JavaScript.  
  
\--enableTableScan

|

|

false

|

Flag that enables executing any query that requires a collection scan to
return results.  
  
-h, --help

|

|

false

|

help for update  
  
\--oplogMinRetentionHours

|

float

|

false

|

Minimum retention window for cluster's oplog expressed in hours.  
  
\--oplogSizeMB

|

int

|

false

|

Storage limit of cluster's oplog expressed in megabytes.  
  
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
  
\--readConcern

|

string

|

false

|

Default level of acknowledgment requested from MongoDB for read operations set
for this cluster.  
  
\--sampleRefreshIntervalBIConnector

|

int

|

false

|

Interval in seconds at which the mongosqld process re-samples data to create
its relational schema. This value defaults to -1.  
  
\--sampleSizeBIConnector

|

int

|

false

|

Number of documents per database to sample when gathering schema information.
This value defaults to -1.  
  
\--tlsProtocol

|

string

|

false

|

Minimum Transport Layer Security (TLS) version that the cluster accepts for
incoming connections.  
  
\--writeConcern

|

string

|

false

|

Default level of acknowledgment requested from MongoDB for write operations
set for this cluster.  
  
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

    
    
    Updating advanced configuration settings of your cluster'.  
      
  
## Examples

    
    
    # Update the minimum oplog size for a cluster:  
      
    atlas cluster advancedSettings update <clusterName> --projectId <projectId> --oplogSizeMB 1000  
      
    
    # Update the minimum TLS protocol version for a cluster:  
      
    atlas cluster advancedSettings update <clusterName> --projectId <projectId> --minimumEnabledTLSProtocol "TLS1_2"  
  
What is MongoDB Atlas? →

