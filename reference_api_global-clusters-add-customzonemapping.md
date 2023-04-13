Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Add Custom Zone Mappings

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

Add an entry to the list of custom zone mappings for the specified Global
Cluster.

## Syntax

    
    
    POST /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/globalWrites/customZoneMapping  
      
  
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

The request body for this endpoint requires a document with at least one
custom zone mapping, as shown in the following example:

    
    
    { "customZoneMappings": [ { "location": <code>, "zone": <zone>}, ... ] }  
      
  
Name

|

Type

|

Description  
  
||  
  
`customZoneMappings`

|

document array

|

Each document in the array maps one ISO location code to a zone in your Global
Cluster.  
  
`customZoneMappings[n].location`

|

string

|

 _Required_ The ISO location code to which you want to map a zone in your
Global Cluster. You can find a list of all supported location codes here.  
  
`customZoneMappings[n].zone`

|

string

|

 _Required_ The name of the zone in your Global Cluster that you want to map
to `location`.  
  
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
Cluster. By default, Atlas maps each location code to the closest geographical
zone. Custom zone mappings allow administrators to override these automatic
mappings.  
  
`managedNamespaces`

|

array of documents

|

Each document specifies a namespace for a Global Cluster managed by Atlas. For
more information, see Global Clusters.  
  
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
  
## Example

### Request

    
    
    curl -X POST -i -u "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest -H "Content-Type: application/json" \  
      
     "https://cloud.mongodb.com/api/atlas/v1.0/groups/6c391af480eef519ea5ceeb1/clusters/GlobalCluster1/globalWrites/customZoneMapping?pretty=true" \  
     --data '{  
       "customZoneMappings" : [{  
          "location":"CA",  
          "zone": "Zone 1"  
          }]  
       }'  
  
### Response

    
    
    {  
      
       "customZoneMapping" : {  
          "CA" : "5b50bf4180eef547653df4d0"  
       },  
       "managedNamespaces" : [ {  
          "collection" : "publishers",  
          "customShardKey" : "city",  
          "db" : "myData"  
       } ]  
    }  
  
What is MongoDB Atlas? →

