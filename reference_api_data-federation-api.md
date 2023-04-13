Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Data Federation

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `dataFederation` resource provides access to the project's federated
database instance configuration. The resource lets you view, create, modify,
and delete federated database instances. The resource requires your project.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

## Important

Changes to federated database instance configurations can affect costs. Before
making changes, please see Billing.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation

|

Get all federated database instances for the specified project.  
  
`GET`

|

/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds

|

Get all the private endpoints for the federated database instances in the
specified project.  
  
`GET`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{NAME}

|

Get an federated database instance in the specified project.  
  
`GET`

|

/api/atlas/v1.0/groups/{GROUP-
ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}

|

Get the specified private endpoint in the specified project.  
  
`GET`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{tenantName}/queryLogs.gz

|

Download query log for the specified federated database instance.  
  
`POST`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation

|

Create a federated database instance in the specified project.  
  
`POST`

|

/api/atlas/v1.0/groups/{GROUP-ID}/privateNetworkSettings/endpointIds

|

Add one AWS private endpoint for the federated database instances in the
specified project.  
  
`PATCH`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{NAME}

|

Update an federated database instance in the specified project.  
  
`DELETE`

|

/api/atlas/v1.0/groups/{GROUP-ID}/dataFederation/{NAME}

|

Delete a federated database instance in the specified project.  
  
`DELETE`

|

/api/atlas/v1.0/groups/{GROUP-
ID}/privateNetworkSettings/endpointIds/{ENDPOINT-ID}

|

Delete one AWS private endpoint in the specified project.  
  
What is MongoDB Atlas? →

