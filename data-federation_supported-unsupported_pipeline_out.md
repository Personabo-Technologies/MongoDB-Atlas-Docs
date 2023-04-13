Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# `$out`

Share Feedback

On this page

  * Permissions Required
  * Syntax
  * Fields
  * Options
  * Examples
  * Simple String Example
  * Single Field from Documents
  * Multiple Fields from Documents
  * Multiple Types of Fields from Documents
  * Write to Collection on Atlas Cluster
  * Run Query in the background
  * Limitations
  * String Data Type
  * Number of Unique Fields
  * CSV and TSV File Format
  * Parquet File Format
  * Errors

$out takes documents returned by the aggregation pipeline and writes them to a
specified collection. The $out operator must be the last stage in the
aggregation pipeline. In Atlas Data Federation, you can use $out to write data
from any one of the supported federated database instance stores or multiple
supported federated database instance stores when using federated queries to
any one of the following:

  * S3 buckets with read and write permissions

  * Atlas cluster namespace

You must connect to your federated database instance to use $out.

S3

Atlas Cluster

## Permissions Required

S3

Atlas Cluster

You must have:

  * A federated database instance configured for S3 bucket with read and write permissions or s3:PutObject permissions.

  * A MongoDB user with atlasAdmin role.

## Syntax

S3

Atlas Cluster

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "<bucket-name>",  
    5|       "region": "<aws-region>",  
    6|       "filename": "<file-name>",  
    7|       "format": {  
    8|         "name": "<file-format>",  
    9|         "maxFileSize": "<file-size>",  
    10|         "maxRowGroupSize": "<row-group-size>",  
    11|         "columnCompression": "<compression-type>"  
    12|       },  
    13|       "errorMode": "stop"|"continue"  
    14|     }  
    15|   }  
    16| }  
  
## Fields

S3

Atlas Cluster

Field

|

Type

|

Description

|

Necessity  
  
|||  
  
`s3`

|

object

|

Location to write the documents from the aggregation pipeline.

|

Required  
  
`s3.bucket`

|

string

|

Name of the S3 bucket to write the documents from the aggregation pipeline to.

## Important

The generated call to S3 inserts a `/` between `s3.bucket` and `s3.filename`.
Don't append a `/` after the `s3.bucket`.

## Example

If you set `s3.bucket` to `myBucket` and `s3.filename` to `myPath/myData`,
Atlas Data Federation writes this out as
`s3://myBucket/myPath/myData.[n].json`.

|

Required  
  
`s3.region`

|

string

|

Name of the AWS region in which the bucket is hosted. If omitted, uses the
federated database instance configuration to determine the region where the
specified `s3.bucket` is hosted.

|

Optional  
  
`s3.filename`

|

string

|

Name of the file to write the documents from the aggregation pipeline to.
Filename can be constant or created dynamically from the fields in the
documents that reach the $out stage. Any filename expression you provide must
evaluate to a `string` data type. If there are any files on S3 with the same
name and path as the newly generated files, $out overwrites the existing files
with the newly generated files.

## Important

The generated call to S3 inserts a `/` between `s3.bucket` and `s3.filename`.
Don't prepend a `/` before the `s3.filename`. If you set `s3. bucket` to
`myBucket` and `s3.filename` to `myPath/myData`, Atlas Data Federation writes
this out as `s3://myBucket/myPath/myData.[n].json`.

|

Required  
  
`s3.format`

|

object

|

Details of the file in S3.

|

Required  
  
`s3`

`.format`

`.name`

|

enum

|

Format of the file in S3. Value can be one of the following:

  * `bson`

  * `bson.gz`

  * `csv`

  * `csv.gz`

  * `json` 1

  * `json.gz` 1

  * `parquet`

  * `tsv`

  * `tsv.gz`

1 For this format, $out writes data in MongoDB Extended JSON format.

## Tip

### See also:

Limitations

|

Required  
  
`s3`

`.format`

`.maxFileSize`

|

bytes

|

Maximum size of the file in S3. When the file size limit for the current file
is reached, a new file is created in S3. The first file appends a `1` before
the filename extension. For each subsequent file, the Atlas Data Federation
increments the appended number by one.

## Example

`<filename>.1.<fileformat>`

`<filename>.2.<fileformat>`

If a document is larger than the `maxFileSize`, Data Federation writes the
document to its own file. The following suffixes are supported:

|

|  
  
|  
  
Base 10: scaling in multiples of 1000

|

  * `B`

  * `KB`

  * `MB`

  * `GB`

  * `TB`

  * `PB`

  
  
Base 2: scaling in multiples of 1024

