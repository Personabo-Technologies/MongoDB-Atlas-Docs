Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Third-Party Integration Settings

Share Feedback

On this page

  * Atlas Endpoints
  * Prometheus Endpoints

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Atlas Endpoints

`https://cloud.mongodb.com/api/atlas/v1.0`

## Important

Each project can only have one configuration per `{INTEGRATION-TYPE}`.

The following lists the endpoints available for managing third-party service
integrations.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/integrations

|

Get all third-party integration configurations for the project associated with
`{GROUP-ID}`.  
  
`GET`

|

/groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}

|

Get a specific third-party integration configuration for `{INTEGRATION-TYPE}`
for the project associated with `{GROUP-ID}`.  
  
`POST`

|

/groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}

|

Add a new third-party integration configuration for `{INTEGRATION-TYPE}` to
the project associated with `{GROUP-ID}`.  
  
`PUT`

|

/groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}

|

Replace the third-party integration configuration for `{INTEGRATION-TYPE}`
with a new configuration, or add a new configuration if there is no
configuration for `{INTEGRATION-TYPE}`, to the project associated with
`{GROUP-ID}`.  
  
`DELETE`

|

/groups/{GROUP-ID}/integrations/{INTEGRATION-TYPE}

|

Remove the third-party integration configuration for `{INTEGRATION-TYPE}` from
the project associated with `{GROUP-ID}`.  
  
## Prometheus Endpoints

`https://cloud.mongodb.com/prometheus/v1.0`

The following lists the endpoints available for managing the Prometheus
integration.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/discovery

|

Returns the latest targets for the project associated with `{GROUP-ID}`.  
  
What is MongoDB Atlas? →

