Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Use Partition Attribute Types

Share Feedback

On this page

  * Supported Partition Attribute Types
  * Supported Conversions

## Note

When specifying the `path`:

  * Specify the data type for the partition attribute.

  * Ensure that the partition attribute type matches the data type to parse.

  * Use the delimiter specified in `delimiter`.

## Supported Partition Attribute Types

The following table lists the supported data types for partition attributes,
filename, and `path` example for each data type:

Key

|

Data Type

|

Example  
  
||  
  
`string`

|

Parses the filename as a string.

|

filename: `/employees/949-555-0195.json`

path: `/employees/{phone string}`

In the preceding example, Data Federation interprets `phone` as a string.

## Tip

### See also:

Parsing Null Values from Filenames  
  
`int`

|

Parses the filename as an integer.

|

filename: `/zipcodes/90210.json`

path: `/zipcodes/{zipcode int}`

In the preceding example, Data Federation interprets `zipcode` as an integer.

## Tip

### See also:

Parsing Padded Numbers from Filenames  
  
`isodate`

|

Parses the filename in RFC 3339 format as an ISO-8601 format date.

|

filename: `/metrics/20060102.json`

  * path: `/metrics/{startTimestamp isodate}`

  * path: `/metrics/{startTimestamp isodate('20060102')}`

In the preceding example, for the first path, Data Federation interprets
`startTimestamp` as an ISODate. For the second path, Data Federation
interprets `startTimestamp` as an ISODate in the specified format and matches
only filenames in the specified format.

If you don't specify a specific format as shown in the first ISODate attribute
path example above, Atlas Data Federation defaults to partitions with the
following date formats:

    
    
    | 1| "2006-01-02T15:04:05Z07:00"  
    |  
    2| "2006-01-02T15:04:05.000000Z07:00"  
    3| "2006-01-02"  
    4| "2006-01-02T15:04:05.000000-0700"  
    5| "2006-01-02T15:04:05-0700"  
    6| "2006-01-02T15:04Z07:00"  
    7| "2006-01-02T15:04-0700"  
    8| "2006-01-02Z07:00"  
    9| "2006-01-02-0700"  
    10| "2006102T15:04:05.000000Z07:00"  
    11| "20060102T15:04:05.000000-0700"  
    12| "20060102T15:04:05Z07:00"  
    13| "20060102T15:04:05-0700"  
    14| "20060102T15:04Z07:00"  
    15| "20060102T15:04-0700"  
    16| "20060102Z07:00"  
    17| "20060102-0700"  
    18| "20060102"  
  
If you wish to specify a format, which improves performance, you must use
special values to indicate the exact position of the attributes in the date
such as day (`02`), month (`01`), year (`2006`), etc. To learn more about the
format and the values used to specify date, see Format a time or date. If you
specify a format that isn't in a RFC 3339 format, you must use regex with the
special values to indicate the position of the date attributes. For an
example, see Create Partitions from ISODate.  
  
`epoch_secs`

|

Parses the filename as a Unix timestamp in seconds.

|

filename: `/metrics/1549046112.json`

path: `/metrics/{startTimestamp epoch_secs}`

In the preceding example, Data Federation interprets `startTimestamp` as a
Unix timestamp in seconds.

## Tip

### See also:

Parsing Padded Numbers from Filenames  
  
`epoch_millis`

|

Parses the filename as a Unix timestamp in milliseconds.

|

filename: `/metrics/1549046112000.json`

path: `/metrics/{startTimestamp epoch_millis}`

In the preceding example, Data Federation interprets `startTimestamp` as a
Unix timestamp in milliseconds.

## Tip

### See also:

Parsing Padded Numbers from Filenames  
  
`objectid`

|

Parses the filename as an ObjectId.

|

filename: `/metrics/507f1f77bcf86cd799439011.json`

path: `/metrics/{objid objectid}`

In the preceding example, Data Federation interprets `objid` as an ObjectId.  
  
`uuid`

|

Parses the filename as a UUID of binary subtype 4.

|

filename: `/metrics/3b241101-e2bb-4255-8caf-4136c566a962.json`

path: `/metrics/{myUuid uuid}`

In the preceding example, Data Federation interprets `myUuid` as a UUID of
binary subtype 4.  
  
## Note

Atlas Data Federation supports the Package Syntax for regular expressions in
the path to the filename.

## Supported Conversions

Atlas Data Federation converts the partition attributes to BSON types when
parsing the `path` to the filename. Later writes of data to S3 must use the
BSON types after converting them to string. The following table shows:

  * The partition attribute types and the BSON types to which Data Federation converts them.

  * The BSON data type to convert to a string for later writes to S3.

Partition Attribute Type

|

Parsed BSON Type

|

Source BSON Type  
  
||  
  
`string`

|

  * UTF-8 string

  * null*

|

  * UTF-8 string

  * null

  
  
`int`

|

  * 64-bit integer

  * null

|

  * 32-bit integer

  * 64-bit integer

  * null (as strings with no padding)

  
  
`isodate`

|

  * UTC datetime

  * null

|

  * UTC datetime (as an ISO-8601 format string)

  * null

  
  
`objectid`

|

  * ObjectId

  * null

|

  * ObjectId (as a string with hex encoding)

  * null

  
  
`uuid`

|

  * BSON Binary data subtype 4 (UUID)

  * null

|

  * BSON Binary data subtype 4 (UUID)

  * null

  
  
← Define Path for S3 DataOptimize Query Performance →

