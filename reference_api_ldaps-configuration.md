Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# LDAP Configuration

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

Use the following endpoints to verify and save an LDAP configuration for an
Atlas project. An LDAP configuration defines settings for Atlas to connect to
your LDAP server over TLS for user authentication and authorization. Your LDAP
server must be visible to the internet or connected to your Atlas cluster with
VPC Peering. In addition, your LDAP server must use TLS.

## Note

You must have the `Atlas admin` user privilege to use these endpoints.

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
  
`POST`

|

/groups/{GROUP-ID}/userSecurity/ldap/verify

|

Request verification of an LDAP configuration. Use this endpoint to test your
LDAP configuration details before saving them.  
  
`GET`

|

/groups/{GROUP-ID}/userSecurity/ldap/verify/{REQUEST-ID}

|

Retrieve the status of a request for verification of an LDAP configuration.  
  
`PATCH`

|

/groups/{GROUP-ID}/userSecurity

|

Save an LDAP configuration for a Atlas project.

If you change your LDAP configuration, Atlas performs a rolling restart of
your cluster. This restart allows Atlas to use the correct settings to
authenticate users.  
  
`GET`

|

/groups/{GROUP-ID}

|

Get the current LDAP configuration for an Atlas project.  
  
`DELETE`

|

/groups/{GROUP-ID}/userSecurity

|

Delete the current `userToDNMapping` from the LDAP configuration for an Atlas
project.

If you change your LDAP configuration, Atlas performs a rolling restart of
your cluster. This restart allows Atlas to use the correct settings to
authenticate users.  
  
What is MongoDB Atlas? →

