Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Delete a Managed Namespace

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * HTTP Response Elements
  * Example
  * Request
  * Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

`https://cloud.mongodb.com/api/atlas/v1.0`

Delete a managed namespace for a Global Cluster. Deleting a managed namespace
does not delete the collection associated with the namespace. Use the Data
Explorer to delete both the collection and the managed namespace.
Alternatively, use this endpoint to delete the managed namespace and `mongosh`
to delete the collection.

## Note

Deleting a managed namespace does not unshard the associated collection.

For more information about managed namespaces, see Global Clusters.

## Syntax

    
    
    DELETE /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/managedNamespaces  
      
  
### Request Path Parameters

Path Element

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required.

|

Unique identifier for the project that contains the Global Cluster.  
  
`CLUSTER-NAME`

|

Required.

|

Name of the Global Cluster.  
  
### Request Query Parameters

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pageNum

|

integer

|

Optional

|

Page number, starting with one, that Atlas returns of the total number of
objects.

|

`1`  
  
itemsPerPage

|

integer

|

Optional

|

Number of items that Atlas returns per page, up to a maximum of 500.

|

`100`  
  
includeCount

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the **totalCount** parameter in the
response body.

|

`true`  
  
pretty

|

boolean

|

Optional

|

Flag that indicates whether Atlas returns the JSON response in the prettyprint
format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag that indicates whether Atlas wraps the response in an envelope.

Some API clients cannot access the HTTP response headers or status code. To
remediate this, set `envelope=true` in the query.

Endpoints that return a list of results use the **results** object as an
envelope. Atlas adds the **status** parameter to the response body.

|

`false`  
  
|

|

|

|  
  
||||  
  
collection

|

string

|

Optional

|

Name of the collection associated with the managed namespace.

|  
  
db

|

string

|

Optional

|

Name of the database containing the collection.

|  
  
### Request Body Parameters

This endpoint does not use HTTP request body parameters.

## HTTP Response Elements

Name

|

Type

|

Description  
  
||  
  
`customZoneMapping`

|

document

|

A comma-separated list of all custom zone mappings defined for the Global
Cluster. Atlas automatically maps each location code to the closest
geographical zone. Custom zone mappings allow administrators to override these
automatic mappings. If your Global Cluster does not have any custom zone
mappings, this document is empty.  
  
`managedNamespaces`

|

array of documents

|

Each document specifies a namespace for a Global Cluster managed by Atlas.  
  
`managedNamespaces[n].collection`

|

string

|

The name of the collection associated with the managed namespace.  
  
`managedNamespaces[n].customShardKey`

|

string

|

The custom shard key for the collection. Global Clusters require a compound
shard key consisting of a `location` field and a user-selected second key, the
custom shard key.  
  
`managedNamespaces[n].db`

|

string

|

The name of the database containing the collection.  
  
`managedNamespaces[n].isCustomShardKeyHashed`

|

boolean

|

Flag that specifies whether the custom shard key for the collection is hashed.
Value can be one of the following:

  * `true` \- if custom shard key is hashed

  * `false` \- if custom shard key is not hashed (default)

Default value is `false`. If `false`, Atlas uses ranged sharding. This is only
available for Atlas clusters with MongoDB v4.4 and later.  
  
`managedNamespaces[n].isShardKeyUnique`

|

boolean

|

Flag that specifies whether the underlying index enforces a unique constraint.
Value can be one of the following:

  * `true` \- if shard key is unique

  * `false` \- if shard key is not unique (default)

  
  
`managedNamespaces[n].numInitialChunks`

|

integer

|

Minimum number of chunks to create initially when sharding an empty collection
with a hashed shard key. To learn more, see Global Cluster Sharding Reference.
This is only available for Atlas clusters with MongoDB v4.4 and later.  
  
`managedNamespaces[n].presplitHashedZones`

|

boolean

|

Flag that specifies whether to perform initial chunk creation and distribution
for an empty or non-existing collection based on the defined zones and zone
ranges for the collection. Value can be one of the following:

  * `true` \- to perform initial chunk creation and distribution

  * `false` \- to not perform initial chunk creation and distribution (default)

Default value is `false`. This is only available for Atlas clusters with
MongoDB v4.4 and later.  
  
## Example

### Request

    
    
    curl -X DELETE -i --digest --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
      "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c391af480eef519ea5deeb1/clusters/Cluster1/globalWrites/managedNamespaces?db=data&collection=distributors&pretty=true"  
  
### Response

    
    
     {  
      
       "customZoneMapping" : {  
         "AF" : "5b48f5a780eef5236f689f94",  
         "AL" : "5b48f5a780eef5236f689f94",  
         "AU" : "5b48f5cddff5220000f7f375",  
         "AU-ACT" : "5b48f5cddff5220000f7f375",  
         "AU-NSW" : "5b48f5cddff5220000f7f375",  
         "AU-NT" : "5b48f5cddff5220000f7f375",  
         "AU-QLD" : "5b48f5cddff5220000f7f375",  
         "AU-SA" : "5b48f5cddff5220000f7f375",  
         "AU-TAS" : "5b48f5cddff5220000f7f375",  
         "AU-VIC" : "5b48f5cddff5220000f7f375",  
         "AU-WA" : "5b48f5cddff5220000f7f375",  
         "DZ" : "5b48f5a780eef5236f689f94"  
    },  
       "managedNamespaces" : [ {  
         "collection" : "zip-codes",  
         "customShardKey" : "city",  
         "db" : "data"  
       }, {  
         "collection" : "retail-stores",  
         "customShardKey" : "store-number",  
         "db" : "mydata"  
       } ]  
     }  
  
What is MongoDB Atlas? →

