Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Pause and Resume Archiving

Share Feedback

On this page

  * Pause Archiving Through the Atlas CLI
  * Pausing and Resuming Through the API
  * Pause Archiving Through the UI
  * Resume Archiving Through the Atlas CLI
  * Resume Archiving Through the UI

## Important

### Feature unavailable in Serverless Instances

Serverless instances don't support this feature at this time. To learn more,
see Serverless Instance Limitations.

You can pause and resume archiving from the Atlas CLI, Atlas UI,and API. When
you pause, previously archived documents continue to be available on the cloud
object storage for querying, but archiving activity for the collection on your
Atlas cluster is stopped until you resume archiving. Also, Atlas pauses data
expiration until you resume. You will continue to incur costs for storage on
the cloud object storage and for reading data. When you resume archiving, data
that meets the criteria for archiving is archived and archived data that meets
the deletion age limit is deleted.

You can pause an online archive and create another online archive for the same
namespace and partition fields as the paused online archive, but only one
online archive can be `Active`. If you try to resume a paused online archive
when another online archive for the same namespace is `Active`, the resume
operation will fail. You must either delete or pause the `Active` online
archive to resume archiving for the paused online archive.

## Pause Archiving Through the Atlas CLI

To pause an online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives pause <archiveId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters onlineArchives pause.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Pausing and Resuming Through the API

To pause an active online archive or resume a paused online archive through
the API, send a `PATCH` request to the onlineArchives endpoint with the unique
ID of the online archive to pause or resume. To learn more about the syntax
and options, see API.

## Pause Archiving Through the UI

To pause archiving, in your Atlas UI:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Navigate to the Online Archive tab for your cluster.

  1. Click the name of the cluster.

  2. Click the Online Archive tab to view the list of online archives, if any, for the cluster.

3

### Click the ellipsis (`...`) in the Actions column for the online archive to
display the list of allowed actions.

You can:

  * Pause Archiving (only if state is Active)

  * Edit Archive

  * Delete Archive

  * Resume Archiving (only if state is Paused)

4

### Select Pause Archiving from the ellipsis menu to temporarily stop
archiving data in the collection.

## Resume Archiving Through the Atlas CLI

To start a paused online archive for a cluster using the Atlas CLI, run the
following command:

    
    
    atlas clusters onlineArchives start <archiveId> [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas clusters onlineArchives start.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Resume Archiving Through the UI

To resume archiving, in your Atlas UI:

1

### Navigate to the Database Deployments page for your project.

  1. If it is not already displayed, select the organization that contains your desired project from the __ Organizations menu in the navigation bar.

  2. If it is not already displayed, select your desired project from the Projects menu in the navigation bar.

  3. If the Database Deployments page is not already displayed, click Database in the sidebar.

2

### Navigate to the Online Archive tab for your cluster.

The list of Online Archives displays.

3

### Click the ellipsis (`...`) in the Actions column for the online archive to
display the list of allowed actions.

You can:

  * Pause Archiving (only if state is Active)

  * Edit Archive

  * Delete Archive

  * Resume Archiving (only if state is Paused)

4

### Select Resume Archiving from the ellipsis menu to start archiving.

## Note

The Resume Archive option is only visible for online archives in Paused state.

← Manage Private Endpoints for Online ArchivesBack Up Online Archive Data →