|

  * `KiB`

  * `MiB`

  * `GiB`

  * `TiB`

  * `PiB`

  
  
If omitted, defaults to `200MiB`.

Optional  
  
`s3`

`.format`

`.maxRowGroupSize`

|

string

|

Supported for Parquet file format only.

Maximum row group size to use when writing to Parquet file. If omitted,
defaults to `128 MiB` or the value of the `s3.format.maxFileSize`, whichever
is smaller. The maximum allowed value is `1 GB`.

|

Optional  
  
`s3`

`.format`

`.columnCompression`

|

string

|

Supported for Parquet file format only.

Compression type to apply for compressing data inside a Parquet file when
formatting the Parquet file. Valid values are:

  * `gzip`

  * `snappy`

  * `uncompressed`

If omitted, defaults to `snappy`.

## Tip

### See also:

Supported Data Formats

|

Optional  
  
`errorMode`

|

enum

|

Specifies how Atlas Data Federation should proceed if there are errors when
processing a document. For example, if Atlas Data Federation encounters an
array in a document when Atlas Data Federation is writing to a CSV file, Atlas
Data Federation uses this value to determine whether or not to skip the
document and process other documents. Valid values are:

  * `continue` to skip the document and continue processing the remaining documents. Atlas Data Federation also writes the document that caused the error to an error file.

## Tip

### See also:

Errors

  * `stop` to stop at that point and not process the remaining documents.

If omitted, defaults to `continue`.

|

Optional  
  
## Options

Option

|

Type

|

Description

|

Necessity  
  
|||  
  
`background`

|

boolean

|

Flag to run aggregation operations in the background. If omitted, defaults to
`false`. When set to `true`, Atlas Data Federation runs the queries in the
background.

    
    
    | { "background" : true }  
      
  
Use this option if you want to submit other new queries without waiting for
currently running queries to complete or disconnect your federated database
instance connection while the queries continue to run in the background.

Optional  
  
## Examples

S3

Atlas Cluster

 **Create a Filename**

The following examples show $out syntaxes for dynamically creating a filename
from a constant string or from the fields of the same or different data types
in the documents that reach the $out stage.

### Simple String Example

## Example

You want to write 1 GiB of data as compressed BSON files to an S3 bucket named
`my-s3-bucket`.

Using the following $out syntax:

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "my-s3-bucket",  
    5|       "filename": "big_box_store/",  
    6|       "format": {  
    7|         "name": "bson.gz"  
    8|       }  
    9|     }  
    10|   }  
    11| }  
  
The `s3.region` is omitted and so, Data Federation determines the region where
the bucket named `my-s3-bucket` is hosted from the storage configuration. $out
writes five compressed BSON files:

  1. The first 200 MiB of data to a file that $out names `big_box_store/1.bson.gz`.

## Note

    * The value of `s3.filename` serves as a constant in each filename. This value doesn't depend upon any document field or value.

    * Your `s3.filename` ends with a delimiter, so Atlas Data Federation appends the counter after the constant.

    * If it didn't end with a delimiter, Atlas Data Federation would have added a `.` between the constant and the counter, like `big_box_store.1.bson.gz`

    * As you didn't change the maximum file size using `s3.format.maxFileSize`, Atlas Data Federation uses the default value of 200 MiB.

  2. The second 200 MiB of data to a new file that $out names `big_box_store/2.bson.gz`.

  3. Three more files that $out names `big_box_store/3.bson.gz` through `big_box_store/5.bson.gz`.

### Single Field from Documents

## Example

You want to write 90 MiB of data to JSON files to an S3 bucket named
`my-s3-bucket`.

Using the following $out syntax:

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "my-s3-bucket",  
    5|       "region": "us-east-1",  
    6|       "filename": {"$toString": "$sale-date"},  
    7|       "format": {  
    8|         "name": "json",  
    9|         "maxFileSize": "100MiB"  
    10|       }  
    11|     }  
    12|   }  
    13| }  
  
$out writes 90 MiB of data to JSON files in the root of the bucket. Each JSON
file contains all of the documents with the same `sale-date` value. $out names
each file using the documents' `sale-date` value converted to a string.

### Multiple Fields from Documents

## Example

You want to write 176 MiB of data as BSON files to an S3 bucket named
`my-s3-bucket`.

Using the following $out syntax:

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "my-s3-bucket",  
    5|       "region": "us-east-1",  
    6|       "filename": {  
    7|         "$concat": [  
    8|           "persons/",  
    9|           "$name", "/",  
    10|           "$unique-id", "/"  
    11|         ]  
    12|       },  
    13|       "format": {  
    14|         "name": "bson",  
    15|         "maxFileSize": "200MiB"  
    16|       }  
    17|     }  
    18|   }  
    19| }  
  
