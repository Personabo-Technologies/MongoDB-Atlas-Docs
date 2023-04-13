Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Alert Configurations

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

The following lists the endpoints available for alert configuration. An alert
configuration defines the conditions that trigger an alert and the methods of
notification.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/alertConfigs/matchers/fieldNames

|

Get all field names that the `matchers.fieldName` parameter accepts when you
create or update an Alert Configuration.  
  
`GET`

|

/groups/{GROUP-ID}/alertConfigs

|

Get all alert configurations for the project associated to `{GROUP-ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/alertConfigs

|

Create an alert configuration for the project associated to `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}

|

Get the alert configuration specified to `{ALERT-CONFIG-ID}` for the project
associated to `{GROUP-ID}`.  
  
`PUT`

|

/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}

|

Update the alert configuration specified to `{ALERT-CONFIG-ID}` for the
project associated to `{GROUP-ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}

|

Enable/disable the alert configuration specified to `{ALERT-CONFIG-ID}` for
the project associated to `{GROUP-ID}`.  
  
`DELETE`

|

/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}

|

Delete the alert configuration specified to `{ALERT-CONFIG-ID}` for the
project associated to `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/alertConfigs/{ALERT-CONFIG-ID}/alerts

|

Get all open alerts for the alert configuration specified to `{ALERT-CONFIG-
ID}` for the project associated to `{GROUP-ID}`.  
  
What is MongoDB Atlas? →

