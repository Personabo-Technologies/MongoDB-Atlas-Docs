Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Configure Maintenance Window

Share Feedback

On this page

  * Maintenance Window Considerations
  * Procedure
  * Respond to Required Maintenance
  * Maintenance Version Upgrades during Maintenance Windows

You can set the hour of the day that Atlas should start weekly maintenance on
your cluster. This setting is optional and is not required for most clusters.
Configure maintenance windows from your project settings.

Typically, you do not need to manually configure a maintenance window. Atlas
performs maintenance automatically in a rolling manner to preserve continuous
availability, with the exception of a momentary replica set election. You can
use the Test Failover capability to ensure that your application is resilient
to replica set elections.

Custom maintenance windows provide greater control over your cluster
performance by allowing maintenance to occur at your preferred time of day.

## Maintenance Window Considerations

### Urgent Maintenance Activities

Atlas performs urgent maintenance activities such as security patches as soon
as they are needed without regard to scheduled maintenance windows.

## Note

Some non-urgent updates that don't require a `mongod` restart, for example
backend services updates, might also occur without regard to scheduled
maintenance windows.

### Ongoing Maintenance Operations

Once you schedule a maintenance window for your cluster, you cannot change it
until any ongoing maintenance operations have completed.

### MongoDB Database Upgrades

If maintenance include the upgrade of the MongoDB versions, Atlas displays the
current and target versions in the console.

### Maintenance Requires Replica Set Elections

Atlas performs maintenance the same way as the maintenance procedure described
in the MongoDB Manual. This procedure requires at least one replica set
election during the maintenance window per replica set.

Use the Test Failover capability to ensure that your application is resilient
to replica set elections.

### Maintenance Starts As Close to the Hour As Possible

Maintenance always begins as close to the scheduled hour as possible, but in-
progress cluster updates or unexpected system issues could delay the start
time.

## Procedure

### Open Your Project Settings

1

#### Navigate to the Settings page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. Next to the Projects menu, expand the Options menu, then click Project Settings.

2

#### View or modify project settings.

### View and Configure Maintenance Window

Atlas CLI

Atlas UI

To return the details for the maintenance window using the Atlas CLI, run the
following command:

    
    
    atlas maintenanceWindows describe [options]  
      
  
To update the maintenance window using the Atlas CLI, run the following
command:

    
    
    atlas maintenanceWindows update [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas maintenanceWindows describe and atlas
maintenanceWindows update.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

### Clear Your Maintenance Window Configuration Settings

If you configured a preferred maintenance window start time, you can clear the
settings using the Atlas CLI or the Atlas UI. Clearing your maintenance window
configuration restores the default maintenance window settings.

Atlas CLI

Atlas UI

To clear the configured maintenance window using the Atlas CLI, run the
following command:

    
    
    atlas maintenanceWindows clear [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas maintenanceWindows clear.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Respond to Required Maintenance

When maintenance is required, Atlas:

  * Displays a banner in your project's cluster list showing the date and time when the maintenance is scheduled.

  * Sends a notification email to users with the `Project Owner` role between 48 and 72 hours before the scheduled maintenance.

## Note

To configure how you receive scheduled maintenance window notifications, see
Configure a Maintenance Window Alert.

Atlas CLI

Atlas UI

To defer the maintenance window using the Atlas CLI, run the following
command:

    
    
    atlas maintenanceWindows defer [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas maintenanceWindows defer.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Maintenance Version Upgrades during Maintenance Windows

If Atlas will upgrade the MongoDB maintenance version on one of your clusters
during the next maintenance window, the cluster's card displays the target
MongoDB maintenance version.

click to enlarge

← Upgrade Major MongoDB Version for a ClusterPause, Resume, or Terminate a
Cluster →

