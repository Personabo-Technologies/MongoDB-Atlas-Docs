Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Diagnostic Commands

Share Feedback

On this page

  * `buildInfo`
  * `collStats`
  * `connectionStatus`
  * `dbStats`
  * `explain`
  * `getLog`
  * `getMore`
  * `hostInfo`
  * `ping`
  * `whatsmyuri`

## `buildInfo`

For the buildInfo command, the response contains the following fields:

Field

|

Description  
  
|  
  
`ok`

|

Returns `1` for success or `0` for failure.  
  
`version`

|

The MongoDB client compatibility version. This is the earliest version of the
MongoDB client with which the Data Federation service is compatible.  
  
`versionArray`

|

The MongoDB client compatibility version in array format.  
  
`dataLake.version`

|

The version number of Data Federation.  
  
`dataLake.gitVersion`

|

The git version of the Data Federation service.  
  
`dataLake.date`

|

The build timestamp of the Data Federation service.  
  
## Example

    
    
    {  
      
      "ok" : <return>,  
      "version" : "<version-number>",  
      "versionArray" : [  
        <number>,  
        <number>,  
        <number>,  
        <number>  
      ],  
      "dataLake" : {  
        "version" : "<version-number>",  
        "gitVersion" : "<version-number>",  
        "date" : "<timestamp>"  
      }  
    }  
  
## `collStats`

For the collStats command, Atlas Data Federation omits the following fields in
the response:

  * `avgObjSize`

  * `capped`

  * `max`

  * `maxSize`

  * `wiredTiger`

  * `nindexes`

  * `totalIndexSize`

  * `indexSizes`

Atlas Data Federation includes the following fields in the response. You can
use these fields to verify what partitions are used to populate a collection,
understand how recently the stats were computed, and determine if Atlas Data
Federation truncated the output document.

Field

|

Description  
  
|  
  
`partitions.format`

|

The file format of the partition.  
  
`partitions.attributes`

|

The filtering attributes of the partition.  
  
`partitions.count`

|

The number of documents in the partition.  
  
`partitions.source`

|

The S3 URL or Atlas cluster name, which contains the backing data of the
partition.  
  
`partitions.size`

|

The size, in bytes, of the partition.  
  
`partitionCount`

|

The number of partitions.  
  
`avgPartitionSize`

|

The average size of all partitions.  
  
`cacheMetadata`

|

Contains information on how recently the stats were computed.  
  
`cacheMetadata.computeTime`

|

The time in ISODate format when the computation for the stats started.  
  
`cacheMetadata.automaticRefreshInProgress`

|

The flag that indicates if a background job is running now to refresh the
cache.  
  
`truncated`

|

The flag that indicates whether Atlas Data Federation enforced the maximum
document size limit of 16MiB. The flag value can be one of the following:

  * `true` \- if the output document size exceeded the limit and was therefore truncated to include only enough partitions that allowed the document to comply with the size limit. If `true`, the `partitionCount` and `avgPartitionSize` values that Atlas Data Federation returns may be smaller than the actual values.

  * `false` \- if Atlas Data Federation returns the entire document.

  
  
## Example

    
    
    {  
      
      ...  
      "partitionCount": <number of partitions>,  
      "avgPartitionSize": <average size of all partitions>,  
      "partitions": [  
        {  
            "format": <file format>,  
            "attributes": <filtering attributes>,  
            "count": <number of documents in partition>,  
            "source": <S3 url or Atlas cluster name>,  
            "size": <size, in bytes, of the partition>  
          },  
        ...  
      ],  
      "truncated": false,  
      "cacheMetadata": {  
        computeTime: ISODate("2021-07-25T15:10:33.513Z"),  
        automaticRefreshInProgress: false  
      },  
      ...  
    }  
  
Atlas Data Federation introduces an optional boolean parameter, `sync`, to
bypass the cache and fetch the most recent storage statistics for a given
collection. The following values are valid for the `sync` parameter:

  * `true` \- to bypass the cache and return the most recent storage statistics

  * `false` \- to return cached data

If the `sync` parameter is omitted, defaults to `false`.

## Example

    
    
    db.runCommand( {collStats: "<string>", sync: true|false} )  
      
  
To learn more about the parameters supported by this command, see collStats.

## `connectionStatus`

For connectionStatus command, Atlas Data Federation returns information about
the current connection, specifically the state of authenticated users and
their available roles.

## Note

Only one user can authenticate on a connection to a federated database
instance at any given time. If a user authenticates and then runs the
`db.auth()` command, Data Federation replaces the previous user's permissions
with the new user's permissions.

The connectionStatus command shows only the newly authenticated user in the
`authenticatedUsers` output field.

## `dbStats`

