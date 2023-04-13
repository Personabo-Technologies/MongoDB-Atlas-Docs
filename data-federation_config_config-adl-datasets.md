Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Atlas Data Lake Datasets

Share Feedback

On this page

  * Example Configuration for Atlas Data Lake Data Store
  * Configuration Format
  * `stores`
  * `databases`

Atlas Data Federation supports Atlas Data Lake datasets as federated database
instance stores. You must define mappings in your federated database instance
storage configuration to your Data Lake dataset to run queries against your
data.

## Important

Information in your storage configuration is visible internally at MongoDB and
stored as operational data to monitor and improve the performance of Atlas
Data Federation. We recommend that you don't use PII in your configurations.

## Example Configuration for Atlas Data Lake Data Store

## Example

Consider an Atlas Data Lake pipeline named `myDataCenter` containing snapshot
data from the `metrics.hardware` collection. The `metrics.hardware` collection
contains JSON documents with metrics derived from the hardware in a
datacenter. The following configuration:

  * Specifies the cloud storage provider `dls:aws` and the provider region `us-east-1` as a federated database instance store.

  * Maps documents from the snapshots of `metrics.hardware` collection on the Atlas cluster name `dlsTest` to the `dataCenter.inventory` collection in the storage configuration. For example, when the Atlas Data Lake pipeline runs on May 5, 2022 at 02:00:10 UTC, Atlas Data Lake creates a dataset with the dataset name `v1$atlas$snapshot$dlsTest$metrics$hardware$20220510T020010Z`.

    
    
    {  
      
      "stores": [  
        {  
          "name": "adlStore",  
          "provider": "dls:aws",  
          "region": "us-east-1"  
        }  
      ],  
      "databases": [  
        {  
          "name": "datacenter",  
          "collections": [  
            {  
              "name": "inventory",  
              "dataSources": [  
                {  
                  "storeName": "adlStore",  
                  "datasetName": "v1$atlas$snapshot$dlsTest$metrics$hardware$20220510T020010Z"  
                }  
              ]  
            }  
          ],  
          "views": []  
        }  
      ]  
    }  
  
Atlas Data Federation maps all the documents in the snapshots to the
`dataCenter.inventory` collection in the storage configuration.

Users connected to the federated database instance can use the MongoDB Query
Language and supported aggregations to query historical data in the snapshot
through the `datacenter.inventory` collection. When you run queries, the query
first goes to Atlas Data Federation. Therefore, if you run aggregation queries
that are supported by your Atlas cluster but not by Atlas Data Federation, the
queries will fail. To learn more about supported and unsupported commands in
Data Federation, see Supported MongoDB Commands.

## Configuration Format

The federated database instance configuration for an Atlas Data Lake dataset
has the following format:

    
    
    1| {  
    |  
    2|   "stores" : [  
    3|     {  
    4|       "name" : "<string>",  
    5|       "provider": "<string>",  
    6|       "region": "<string>"  
    7|     }  
    8|   ],  
    9|   "databases" : [  
    10|       {  
    11|         "name" : "<string>",  
    12|         "collections" : [  
    13|           {  
    14|             "name" : "<string>",  
    15|             "dataSources" : [  
    16|               {  
    17|                 "storeName" : "<string>",  
    18|                 "datasetName" : "<string>",  
    19|                 "datasetPrefix": "<string>",  
    20|                 "trimLevel": <int>,  
    21|                 "provenanceFieldName": "<string>"  
    22|               }  
    23|             ]  
    24|           }  
    25|         ],  
    26|         "views" : [   
    27|           {  
    28|             "name" : "<string>",   
    29|             "source" : "<string>",   
    30|             "pipeline" : "<string>"   
    31|           }  
    32|         ]   
    33|       }  
    34|   ]  
    35| }  
    36|     
  
### `stores`

    
    
    1| "stores" : [  
    |  
    2|   {  
    3|     "name" : "<string>",  
    4|     "provider": "<string>",  
    5|     "region": "<string>"  
    6|   }  
    7| ]  
  
`stores`

    

Array of objects where each object represents a data store to associate with
the federated database instance. The federated database instance store
references files in an S3 bucket, documents in an Atlas cluster, files stored
at publicly accessible URLs, or Atlas Data Lake datasets. Atlas Data
Federation can only access data stores defined in the `stores` object.

`stores.[n].name`

    

Name of the federated database instance store. The
`databases.[n].collections.[n].dataSources.[n].storeName` field references
this value as part of mapping configuration.

`stores.[n].provider`

    

Cloud provider where the snapshot data is stored. Value must be
`dls:<subtype>` for a snapshot. Atlas Data Federation only supports `aws` as
subtype. Therefore, this value must be `dls:aws`.

`stores.[n].region`

    

Region name of your Data Lake. Each store is associated with a single region,
where both the metadata and snapshot data are stored. If you have multiple
datasets in different regions, you must add a store for each region to map
data in that region to virtual databases and collection in federated database
instance.

### `databases`

    
    
    1| "databases" : [  
    |  
    2|   {  
    3|     "name" : "<string>",  
    4|     "collections" : [  
    5|       {  
    6|         "name" : "<string>",  
    7|         "dataSources" : [  
    8|           {  
    9|             "storeName" : "<string>",  
    10|             "datasetName" : "<string>",  
    11|             "datasetPrefix": "<string>",  
    12|             "trimLevel": <int>,  
    13|             "provenanceFieldName": "<string>"  
    14|           }  
    15|         ]  
    16|       }  
    17|     ],  
    18|     "views" : [   
    19|       {  
    20|         "name" : "<string>",   
    21|         "source" : "<string>",   
    22|         "pipeline" : "<string>"   
    23|       }  
    24|     ]   
    25|   }  
    26| ]  
  
