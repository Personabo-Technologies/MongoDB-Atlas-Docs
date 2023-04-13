Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `create`

Share Feedback

On this page

  * Syntax
  * Parameters
  * Output
  * Examples
  * Basic Example
  * Wildcard Usage Examples
  * Multiple Data Sources Example
  * Verify Collection
  * Troubleshoot Errors

The `create` command creates a collection for existing `stores` or a view on a
collection in the federated database instance storage configuration.

The wildcard `"*"` can be used with the `create` command in two ways:

  * As the name of the collection to dynamically create collections that maps to files and folders in the specified `stores` federated database instance store.

  * In the `path` parameter to create a collection that maps to multiple files and folders in the specified file path on the `stores` federated database instance store.

Click on the tab to learn more about creating a collection or a view.

Collection

Views

This tab contains the syntax and parameters for creating a collection. Choose
the tab for your federated database instance store to learn more about the
syntax and parameters for that federated database instance store.

S3

Atlas Cluster

HTTP

Atlas Data Lake

This tab contains the syntax and parameters for creating a collection for S3
federated database instance store.

## Syntax

Collection

Views

S3

Atlas Cluster

HTTP

Atlas Data Lake

    
    
    db.runCommand({ "create" : "<collection-name>|*", "dataSources" : [{ "storeName" : "<store-name>", "path" : "<path-to-files-or-folders>", "defaultFormat" :  "<file-extension>" }]})  
      
  
## Parameters

Collection

Views

S3 Configuration

Atlas Configuration

HTTP Configuration

ADL Configuration

Parameter

|

Type

|

Description

|

Necessity  
  
|||  
  
`<collection-name>|*`

|

string

|

Either the name of the collection to which Data Federation maps the data
contained in the federated database instance store or the wildcard `"*"` to
dynamically create collections.

You can generate collection names dynamically from file paths by specifying
`*` for the collection name and the `collectionName()` function in the
`dataSources.collection` field. By default, Atlas Data Federation creates up
to `100` wildcard collections. You can customize the maximum number of
wildcard collections that Atlas Data Federation automatically generates using
the `databases.[n].maxWildcardCollections` parameter. Note that each wildcard
collection can contain only one `dataSource`.

|

Required  
  
`dataSources`

|

object

|

Array of objects where each object represents a federated database instance
store in the `stores` array to map with the collection.

|

Required  
  
`dataSources.storeName`

|

string

|

Name of a federated database instance store to map to the collection. The
value must match the `stores.[n].name` in the `stores` array.

|

Required  
  
`dataSources.path`

|

string

|

The path to the files and folders. Specify `/` to capture all files and
folders from the `prefix` path. See Define Path for S3 Data for more
information.

|

Required  
  
`dataSources.defaultFormat`

|

string

|

Format that Data Federation defaults to if it encounters a file without an
extension while querying the federated database instance store. The following
values are valid:

`.json, .json.gz, .bson, .bson.gz, .avro, .avro.gz, .orc, .tsv, .tsv.gz, .csv,
.csv.gz, .parquet`

If omitted, Data Federation attempts to detect the file type by processing a
few bytes of the file.

|

Optional  
  
## Output

The command returns the following output if it succeeds. You can verify the
results by running the commands in Verify Collection. If it fails, see
Troubleshoot Errors below for recommended solutions.

    
    
    { ok: 1 }  
      
  
## Examples

Create Collections Examples

Create Views Example

S3 Example

Atlas Example

HTTP Example

Atlas Data Lake Example

The following examples use the sample `airbnb` data on an AWS S3 store with
the following settings:

|  
  
|  
  
 **Store Name**

|

`egS3Store`  
  
 **Region**

|

`us-east-2`  
  
 **Bucket**

|

`test-data-federation`  
  
 **Prefix**

|

`json`  
  
 **Delimiter**

|

`/`  
  
 **Sample Dataset**

|

`airbnb`  
  
### Basic Example

The following command creates a collection named `airbnb` in the `sampleDB`
database in the storage configuration.

S3 Example

Atlas Example

HTTP Example

Atlas Data Lake Example

The `airbnb` collection maps to the `airbnb` sample dataset in the `json`
folder in the S3 store named `egS3Store`.

    
    
    use sampleDB  
      
    db.runCommand({ "create" : "airbnb", "dataSources" : [{ "storeName" : "egS3Store", "path" : "/json/airbnb", "defaultFormat" : ".json" }]})  
  
HIDE OUTPUT

    
    
    { "ok" : 1 }  
      
  
The following commands show that the collection was successfully created:

    
    
    show collections  
      
  
HIDE OUTPUT

    
    
    airbnb  
      
      
    
    db.runCommand({"storageGetConfig" : 1 })  
      
  
HIDE OUTPUT

    
    
    {  
      
            "ok" : 1,  
            "storage" : {  
                    "stores" : [{  
                                  "name" : "egS3Store",  
                                  "provider" : "s3",  
                                  "region" : "us-east-2",  
                                  "bucket" : "test-data-federation",  
                                  "delimiter" : "/",  
                                  "prefix" : ""  
                    }],  
                    "databases" : [{  
                            "name" : "sampleDB",  
                            "collections" : [{  
                                    "name" : "airbnb",  
                                    "dataSources" : [{  
                                            "storeName" : "egS3Store",  
                                            "path" : "/json/airbnb",  
                                            "defaultFormat" : ".json"  
                                    }]  
                            }]  
                    }]  
            }  
    }  
  
### Wildcard Usage Examples

S3 Example

