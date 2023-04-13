Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Maintenance Windows

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `maintenanceWindow` resource provides access to retrieve or update the
current Atlas project maintenance window. To learn more about Maintenance
Windows, see the Set Preferred Cluster Maintenance Start Time setting on the
View/Modify Project Settings page.

## Note

Atlas performs maintenance the same way as the manual maintenance procedure.
This requires at least one replica set election during the maintenance window
per replica set.

You can defer a scheduled maintenance event for a project up to two times.
Deferred maintenance events occur during your preferred maintenance window
exactly one week after the previously scheduled date and time.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/maintenanceWindow

|

Get the current user-defined maintenance window for the given project.  
  
`PATCH`

|

/groups/{GROUP-ID}/maintenanceWindow

|

Update the current maintenance window for the given project.  
  
`POST`

|

/groups/{GROUP-ID}/maintenanceWindow/defer

|

Defer the next scheduled maintenance for the given project for one week.  
  
`POST`

|

/groups/{GROUP-ID}/maintenanceWindow/autoDefer

|

Defer any scheduled maintenance for the given project for one week.  
  
`DELETE`

|

/groups/{GROUP-ID}/maintenanceWindow

|

Clear the current maintenance window for the given project.  
  
What is MongoDB Atlas? →

