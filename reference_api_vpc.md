Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Network Peering

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Endpoints

The following lists the endpoints available for Network Peering.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/containers/all

|

Get details for all network peering containers in an Atlas project.  
  
`GET`

|

/groups/{GROUP-ID}/containers

|

Get details for all network peering containers in an Atlas project for a
single cloud provider.  
  
`GET`

|

/groups/{GROUP-ID}/containers/{CONTAINER-ID}

|

Get details for one network peering container in an Atlas project.  
  
`POST`

|

/groups/{GROUP-ID}/containers

|

Create one new network peering container in an Atlas project.  
  
`PATCH`

|

/groups/{GROUP-ID}/containers/{CONTAINER-ID}

|

Update details for one network peering container in an Atlas project.  
  
`DELETE`

|

/groups/{GROUP-ID}/containers/{CONTAINER-ID}

|

Remove one network peering container in an Atlas project.  
  
`GET`

|

/groups/{GROUP-ID}/peers

|

Get details for all network peering connections in an Atlas project.  
  
`GET`

|

/groups/{GROUP-ID}/peers/{PEER-ID}

|

Get details for one network peering connection in an Atlas project.  
  
`POST`

|

/groups/{GROUP-ID}/peers

|

Create a new network peering connection in an Atlas project.  
  
`PATCH`

|

/groups/{GROUP-ID}/peers/{PEER-ID}

|

Update a new network peering connection in an Atlas project.  
  
`DELETE`

|

/groups/{GROUP-ID}/peers/{PEER-ID}

|

Delete one network peering connection in an Atlas project.  
  
`GET`

|

/groups/{GROUP-ID}/privateIpMode

|

Verify if an Atlas project is in Connect via Peering Only mode.

## Note

Atlas has deprecated Connect via Peering Only. You should use split horizon
connection strings.  
  
`PATCH`

|

/groups/{GROUP-ID}/privateIpMode

|

Disable Connect via Peering Only mode for one Atlas project.

## Note

Atlas has deprecated Connect via Peering Only. You should use split horizon
connection strings.  
  
What is MongoDB Atlas? →