Atlas Example

HTTP Example

Atlas Data Lake Example

These examples show how the wildcard `"*"` can be specified with the `create`
command.

Collection Name Example

Path Glob Example

The following example uses the `create` command to dynamically create
collections.

The following example uses the `create` command to dynamically create
collections for the files in the path `/json/` in the `egS3Store` federated
database instance store. It uses the `collectionName()` function to name the
collections after the filenames in the specified path.

    
    
    use sampleDB  
      
    db.runCommand({ "create" : "*", "dataSources" : [{ "storeName" : "egS3Store", "path": "/json/{collectionName()}"}]})  
  
HIDE OUTPUT

    
    
    { "ok" : 1 }  
      
  
The following commands show that the collection was successfully created:

    
    
    show collections  
      
  
HIDE OUTPUT

    
    
    airbnb  
      
      
    
    db.runCommand({"storageGetConfig" : 1 })  
      
  
HIDE OUTPUT

    
    
    {  
      
      "ok" : 1,  
      "storage" : {  
        "stores" : [{  
          "name" : "egS3Store",  
          "provider" : "s3",  
          "region" : "us-east-2",  
          "bucket" : "test-data-federation",  
          "delimiter" : "/",  
          "prefix" : ""  
        }],  
        "databases" : [{  
          "name" : "sampleDB",  
          "collections" : [{  
            "name" : "*",  
            "dataSources" : [{  
              "storeName" : "egS3Store",  
              "path" : "/json/{collectionName()}"  
            }]  
          }]  
        }]  
      }  
    }  
  
### Multiple Data Sources Example

The following command creates a collection named `egCollection` in the
`sampleDB` database in the storage configuration. The `egCollection`
collection maps to the following sample datasets:

  * `airbnb` dataset in the `json` folder in the S3 store named `egS3Store`

  * `airbnb` dataset in the `sample_airbnb.listingsAndReviews` collection on the Atlas cluster named `myTestCluster`

  * `airbnb` dataset in the URL `https://atlas-data-lake.s3.amazonaws.com/json/sample_airbnb/listingsAndReviews.json`

    
    
    use sampleDB  
      
    db.runCommand({ "create" : "egCollection", "dataSources" : [{ "storeName" : "egS3Store", "path" : "/json/airbnb" },{ "storeName" : "egAtlasStore", "database": "sample_airbnb", "collection": "listingsAndReviews" },{"storeName" : "egHttpStore", "urls": ["https://atlas-data-lake.s3.amazonaws.com/json/sample_airbnb/listingsAndReviews.json"]}]})  
  
HIDE OUTPUT

    
    
    { "ok" : 1 }  
      
  
The following commands show that the collection was successfully created:

    
    
    show collections  
      
  
HIDE OUTPUT

    
    
    egCollection  
      
      
    
    db.runCommand({"storageGetConfig":1})  
      
  
HIDE OUTPUT

    
    
    {  
      
           "ok" : 1,  
           "storage" : {  
                  "stores" : [  
                         {  
                                "name" : "egS3Store",  
                                "provider" : "s3",  
                             "region" : "us-east-2",  
                                "bucket" : "test-data-federation",  
                                "delimiter" : "/",  
                                "prefix" : ""  
                         },  
                         {  
                                "name" : "egAtlasStore",  
                                "provider" : "atlas",  
                             "clusterName" : "myTestCluster",  
                                "projectId" : "<project-id>"  
                         },  
                         {  
                                "name" : "egHttpStore",  
                                "provider" : "http",  
                                "urls" : ["https://atlas-data-lake.s3.amazonaws.com/json/sample_airbnb/listingsAndReviews.json"]  
                         }  
                  ],  
                  "databases" : [  
                         {  
                           "name" : "sampleDB",  
                           "collections" : [{  
                               "name" : "egCollection",  
                                  "dataSources" : [  
                                         {  
                                           "storeName" : "egS3Store",  
                                           "path" : "json/airbnb"  
                                         },  
                                         {  
                                           "storeName" : "egAtlasStore",  
                                           "database" : "sample_airbnb",  
                                           "collection" : "listingsAndReviews"  
                                         },  
                                         {  
                                           "storeName" : "egHttpStore",  
                                           "urls" : ["https://atlas-data-lake.s3.amazonaws.com/json/sample_airbnb/listingsAndReviews.json"]  
                                         }  
                                   ]  
                           }]  
                         }  
                  ]  
           }  
    }  
  
## Verify Collection

You can verify that the command successfully created the collection or view by
running one of the following commands:

    
    
    show collections  
      
    db.runCommand({ "storageGetConfig" : 1 })  
    db.runCommand({ "listCollections" : 1 })  
  
## Troubleshoot Errors

Collection

Views

If the command fails, it returns one of the following errors:

 **Store Name Does Not Exist**

    
    
     {  
      
            "ok" : 0,  
            "errmsg" : "store name does not exist",  
            "code" : 9,  
            "codeName" : "FailedToParse"  
    }  
  
 **Solution:** Ensure that the specified `storeName` matches the name of a
store in the `stores` array. You can run the `listStores` command to retrieve
the list of stores in your federated database instance storage configuration.

 **Collection Name Already Exists**

    
    
     {  
      
            "ok" : 0,  
            "errmsg" : "collection name already exists in the database",  
            "code" : 9,  
            "codeName" : "FailedToParse"  
    }  
  
 **Solution:** Ensure that the collection `name` is unique. You can run the
`show collections` command to retrieve the list of existing collections.

← `listStores``renameCollection` →

