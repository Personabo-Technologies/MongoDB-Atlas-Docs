Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# atlas organizations apiKeys accessLists create

Share Feedback

On this page

  * Syntax
  * Options
  * Inherited Options
  * Output
  * Examples

Create an IP access list entry for your API Key.

To view possible values for the apiKey option, run atlas organizations apiKeys
list.

To use this command, you must authenticate with a user account or an API key
that has the Read Write role.

## Syntax

    
    
    atlas organizations apiKeys accessLists create [options]  
      
  
## Options

Name

|

Type

|

Required

|

Description  
  
|||  
  
\--apiKey

|

string

|

true

|

Unique 24-digit string that identifies your API key.  
  
\--cidr

|

strings

|

false

|

Access list entry in CIDR notation to be added for your API key. To add more
than one entry, you can specify each entry with a separate cidr flag or
specify all the entries as a comma-separated list using one cidr flag. You
can't set both cidr and ip in the same command.  
  
\--currentIp

|

|

false

|

Flag that adds the IP address from the host that is currently executing the
command to the access list. Only applicable for type ipAddress entries. You
don't need the entry argument when you use the currentIp option.  
  
-h, --help

|

|

false

|

help for create  
  
\--ip

|

strings

|

false

|

IP address that you want to add to the access list for your API key. To add
more than one IP address, you can specify each address with a separate ip flag
or specify the all addresses as a comma-separated list using one ip flag. You
can't set both ip and cidr in the same command.  
  
\--orgId

|

string

|

false

|

Organization ID to use. Overrides the settings in the configuration file or
environment variable.  
  
-o, --output

|

string

|

false

|

Output format. Valid values are json, json-path, go-template, or go-template-
file.  
  
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

    
    
    Created new access list entry(s).  
      
  
## Examples

    
    
    # Create access list entries for two IP addresses for the API key with the ID 5f24084d8dbffa3ad3f21234 in the organization with the ID 5a1b39eec902201990f12345:  
      
    atlas organizations apiKeys accessLists create --apiKey 5f24084d8dbffa3ad3f21234 --cidr 192.0.2.0/24,198.51.100.0/24 --orgId 5a1b39eec902201990f12345 --output json  
  
What is MongoDB Atlas? →

