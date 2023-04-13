Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Goto

Share Feedback

On this page

  * Use Atlas Goto
  * Atlas Goto Commands
  * Enable Atlas Goto
  * Disable Atlas Goto

Atlas Goto is a native Atlas tool for quick UI navigation. You can use Atlas
Goto shortcut commands to efficiently jump to different locations in the Atlas
UI.

## Note

Atlas Goto is unavailable for Atlas for Government.

## Use Atlas Goto

To use Atlas Goto:

  1. (Optional): If disabled, Enable Atlas Goto. Atlas Goto is enabled by default.

  2. Use the following keyboard shortcuts to open the Atlas Goto modal and issue commands:

Keyboard Shortcut

|

Action  
  
|  
  
Ctrl \+ Space or Cmd \+ /

|

Open the Atlas Goto modal from anywhere in the Atlas UI.  
  
Atlas Goto shortcut command, then Enter

|

Navigate to the specified location.  
  
Atlas Goto shortcut command, then Ctrl \+ Space or Shift \+ Enter

|

Navigate to the specified location in a new tab or window.  
  
Tab key or up/down arrow keys (after opening the Atlas Goto modal)

|

See the available commands and select them from the drop-down menu.  
  
Tab key or up/down arrow keys (after displaying the commands)

|

Cycle through the available commands or autocomplete a partially-specified
command.  
  
Tab \+ Enter (after displaying the commands)

|

Cycle backards through the available commands.  
  
## Atlas Goto Commands

With Atlas Goto enabled, you can use the following shortcut commands within
the Atlas UI. Replace any placeholder values shown in curly brackets with your
values. You can use the Tab key to autocomplete cluster names, organization
names, and project names.

## Note

If the cluster name, organization name, or project name contain spaces, you
must enclose the name in quotation marks.

Command

|

Action  
  
|  
  
`access`

|

Go to the access manager for the current project or the access manager for the
current organization depending on your location.  
  
`activity`

|

Go to the activity feed for the current project or organization depending on
your location.  
  
`advisor`

|

Go to the Performance Advisor tab for the current cluster.

The `advisor` command is unavailable for sharded clusters.  
  
`alerts`

|

Go to the alerts for the current project or organization depending on your
location.  
  
`apps`

|

Go to the top-level Atlas App Services page for the current project.  
  
`apps {projectName}`

|

Go to the top-level Atlas App Services page for the specified project.  
  
`backup`

|

Go to the Backup tab for the current cluster.  
  
`billing`

|

Go to the Billing page for the current organization.  
  
`charts`

|

Go to the top-level Charts page for the current project.  
  
`charts {projectName}`

|

Go to the top-level Charts page for the specified project.  
  
`{clusterName}`

|

Go to the specified cluster within the current project.  
  
`cluster {clusterName}`

|

Go to the specified cluster within the current project. Using `cluster` before
the `{clusterName}` allows you to autocomplete the cluster name using Tab.  
  
`cluster {clusterName} advisor`

|

Go to the Performance Advisor tab for the specified cluster within the current
project.

You can also use the `advisor` command without specifying a cluster to go to
the Performance Advisor tab for the current cluster.

The `cluster {clusterName} advisor` and `advisor` commands are unavailable for
sharded clusters.  
  
`cluster {clusterName} backup`

|

Go to the Backup tab for the specified cluster within the current project.

You can also use the `backup` command without specifying a cluster to go to
the Backup tab for the current cluster.  
  
`cluster {clusterName} collections`

|

Go to the Collections tab for the specified cluster within the current
project.

You can also use the `collections`` command without specifying a cluster to go
to the Collections tab for the current cluster.  
  
`cluster {clusterName} connect`

|

Go to the connection modal for the specified cluster.  
  
`cluster {clusterName} metrics`

|

Go to the Metrics tab for the specified cluster within the current project.

You can also use the `metrics` command without specifying a cluster to go to
the Metrics tab for the current cluster.  
  
`cluster {clusterName} profiler`

|

Go to the Profiler tab for the specified cluster within the current project.

You can also use the `profiler` command without specifying a cluster to go to
the Profiler tab for the current cluster.

The `cluster {clusterName} profiler` and `profiler` commands are unavailable
for sharded clusters.  
  
`cluster {clusterName} rtp`

|

Go to the Real Time tab for the specified cluster within the current project.

You can also use the `rtp` command without specifying a cluster to go to the
Real Time tab for the current cluster.

The `cluster {clusterName} rtp` and `rtp` commands are unavailable for sharded
clusters and serverless instances.  
  
`cluster {clusterName} search`

|

Go to the Atlas Search page for the specified cluster.

You can also use the `search` command without specifying a cluster to go to
the Atlas Search page for the current cluster.

The `cluster {clusterName} search` and `search` commands are unavailable for
serverless instances.  
  
`collections`

|

Go to the Collections tab for the current cluster.  
  
`connect`

|

Go to the connection modal for the current cluster.  
  
`help`

|

Go to this Atlas Goto page in the documentation for help.  
  
`metrics`

|

Go to the Metrics tab for the current cluster.  
  
`org`

|

Go to the projects list for the current organization.  
  
`org settings`

|

Go to the Organization Settings for the current organization.  
  
`org access`

|

Go to the access manager for the current organization.  
  
`org activity`

|

Go to the activity feed for the current organization.  
  
`org alerts`

|

Go to the alerts for the current organization.  
  
`orgs`

|

Go to the list of your organizations.  
  
`orgs {orgName}`

|

Go to the projects list for the specified organization.  
  
`orgs {orgName} access`

|

the access manager for the specified organization.  
  
`orgs {orgName} activity`

|

Go to the activity feed for the specified organization.  
  
`orgs {orgName} alerts`

|

Go to the alerts for the specified organization.  
  
`orgs {orgName} settings`

|

Go to the Organization Settings for the specified organization.  
  
`orgs {orgName} support`

|

Go to the MongoDB Support page for the specified organization.  
  
`{projectName}`

|

Go to the database deployments list for the specified project within the
current organization.  
  
`preferences`

|

Go to the User Preferences page where you can enable or disable Atlas Goto.  
  
`profiler`

|

Go to the Profiler tab for the current cluster.

The `profiler` command is unavailable for sharded clusters.  
  
`project`

|

Go to the database deployments list for the current project.  
  
`project {projectName}`

|

Go to the database deployments list for the specified project within the
current organization. Using `project` before the `{projectName}` allows you to
autocomplete the project name using Tab.  
  
`rtp`

|

Go to the Real Time tab for the current cluster.  
  
`search`

|

Go to the Atlas Search page for the current cluster.

The `search` command is unavailable for serverless instances.  
  
`settings`

|

Go to the Project Settings for the current project or the Organization
Settings for the current organization depending on your location.  
  
`support`

|

Go to the MongoDB Support page for the current project or organization
depending on your location.  
  
## Enable Atlas Goto

Follow these steps to enable Atlas Goto.

1

### Click on your name in the upper right corner of the Atlas UI.

Your account menu displays.

2

### Click User Preferences.

The Personalization page displays.

3

### Toggle Atlas Goto to ON.

## Disable Atlas Goto

Follow these steps to disable Atlas Goto. After you disable Atlas Goto, the
Atlas Goto shortcut commands no longer work.

1

### Click on your name in the upper-right corner of the Atlas UI.

Your account menu displays.

2

### Click User Preferences.

The Personalization page displays.

3

### Toggle Atlas Goto to OFF.

← ReferenceCloud Providers →

