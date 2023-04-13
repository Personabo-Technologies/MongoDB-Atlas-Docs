Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Global Clusters

Share Feedback

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Global Clusters endpoints provide the ability to add, remove, and retrieve
managed namespaces and custom zone mappings associated with Global Clusters.
Each collection in a Global Cluster is associated with a managed namespace.
For example, the namespace for the `publishers` collection in the `partners`
database is `partners.publishers`.

When you create a managed namespace for a Global Cluster, Atlas creates an
empty collection for that namespace. In addition, Atlas recreates the
collection associated with a managed namespace if you delete the collection
using `mongosh`. However, the recreated collection is empty; Atlas does not
repopulate it with data.

## Note

Creating a managed namespace does not populate a collection with data.
Similarly, deleting a managed namespace does not delete the associated
collection.

Atlas shards the empty collection using the required `location` field and a
custom shard key. For example, if the your custom shard key is `city`, the
compound shard key is `location, city`.

Each Global Cluster is also associated with one or more Global Writes Zones.
When a user creates a Global Cluster, Atlas automatically maps each location
code to the closest geographical zone. Custom zone mappings allow
administrators to override these automatic mappings. For example, a use case
may require mapping a location code to a geographically distant zone.
Administrators can manage custom zone mappings with the APIs below and the
Global Cluster Configuration pane when you create or modify your Global
Cluster.

## Endpoints

Method

|

Endpoint

|

Description  
  
||  
  
`GET`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites

|

Retrieve all managed namespaces and custom zone mappings associated with the
specified Global Cluster.  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/managedNamespaces

|

Adds a managed namespace to the specified Global Cluster.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/managedNamespaces

|

Deletes the specified managed namespace from the specified Global Cluster  
  
`POST`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/customZoneMapping

|

Add an entry to the list of custom zone mappings for the specified Global
Cluster.  
  
`DELETE`

|

/groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/customZoneMapping

|

Remove all custom zone mappings for the specified Global Cluster.  
  
What is MongoDB Atlas? →

