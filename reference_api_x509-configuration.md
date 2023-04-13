Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# X.509 Authentication for Database Users

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Use the following endpoints to manage database users who authenticate using
X.509 certificates. You can manage these X.509 certificates or let Atlas do it
for you.

Management

|

Description  
  
|  
  
Atlas

|

Atlas manages your Certificate Authority and can generate certificates for
your database users. No additional X.509 configuration is required.  
  
Customer

|

You must provide a Certificate Authority and generate certificates for your
database users. To learn more about managing X.509, see Self-Managed X.509.  
  
## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Required Roles

You must have the `Atlas admin` role to use these endpoints.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/databaseUsers/{USERNAME}/certs

|

Get a list of all Atlas-managed, unexpired certificates for a user.  
  
`POST`

|

/groups/{GROUP-ID}/databaseUsers/{USERNAME}/certs

|

Generate an Atlas-managed X.509 certificate for a MongoDB user that
authenticates using X.509 certificates. If you are managing your own
Certificate Authority in Self-Managed X.509 mode, you are responsible for
generating and distributing certificates instead.  
  
`GET`

|

/groups/{GROUP-ID}/userSecurity

|

Get the current customer-managed X.509 configuration details for an Atlas
project.  
  
`PATCH`

|

/groups/{GROUP-ID}/userSecurity

|

Save a customer-managed X.509 configuration for an Atlas project.  
  
`DELETE`

|

/groups/{GROUP-ID}/userSecurity/customerX509

|

Clear customer-managed X.509 settings on a project. This disables customer-
managed X.509.  
  
What is MongoDB Atlas? →