`databases`

    

Array of objects that define the mapping between each federated database
instance store defined in `stores` and Atlas Data Lake datasets. Each object
represents a database, its collections, and, optionally, any views on the
collections. Each database can have multiple `collections` and `views`
objects.

`databases.[n].name`

    

Name of the database to which Atlas Data Federation maps the data contained in
the data store.

`databases.[n].collections`

    

Array of objects where each object represents a collection and data sources
that map to a `stores` federated database instance store.

`databases.[n].collections.[n].name`

    

Name of the collection to which Atlas Data Federation maps the data contained
in each `databases.[n].collections.[n].dataSources.[n].storeName`. Each object
in the array represents the mapping between the collection and an object in
the `stores` array.

You can generate collection names dynamically by specifying `*` for the
collection name. To dynamically generate collection names, you must also
specify the following:

  * `databases.[n].collections.[n].dataSources.[n].datasetPrefix`

  * `databases.[n].collections.[n].dataSources.[n].trimLevel`

For wildcard collections, Atlas Data Federation maps a dataset name to a
collection name first by splitting the namespace into a list of fields on the
`$` delimiter, then by trimming a number of fields from the left of the list,
and finally by combining the remaining fields using `_`.

`databases.[n].collections.[n].dataSources`

    

Array of objects where each object represents a federated database instance
store in the `stores` array to map with the collection. You can specify
multiple `dataSources` for a wildcard collection only if all the `dataSources`
for the collection map to Atlas Data Lake dataset `stores`.

`databases.[n].collections.[n].dataSources.[n].storeName`

    

Name of a federated database instance store to map to the `<collection>`. Must
match the `name` of an object in the `stores` array.

`databases.[n].collections.[n].dataSources.[n].datasetName`

    

Name of the Atlas Data Lake dataset to map with the collection. The Atlas Data
Lake `datasetName` is in the following format:

    
    
    <version>$<type>$<subtype>$<clusterName>$<dbName>$<collectionName>$<snapshotId>  
      
  
## Example

Consider the following Atlas Data Lake dataset name.

    
    
    v1$atlas$snapshot$clusterName$dbName$collectionName$snapshotId  
      
  
Here:

  * `v1` is the version

  * `atlas` is the type of data source

  * `snapshot` is the subtype

  * `clusterName` is the name of the Atlas cluster

  * `dbName` is the name of the database on the Atlas cluster

  * `collectionName` is the collection in the database

  * `snapshotId` is the unique identifier of the snapshot of the data in the collection

`databases.[n].collections.[n].dataSources.[n].datasetPrefix`

    

Dataset name prefix to match against Atlas Data Lake dataset names. You can
set this setting for wildcard collections only. If specified, Atlas Data
Federation maps collections to only the dataset names whose prefix match the
value specified here.

`databases.[n].collections.[n].dataSources.[n].trimLevel`

    

Unsigned integer that specifies how many fields of the dataset name to trim
from the left of the dataset name before mapping the remaining fields to a
wildcard collection name. Value must be greater than `0` and less than `7`.
You can set this setting for wildcard collections only.

## Example

Consider the following Atlas Data Lake dataset name:

    
    
    v1$atlas$snapshot$MyCluster$MyDB$MyCollection$snapshotDate  
      
  
Atlas Data Federation dynamically generates the following collection names for
different trim levels:

Trim Level

|

Collection Name  
  
|  
  
`5`

|

`MyCollection_snapshotDate`  
  
`4`

|

`MyDB_MyCollection_snapshotDate`  
  
`3`

|

`MyCluster_MyDB_MyCollection_snapshotDate`  
  
`2`

|

`snapshot_MyCluster_MyDB_MyCollection_snapshotDate`  
  
`1`

|

`atlas_snapshot_atlas_MyCluster_MyDB_MyCollection_snapshotDate`  
  
`0`

|

`v1_atlas_snapshot_atlas_MyCluster_MyDB_MyCollection_snapshotDate`  
  
You can't configure this setting using the Visual Editor in the Atlas UI.
Therefore, this setting defaults to trim level `5` for configurations using
the Visual Editor.

`databases.[n].collections.[n].dataSources.[n].provenanceFieldName`

    

Name for the field that includes the provenance of the documents in the
results. If you specify this setting in the storage configuration, Atlas Data
Federation returns the following fields for each document in the result:

Field Name

|

Description  
  
|  
  
`provider`

|

Provider (`stores.[n].provider`) in the federated database instance storage
configuration  
  
`clusterName`

|

Name of the Atlas cluster  
  
`databaseName`

|

Name of the database on the Atlas cluster  
  
`collectionName`

|

Name of the collection  
  
`snapshotID`

|

Unique 24-hexadecimal character string that identifies the snapshot  
  
`dataSetName`

|

Name of the Data Lake dataset
(`databases.[n].collections.[n].dataSources.[n].datasetName`)  
  
You can't configure this setting using the Visual Editor in the Atlas UI.

← Create From the UICreate From the UI →

