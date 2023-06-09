Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas metrics disks describe

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the measurements of a disk or partition on the specified host.

To return the hostname and port needed for this command, run atlas processes
list

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas metrics disks describe <hostname:port> <diskName> [options]  
      
  
## Arguments

Name

|

Type

|

Required

|

Description  
  
|||  
  
hostname:port

|

string

|

true

|

Hostname and port number of the instance running the MongoDB process.  
  
diskName

|

string

|

true

|

Label that identifies the disk or partition from which you want to retrieve
metrics.  
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--end

|

string

|

false

|

ISO 8601-formatted date and time that specifies when to stop retrieving
measurements. You can't set this parameter and period in the same request.  
  
\--granularity

|

string

|

true

|

ISO 8601-formatted duration that specifies the interval between measurement
data points. Only the following subset of ISO 8601-formatted time periods are
supported: PT10S, PT1M, PT5M, PT1H, P1D. When you specify granularity, you
must specify either period or start and end.  
  
-h, --help

|

|

false

|

help for describe  
  
\--limit

|

int

|

false

|

Number of items per results page.  
  
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

Page number that specifies a page of results.  
  
\--period

|

string

|

false

|

ISO 8601-formatted time period that specifies the length of time in the past
to query. You can't set this parameter and start/end in the same request  
  
\--projectId

|

string

|

false

|

Hexadecimal string that identifies the project to use. This option overrides
the settings in the configuration file or environment variable.  
  
\--start

|

string

|

false

|

ISO 8601-formatted date and time that specifies when to start retrieving
measurements. You can't set this parameter and period in the same request.  
  
\--type

|

strings

|

false

|

Measurements to return. If this is not specified, all measurements are
returned. Valid values are DATABASE_AVERAGE_OBJECT_SIZE,
DATABASE_COLLECTION_COUNT, DATABASE_DATA_SIZE, DATABASE_STORAGE_SIZE,
DATABASE_INDEX_SIZE, DATABASE_INDEX_COUNT, DATABASE_EXTENT_COUNT,
DATABASE_OBJECT_COUNT, and DATABASE_VIEW_COUNT  
  
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

    
    
    # Return the JSON-formatted disk metrics from the last 36 hours with 5-minute granularity for the database named testDB in the host atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017  
      
    atlas metrics disks describe atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017 testDB --granularity PT1M --period P1DT12H --output json  
  
What is MongoDB Atlas? →

