Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add a Managed Namespace

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

Add a managed namespace to a Global Cluster. For more information about
managed namespaces, see Global Clusters.

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/managedNamespaces  
      
  
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

The unique identifier for the project that contains the Global Cluster.  
  
`CLUSTER-NAME`

|

Required.

|

The name of the Global Cluster.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

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
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
### Request Body Parameters

Name

|

Type

|

Description  
  
||  
  
`collection`

|

string

|

The name of the collection associated with the managed namespace.  
  
`customShardKey`

|

string

|

The custom shard key for the collection. Global Clusters require a compound
shard key consisting of a `location` field and a user-selected second key, the
custom shard key.  
  
`db`

|

string

|

The name of the database containing the collection.  
  
`isCustomShardKeyHashed`

|

boolean

|

 _Optional._ Flag that specifies whether the custom shard key for the
collection is hashed. Value can be one of the following:

  * `true` \- if custom shard key is hashed

  * `false` \- if custom shard key is not hashed (default)

If omitted, defaults to `false`. If `false`, Atlas uses ranged sharding. This
is only available for Atlas clusters with MongoDB v4.4 and later.  
  
`isShardKeyUnique`

|

boolean

|

 _Optional._ Flag that specifies whether the underlying index enforces a
unique constraint. Value can be one of the following:

  * `true` \- if shard key is unique

  * `false` \- if shard key is not unique (default)

If omitted, defaults to `false`. You cannot specify `true` when using hashed
shard keys.  
  
`numInitialChunks`

|

integer

|

 _Optional._ Specifies the minimum number of chunks to create initially when
sharding an empty collection with a hashed shard key. Atlas then creates and
balances chunks across the cluster. The `numInitialChunks` must be less than
`8192` per shard. If omitted, defaults to `2`. To learn more, see Global
Cluster Sharding Reference. This is only available for Atlas clusters with
MongoDB v4.4 and later.  
  
`presplitHashedZones`

|

boolean

|

 _Optional._ For hashed sharding only. Flag that specifies whether to perform
initial chunk creation and distribution for an empty or non-existing
collection based on the defined zones and zone ranges for the collection.
Value can be one of the following:

  * `true` \- to perform initial chunk creation and distribution

  * `false` \- to not perform initial chunk creation and distribution (default)

If omitted, defaults to `false`. This is only available for Atlas clusters
with MongoDB v4.4 and later.  
  
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

    
    
    curl -X POST -i --digest --user "{PUBLIC-KEY}:{PRIVATE-KEY}" -H "Content-Type: application/json" \  
      
      "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c391af480eef519ea5deeb1/clusters/Cluster1/globalWrites/managedNamespaces?pretty=true" \  
      --data '{  
        "db":"mydata",  
        "collection":"publishers",  
        "customShardKey":"city"  
      }'  
  
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
         "collection" : "publishers",  
         "customShardKey" : "city",  
         "db" : "mydata",  
         "isCustomShardKeyHashed": false,  
         "isShardKeyUnique": false,  
         "numInitialChunks": null,  
         "presplitHashedZones": false  
       },{  
         "collection" : "stores",  
         "customShardKey" : "store_number",  
         "db" : "mydata",  
         "isCustomShardKeyHashed": false,  
         "isShardKeyUnique": false,  
         "numInitialChunks": null,  
         "presplitHashedZones": false  
       } ]  
     }  
  
What is MongoDB Atlas? →

