Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Events

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `events` resource provides access to retrieve events for the specified
organization or project.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/orgs/{ORG-ID}/events

|

Get all events for the organization associated with `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/events/{EVENT-ID}

|

Get the event with ID `{EVENT-ID}` for the organization associated with `{ORG-
ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/events

|

Get all events for the project associated with `{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/events/{EVENT-ID}

|

Get the event with ID `{EVENT-ID}` for the project associated with `{GROUP-
ID}`  
  
What is MongoDB Atlas? →

