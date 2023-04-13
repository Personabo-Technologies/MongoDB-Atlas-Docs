Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Database Users

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

The `databaseUsers` resource lets you retrieve, create and modify the database
users in your cluster.

Each database user requires the following parameters to authenticate with a
MongoDB database:

  * username

  * password

  * authentication database

Atlas sets `admin` as the authentication database for all users. The
authentication database doesn't set the user's privileges on the project's
databases.

Each database user has a list of roles that authorize certain privileges on a
project's databases.

By default, a database user's roles apply to all the clusters in the project:

## Example

Two clusters have a `products` database. One user, Pat, has a role granting
`read` access on the `products` database. Pat can access `products` on both
clusters.

## Note

If a database user is assigned a custom role, they cannot be assigned any
other roles.

You can limit a database user's access to one or more specific clusters or
data lakes.

The `databaseUsers` resource supports creating temporary database users that
automatically expire within a user-configurable 7-day period.

Atlas audits the creation, deletion, and updates of database users in the
project's Activity Feed. Atlas audits actions pertaining to both temporary and
non-temporary database users. To view the project's Activity Feed, click
Activity Feed in the Project section of the left navigation. For more
information on the project Activity Feed, see View All Activity.

The `databaseUsers` resource requires your Project ID.

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/databaseUsers

|

Get all users in the project.  
  
`GET`

|

/groups/{GROUP-ID}/databaseUsers/admin/{USERNAME}

|

Get a single user in the project.  
  
`POST`

|

/groups/{GROUP-ID}/databaseUsers

|

Create a user for the project.  
  
`PATCH`

|

/groups/{GROUP-ID}/databaseUsers/admin/{USERNAME}

|

Update a user for the project.  
  
`DELETE`

|

/groups/{GROUP-ID}/databaseUsers/admin/{USERNAME}

|

Delete a user for the project.  
  
What is MongoDB Atlas? →

