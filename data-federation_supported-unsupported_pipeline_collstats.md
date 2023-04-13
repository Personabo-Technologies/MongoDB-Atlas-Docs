Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `$collStats`

Share Feedback

On this page

  * Syntax
  * Fields
  * Output
  * Examples
  * Errors

`$collStats` returns statistics for a given collection. `$collstats` must be
the first stage in the aggregation pipeline. For more information, see
$collStats. In Data Federation, `$collStats` can only be used to retrieve
information about the partitions for a given collection or view.

## Syntax

In Atlas Data Federation, $collStats accepts an empty document. It supports
the optional field `count` only and returns an error if an unsupported option
is specified.

    
    
    db.<collection-name>|<view-name>.aggregate([{ "$collStats" : { "count" : {} } }])  
      
  
## Fields

Field

|

type

|

Description

|

Necessity  
  
|||  
  
`count`

|

document

|

Adds the total number of documents in the partitions to the return document.

|

Optional  
  
## Output

`$collStats` returns the following fields in the document for each partition:

Field

|

Type

|

Description  
  
||  
  
`count`

|

number

|

The total number of documents in the partition. This is returned only if you
specify the `count` option.  
  
`ns`

|

string

|

The namespace of the current collection or view in the format
`[database].[collection|view]`.  
  
`partition`

|

document

|

The details about the partition such as the source, format, size, and
partition attributes, if any.  
  
`partition.format`

|

string

|

The format of the file. Value can be any of the Supported Data Formats for
data in S3 bucket or `MONGO` for data in the Atlas cluster.  
  
`partition.attributes`

|

document

|

The partition attributes for this partition defined in the `path` for S3
partitions. An empty document indicates that there are no partition attributes
in the partition's data source.  
  
`partition.size`

|

int

|

The size of the partition.  
  
`partition.source`

|

string

|

The source for the partition. The value can be one of the following:

  * The path to the file on S3.

  * The cluster name for partitions on Atlas.

  
  
## Examples

Basic Example

Count Example

The following example shows $collStats syntax for retrieving the partitions
from a `s3Db.abc` collection with 3 files in an S3 federated database instance
store:

    
    
    use s3Db  
      
    db.abc.aggregate([ {$collStats: {}} ])  
  
The preceding command returns the following output:

    
    
    { "ns" : "s3Db.abc", "partition" : { "format" : "JSON", "attributes" : { "year" : NumberLong(2018) }, "size" : 139, "source" : "s3://my-bucket/s3Db/abc/2018/1.json?delimiter=%2F&region=us-east-1" } }  
      
    { "ns" : "s3Db.abc", "partition" : { "format" : "JSON", "attributes" : { "year" : NumberLong(2017) }, "size" : 124, "source" : "s3://my-bucket/s3Db/abc/2017/1.json?delimiter=%2F&region=us-east-1" } }  
    { "ns" : "s3Db.abc", "partition" : { "format" : "JSON", "attributes" : { "year" : NumberLong(2017) }, "size" : 130, "source" : "s3://my-bucket/s3Db/abc/2017/2.json?delimiter=%2F&region=us-east-1" } }  
  
The following example shows $collStats syntax for retrieving the partitions
from the `atlasDb.sampleColl` collection in the Atlas cluster named
`mySandboxCluster`:

    
    
    use atlasDb  
      
    db.sampleColl.aggregate([ {$collStats: {}} ])  
  
The preceding command returns the following output:

    
    
    { "ns" : "atlasDb.sampleColl", "partition" : { "format" : "MONGO", "attributes" : {  }, "size" : 94362191, "source" : "mySandboxCluster" } }  
      
  
## Errors

An error similar to the following is returned if the collStats argument
document contains any of the options allowed by the MongoDB server but not by
Atlas Data Federation.

    
    
    {  
      
           "ok" : 0,  
           "errmsg" : "$collStats param 'latencyStats' is not valid for Data Lake, correlationID = 1622929884a47d16f4888a1c",  
           "code" : 9,  
           "codeName" : "FailedToParse"  
    }  
  
← Supported Aggregation Pipeline Stages and Operators`$lookup` →

