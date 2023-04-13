Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Programmatic API Keys

Share Feedback

On this page

  * Organization API Key Endpoints
  * Organization API Key Access List Endpoints
  * Organization API Keys on Projects Endpoints

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

## Organization API Key Endpoints

Use the following resources to view, create, or delete programmatic API Keys
within the specified Atlas organization.

Users with the `Organization Owner` role in the organization associated with
the API Key can use the Organization API Key to access these endpoints.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/orgs/{ORG-ID}/apiKeys

|

Get all Organization API Keys associated with `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}

|

Get one Organization API Key.  
  
`PATCH`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}

|

Update an Organization API Key.  
  
`POST`

|

/orgs/{ORG-ID}/apiKeys

|

Create an Organization API Key for the specified organization.  
  
`DELETE`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}

|

Delete the Organization API Key with ID `{API-KEY-ID}`.  
  
## Organization API Key Access List Endpoints

Use the following resources to view, create, and update access lists for
Organization programmatic API Keys.

Users with the `Organization Owner` role in the organization associated with
the API Key can use the Organization API Key to access these endpoints.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accesslist

|

Get all API Key access list entries that belong to `{API-KEY-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accesslist/{IP-ADDRESS}

|

Get the API Key access list entry for `{API-KEY-ID}` specified by `{IP-
ADDRESS}`.  
  
`POST`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accesslist

|

Create one or more API Key access list entries for `{API-KEY-ID}`.  
  
`DELETE`

|

/orgs/{ORG-ID}/apiKeys/{API-KEY-ID}/accesslist/{IP-ADDRESS}

|

Delete the API Key access list entry for `{API-KEY-ID}` specified by `{IP-
ADDRESS}`.  
  
## Organization API Keys on Projects Endpoints

Use the following resources to view, create and assign, or unassign
Organization programmatic API Keys within the specified Atlas project.

Users with the `Project Owner` role in the project associated with the API Key
can use the Organization API Key to access these endpoints.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/apiKeys

|

Get All Organization API Keys Assigned to One Project with ID `{GROUP_ID}`.  
  
`PATCH`

|

/groups/{GROUP-ID}/apiKeys/{API-KEY-ID}

|

Modify Roles of One Organization API Key to One Project.  
  
`POST`

|

/groups/{GROUP-ID}/apiKeys

|

Create and Assign One Organization API Key to One Project.  
  
`PATCH`

|

/groups/{GROUP-ID}/apiKeys/{API-KEY-ID}

|

Assign One Organization API Key to One Project.  
  
`DELETE`

|

/groups/{GROUP-ID}/apiKeys/{API-KEY-ID}

|

Unassign One Organization API Key (`{API-KEY-ID}`) from One Project.  
  
What is MongoDB Atlas? →