$out writes 176 MiB of data to BSON files. To name each file, $out
concatenates:

  * A constant string `persons/` and, from the documents:

    * The string value of the `name` field,

    * A forward slash (`/`),

    * The string value of the `unique-id` field, and

    * A forward slash (`/`).

Each BSON file contains all of the documents with the same `name` and `unique-
id` values. $out names each file using the documents' `name` and `unique-id`
values.

### Multiple Types of Fields from Documents

## Example

You want to write 154 MiB of data as compressed JSON files to an S3 bucket
named `my-s3-bucket`.

Consider the following $out syntax:

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "my-s3-bucket",  
    5|       "region": "us-east-1",  
    6|       "filename": {  
    7|         "$concat": [  
    8|           "big-box-store/",  
    9|           {  
    10|             "$toString": "$store-number"  
    11|           }, "/",  
    12|           {  
    13|             "$toString": "$sale-date"  
    14|           }, "/",  
    15|           "$part-id", "/"  
    16|         ]  
    17|       },  
    18|       "format": {  
    19|         "name": "json.gz",  
    20|         "maxFileSize": "200MiB"  
    21|       }  
    22|     }  
    23|   }  
    24| }  
  
$out writes 154 MiB of data to compressed JSON files, where each file contains
all documents with the same `store-number`, `sale-date`, and `part-id` values.
To name each file, $out concatenates:

  * A constant string value of `big-box-store/`,

  * A string value of a unique store number in the `store-number` field,

  * A forward slash (`/`),

  * A string value of the date from the `sale-date` field,

  * A forward slash (`/`),

  * A string value of part ID from the `part-id` field, and

  * A forward slash (`/`).

### Run Query in the background

The following example shows $out syntax for running an aggregation pipeline
that ends with the $out stage in the background.

S3

Atlas Cluster

## Example

    
    
    db.mySampleData.aggregate(  
      
      [  
        {  
          "$out": {  
            "atlas": {  
              "clusterName":"myTestCluster",  
              "db":"sampleDB",  
              "coll":"mySampleData"  
            }  
          }  
        }  
      ],  
      { "background" : true }  
    )  
  
$out writes to JSON files in the root of the bucket in the background. Each
JSON file contains all of the documents with the same `sale-date` value. $out
names each file using the documents' `sale-date` value converted to a string.

## Limitations

S3

Atlas Cluster

### String Data Type

Data Federation interprets empty strings (`""`) as `null` values when parsing
filenames. If you want Data Federation to generate parseable filenames, wrap
the field references that could have `null` values using $convert with an
empty string `onNull` value.

## Example

This example shows how to handle null values in the `year` field when creating
a filename from the field value.

    
    
    1| {  
    |  
    2|   "$out": {  
    3|     "s3": {  
    4|       "bucket": "my-s3-bucket",  
    5|       "region": "us-east-1",  
    6|       "filename": {  
    7|         "$concat": [  
    8|           "big-box-store/",  
    9|           {  
    10|             "$convert": {  
    11|               "input": "$year",  
    12|               "to": "string",  
    13|               "onNull": ""  
    14|             }  
    15|           }, "/"  
    16|         ]  
    17|       },  
    18|       "format": {  
    19|         "name": "json.gz",  
    20|         "maxFileSize": "200MiB"  
    21|       }  
    22|     }  
    23|   }  
    24| }  
  
### Number of Unique Fields

When writing to CSV, TSV, or Parquet file format, Atlas Data Federation
doesn't support more than 2500 unique fields.

### CSV and TSV File Format

When writing to CSV or TSV format, Atlas Data Federation does not support the
following data types in the documents:

  * Arrays

  * DB pointer

  * JavaScript

  * JavaScript code with scope

  * Minimum or maximum key data type

In a CSV file, Atlas Data Federation represents nested documents using the dot
(`.`) notation. For example, Atlas Data Federation writes `{ x: { a: 1, b: 2 }
}` as the following in the CSV file:

    
    
    x.a,x.b  
      
    1,2  
  
Atlas Data Federation represents all other data types as strings. Therefore,
the data types in MongoDB read back from the CSV file may not be the same as
the data types in the original BSON documents from which the data types were
written.

### Parquet File Format