For dbStats command, Atlas Data Federation introduces an optional boolean
parameter, `sync`, to bypass the cache and fetch the most recent storage
statistics for a given database. The following values are valid for the `sync`
parameter:

  * `true` \- to bypass the cache and return the most recent storage statistics

  * `false` \- to use the cached data also

If the `sync` parameter is omitted, defaults to `false`.

## Example

    
    
    db.runCommand( {dbStats: 1, sync: true|false} )  
      
  
To learn more about the parameters supported by this command, see dbStats.

Atlas Data Federation command omits the followig fields in the response:

  * `object`

  * `avgObjSize`

  * `fsUsedSize`

  * `fsTotalSize`

The commands adds the following fields in the response. You can use these
fields to determine whether the command returned stale data.

Field

|

Description  
  
|  
  
`cacheMetadata`

|

Contains information on how recently the stats were computed.  
  
`cacheMetadata.computeTime`

|

The time in ISODate format when the computation for the stats started.  
  
`cacheMetadata.automaticRefreshInProgress`

|

The flag that indicates if a background job is running now to refresh the
cache.  
  
## `explain`

For explain command, the data returned by `explain` documents the Data
Federation query plan. The `explain` output differs from MongoDB in that it
provides information about the data partitions used to satisfy the query.

The following commands can be explained in Data Federation:

  * `aggregate()`

  * `count()`

  * `find()`

Atlas Data Federation supports the following `verbosity` modes:

  * `queryPlanner` \- provides information on the query plan.

  * `queryPlannerExtended` \- provides detailed information on the query plan including information about the S3 objects, such as the S3 object names and sizes, that will be queried.

Atlas Data Federation doesn't support `executionStats` and `allPlansExecution`
modes.

## Example

The following example shows how to use the `explain` command to get
information about the aggregate command, including detailed information on the
query plan.

    
    
    db.runCommand({ "explain": { "aggregate": "user", "verbosity": "queryPlannerExtended", "pipeline": [ ], "cursor": {} }})  
      
  
When you run `explain`, Atlas Data Federation returns the following fields:

Output Field Name

|

Description  
  
|  
  
`stats`

|

Document that describes the number and total size of partitions that Atlas
Data Federation might open for the query.  
  
`stats.size`

|

Total size of partitions that Atlas Data Federation might open for the query.  
  
`stats.numberOfPartitions`

|

Number of partitions that Atlas Data Federation might open for the query.  
  
`plan`

|

Document that contains the query execution plan for the query. The document
contains nested execution plan nodes, each of which is a document describing
the plan node. The nested plan node documents contain internal description of
Atlas Data Federation's query execution, and include various node kinds that
are subject to change. Contact MongoDB support if you need more help with
understanding the query plan.  
  
Basic Example

find Example

    
    
    db.runCommand({ "explain": { "aggregate": "user", "verbosity": "queryPlanner", "pipeline": [ ], "cursor": {} }})  
      
  
HIDE OUTPUT

    
    
    1| {  
    |  
    2|   ok: 1,  
    3|   stats: { size: '42.06258487701416 MiB', numberOfPartitions: 1 },  
    4|   plan: {  
    5|     kind: 'region',  
    6|     region: 'AWS/us-east-1',  
    7|     node: {  
    8|       kind: 'data',  
    9|       size: '42.06258487701416 MiB',  
    10|       numberOfPartitions: 1,  
    11|       partitions: [ { source: 'sbx', provider: 'atlas', size: '42.06258487701416 MiB' } ]  
    12|     }  
    13|   }  
    14| }  
  
## `getLog`

For getLog command, Atlas Data Federation returns a successful response, but
doesn't includes log data.

## `getMore`

For getMore command, Atlas Data Federation returns subsequent batches of
documents currently pointed to by a cursor, when used in conjunction with
commands that return a cursor, e.g. find and aggregate.

## `hostInfo`

For hostInfo command, Atlas Data Federation returns only the following subset
of fields from the standard MongoDB response:

    
    
    {  
      
      "ok" : <return>,  
      "system" : {  
        "currentTime" : ISODate("<timestamp>"),  
        "hostname" : "<hostname>",  
        "cpuAddrSize" : <number>,  
        "memSizeMB" : <number>,  
        "numCores" : <number>,  
        "cpuArch" : "<identifier>",  
      },  
      "os" : {  
        "type" : "<string>",  
        "name" : "<string>",  
      },  
      "extra" : { }  
    }  
  
## `ping`

For ping command, Atlas Data Federation tests whether a server is responding
to commands.

## `whatsmyuri`

For whatsmyuri command, Atlas Data Federation returns the client IP address.

← Administration CommandsQuery and Write Operation Commands →

