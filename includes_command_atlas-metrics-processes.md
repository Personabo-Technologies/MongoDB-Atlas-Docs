Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas metrics processes

Share Feedback

On this page

  * Syntax
  * Arguments
  * Options
  * Inherited Options
  * Examples

Return the process measurements for the specified host.

To return the hostname and port needed for this command, run atlas processes
list

To use this command, you must authenticate with a user account or an API key
that has the Project Read Only role.

## Syntax

    
    
    atlas metrics processes <hostname:port> [options]  
      
  
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

help for processes  
  
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
returned. To learn which values the CLI accepts, see the Items Enum for m in
the Atlas API spec: https://www.mongodb.com/docs/atlas/reference/api-
resources-spec/#tag/Monitoring-and-Logs/operation/getHostMeasurements/.  
  
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

    
    
    # Return the JSON-formatted process metrics for the host atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017  
      
    atlas metrics processes atlas-lnmtkm-shard-00-00.ajlj3.mongodb.net:27017 --output json  
  
What is MongoDB Atlas? →