For Parquet, Atlas Data Federation reads back fields with null or undefined
values as missing because Parquet doesn't distinguish between null or
undefined values and missing values. Although Atlas Data Federation supports
all data types, for BSON data types that do not have a direct equivalent in
Parquet, such as JavaScript, regular expression, etc., it:

  * Chooses a representation that allows the resulting Parquet file to be read back using a non-MongoDB tool.

  * Stores a MongoDB schema in the Parquet file's key/value metadata so that Atlas Data Federation can reconstruct the original BSON document with the correct data types if the Parquet file is read back by Atlas Data Federation.

## Example

Consider the following BSON documents:

    
    
    {  
      
      "clientId": 102,  
      "phoneNumbers": ["123-4567", "234-5678"],  
      "clientInfo": {  
        "name": "Taylor",  
        "occupation": "teacher"  
      }  
    }  
    {  
      "clientId": "237",  
      "phoneNumbers" ["345-6789"]  
      "clientInfo": {  
        "name": "Jordan"  
      }  
    }  
  
If you write the preceding BSON documents to Parquet format using $out to S3,
the Parquet file schema for your BSON documents would look similar to the
following:

    
    
    message root {  
      
      optional group clientId {  
        optional int32 int;  
        optional binary string; (STRING)  
      }  
      optional group phoneNumbers (LIST) {  
        repeated group list {  
          optional binary element (STRING);  
        }  
      }  
      optional group clientInfo {  
        optional binary name (STRING);  
        optional binary occupation (STRING);  
      }  
    }  
  
Your Parquet data on S3 would look similar to the following:

    
    
    1| clientId:  
    |  
    2| .int = 102  
    3| phoneNumbers:  
    4| .list:  
    5| ..element = "123-4567"  
    6| .list:  
    7| ..element = "234-5678"  
    8| clientInfo:  
    9| .name = "Taylor"  
    10| .occupation = "teacher"  
    11|   
      
    12| clientId:  
    13| .string = "237"  
    14| phoneNumbers:  
    15| .list:  
    16| ..element = "345-6789"  
    17| clientInfo:  
    18| .name = "Jordan"  
  
The preceding example demonstrates how Atlas Data Federation handles complex
data types:

  * Atlas Data Federation maps documents at all levels to a Parquet group.

  * Atlas Data Federation encodes arrays using the `LIST` logical type and the mandatory three-level list or element structure. To learn more, see Lists.

  * Atlas Data Federation maps polymorphic BSON fields to a group of multiple single-type columns because Parquet doesn't support polymorphic columns. Atlas Data Federation names the group after the BSON field. In the preceding example, Atlas Data Federation creates a Parquet group named `clientId` for the poymorphic field named `clientId` with two children named after its BSON types, `int` and `string`.

## Errors

S3

Atlas Cluster

  * If the filename is not of type string, Data Federation writes documents to a special error file in your bucket.

  * If the documents cannot be written to a file with the specified filename, Data Federation writes documents to ordinally-named files in the specified format and specified size.

## Example

    * `s3://{<bucket-name>}/atlas-data-federation-{<correlation-id>}/out-error-docs/1.json`

    * `s3://{<bucket-name>}/atlas-data-federation-{<correlation-id>}/out-error-docs/2.json`

Data Federation returns an error message that specifies the number of
documents that had invalid filenames and the directory where these documents
were written.

  * If Data Federation encounters an error while processing a document, it writes the document to a special error file in your bucket.
    
        s3://{<bucket-name>}/atlas-data-federation-{<correlation-id>}/out-error-docs/{<n>}.json  
      
  
where `n` is the index of the document being written.

Data Federation also writes the error message for each document to an error
index file:

    
        s3://{<bucket-name>}/atlas-data-federation-{<correlation-id>}/out-error-index/{<i>}.json  
      
  
where `i` begins with `1`. Data Federation writes error messages to the file
until the file reaches the `maxFileSize` and then, Data Federation increments
the value of `i` and continues writing any further error messages to the new
file.

The error messages in the error index file look similar to the following:

## Example

    
        {  
      
            "n": 1234,  
            "error": "field \"foo\" is of type array, which is not supported for CSV"  
    }  
  
where `n` is the index of the document which caused the error.

Data Federation also creates an error summary file after running the entire
query:

    
        s3://{<bucket-name>}/atlas-data-federation-{<correlation-id>}/out-error-summary.json  
      
  
The summary file contains a single document for each type of error and a count
of the number of documents which caused that type of error.

## Example

    
        {  
      
            "errorType": "field is of type array, which is not supported for CSV",  
            "count": 10  
    }  
  

## Tip

### See also:

  * $out Aggregation Stage Reference

  * Tutorial: Federated Queries and $out to S3

← `$merge`Retrieve Federated Database Instance Query History →

