Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Organizations

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

The `orgs` resource provides access to manage Atlas organizations.

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

/orgs

|

Get all Atlas organizations the authenticated user has access to.  
  
`GET`

|

/orgs/{ORG-ID}

|

Get information about the Atlas organization identified by `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/users

|

Get information about the Atlas users associated with `{ORG-ID}`.  
  
`PATCH`

|

/orgs/{ORG-ID}

|

Rename an Atlas organization.  
  
`DELETE`

|

/orgs/{ORG-ID}

|

Delete the Atlas organization identified by `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/groups

|

Get all projects in the organization identified by `{ORG-ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/invites

|

Retrieves all pending invitations to the organization identified by `{ORG-
ID}`.  
  
`GET`

|

/orgs/{ORG-ID}/invites/{INVITATION-ID}

|

Retrieves one pending invitation to the organization identified by
`{INVITATION-ID}`.  
  
`POST`

|

/orgs/{ORG-ID}/invites

|

Invites one user to the organization identified by `{ORG-ID}`.  
  
`PATCH`

|

/orgs/{ORG-ID}/invites

|

Update one pending invitation to the organization associated with `{ORG-ID}`.  
  
`PATCH`

|

/orgs/{ORG-ID}/invites/{INVITATION-ID}

|

Update one pending invitation by `{INVITATION-ID}` to the organization
associated with `{ORG-ID}`.  
  
`DELETE`

|

/orgs/{ORG-ID}/invites/{INVITATION-ID}

|

Deletes one pending invitation to an organization identified by `{INVITATION-
ID}`.  
  
## Tip

### See also:

Invoices for endpoints that permit you to retrieve an organization's invoices.

Programmatic API Keys for endpoints that permit you to configure API Keys for
an organization.

What is MongoDB Atlas? →

