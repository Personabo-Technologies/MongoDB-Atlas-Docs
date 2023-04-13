Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Unsupported Commands in Atlas

Share Feedback

On this page

  * Unsupported Commands in `M0/M2/M5` Clusters
  * Limited Commands
  * Unsupported Commands
  * Unsupported Command Line Options
  * Unsupported Commands in `M10+` Clusters
  * Limited Commands
  * Unsupported Commands
  * Unsupported Command Line Options
  * MongoDB 4.2+ Incompatibility
  * Contact Support
  * Unsupported Commands in Serverless Instances
  * Unsupported Command Line Options

## Unsupported Commands in `M0/M2/M5` Clusters

Atlas `M0` free clusters and `M2`/`M5` shared clusters don't support all
functionality available to other clusters.

## Important

`M0` free clusters and `M2`/`M5` shared clusters don't support read or write
operations on the `admin` database.

To learn more about `M0`/`M2`/`M5` limitations, see Atlas M0 (Free Cluster),
M2, and M5 Limitations.

## Note

If you use an unsupported command or invalid syntax, Atlas returns the
following error message:

    
    
     <$command> is not allowed or the syntax is incorrect,  
      
     see the Atlas documentation for more information.  
  
To learn more about valid syntax, see Database Commands

### Limited Commands

You can run the following commands with limitations in `M0` free clusters and
`M2`/`M5` shared clusters:

Command

|

Limitation  
  
|  
  
`aggregate`

|

  * Limits the `maxTimeMs` parameter to 300 seconds (`300000`).

  * Ignores the `allowDiskUsage` parameter.

  * Doesn't support $accumulator and $function operators.

  
  
`count`

|

  * Doesn't support the `$where` operator.

  * Limits the `count` operation on the `local` database to the `system.replset` and `oplog.rs` collections.

  
  
`dbStats`

|

`M0` free clusters and `M2/M5` shared clusters don't allow the `dbStats`
command on the `local` and `config` databases.

To learn more, see Operational Limitations.  
  
`distinct`

|

Doesn't support `$where` operator.  
  
`find`

|

  * Doesn't support the `$where` operator.

  * Limits the `find` operation on the `local` database to the `oplog.rs` collection.

  * Limits the `find` operation to using an equality condition when querying the `ns` field in the `oplog.rs` collection on the `local` database.
    
        | { "ns" : "test.foo" }  
      
  

  
  
`getParameter`

|

Limits execution to these two documents:

  * `{ "getParameter": 1, "authSchemaVersion": 1 }`

  * `{ "getParameter": 1, "authenticationMechanisms": 1 }`

  
  
`db.killOp()`

|

Limits the `db.killOp()` method to to the MongoDB user who ran the operation.  
  
`serverStatus`

|

Limits response to the following fields:

|

  * `$clusterTime.clusterTime`

  * `$clusterTime.operationTime`

  * `$clusterTime.signature.hash`

  * `$clusterTime.signature.keyId`

  * `$clusterTime.signature`

  * `asserts.msg`

  * `asserts.regular`

  * `asserts.rollovers`

  * `asserts.user`

  * `asserts.warning`

  * `atlasVersion.gitVersion`

  * `atlasVersion.version`

  * `connections.available`

  * `connections.current`

  * `connections.totalCreated`

  * `extra_info.note`

  * `extra_info.page_faults`

  * `host`

  * `localTime`

  * `mem.bits`

  * `mem.mapped`

  * `mem.mappedWithJournal`

  * `mem.resident`

  * `mem.supported`

  * `mem.virtual`

  * `metrics.atlas.bytesInWrites`

  * `metrics.atlas.connectionPool.totalCreated`

  * `network.bytesIn`

  * `network.bytesOut`

  * `network.numRequests`

  * `ok`

  * `opcounters.command`

  * `opcounters.delete`

  * `opcounters.getmore`

  * `opcounters.insert`

  * `opcounters.query`

  * `opcounters.update`

  * `opcountersRepl.command`

  * `opcountersRepl.delete`

|

  * `opcountersRepl.getmore`

  * `opcountersRepl.insert`

  * `opcountersRepl.query`

  * `opcountersRepl.update`

  * `pid`

  * `process`

  * `repl.electionId`

  * `repl.hosts[]`

  * `repl.ismaster`

  * `repl.lastWrite.lastWriteDate`

  * `repl.lastWrite.majorityOpTime.t`

  * `repl.lastWrite.majorityOpTime.ts`

  * `repl.lastWrite.majorityWriteDate`

  * `repl.lastWrite.opTime.t`

  * `repl.lastWrite.opTime.ts`

  * `repl.me`

  * `repl.primary`

  * `repl.rbid`

  * `repl.secondary`

  * `repl.setName`

  * `repl.setVersion`

  * `repl.tags.nodeType`

  * `repl.tags.provider`

  * `repl.tags.region`

  * `repl.tags`

  * `storageEngine.backupCursorOpen`

  * `storageEngine.dropPendingIdents`

  * `storageEngine.name`

  * `storageEngine.oldestRequiredTimestampForCrashRecovery`

  * `storageEngine.persistent`

  * `storageEngine.readOnly`

  * `storageEngine.supportsCommittedReads`

  * `storageEngine.supportsPendingDrops`

  * `storageEngine.supportsSnapshotReadConcern`

  * `uptime`

  * `uptimeEstimate`

  * `uptimeMillis`

  * `version`

  
|  
  
`usersInfo`

|

Limits to the following document:

    
    
    | { "user": "<MYUSER>", "db": "admin" }  
      
  
### Unsupported Commands

`M0` free clusters and `M2`/`M5` shared clusters don't support the following
commands:

## Note

The commands available for clusters of all other tiers, `M10` and larger,
correspond to the privileges defined for the built-in Atlas MongoDB roles. To
learn more about permissions, see Atlas User Privileges.

  * `_migrateClone`

  * `_recvChunkAbort`

  * `_recvChunkCommit`

  * `_recvChunkStart`

  * `_recvChunkStatus`

  * `_transferMods`

  * `appendOplogNote`

  * `applyOps`

  * `authenticate`

  * `authSchemaUpgrade`

  * `checkShardingIndex`

  * `cleanupOrphaned`

  * `cloneCollection`

  * `cloneCollectionAsCapped`

  * `compact`

  * `copydbgetnonce`

  * `copydbsaslstart`

  * `createRole`

  * `createUser`

  * `$currentOp` aggregation pipeline stage

  * `currentOpCtx`

  * `dataSize`

  * `dbHash`

  * `dropAllRolesFromDatabase`

  * `dropAllUsersFromDatabase`

  * `dropRole`

  * `enableFreeMonitoring`

  * `forcerror`

  * `fsync`

  * `fsyncUnlock`

|

  * `getDiagnosticData`

  * `getPrevError`

  * `getShardMap`

  * `getShardVersion`

  * `grantPrivilegesToRole`

  * `grantRolesToRole`

  * `grantRolesToUser`

  * `handshake`

  * `hostInfo`

  * `invalidateUserCache`

  * `killAllSessions`

  * `killAllSessionsByPattern`

  * `killSessions`

  * `$listLocalSessions`

  * `$listSessions`

  * `lockInfo`

  * `logRotate`

  * `shardedFinish`

  * `mapReduce`

  * `planCacheClear`

  * `planCacheClearFilters`

  * `planCacheListFilters`

  * `planCacheListPlans`

  * `planCacheListQueryShapes`

  * `$planCacheStats` aggregation pipeline stage

  * `planCacheSetFilter`

  * `reIndex`

  * `repairCursor`

  * `repairDatabase`

|

  * `replSetDeclareElectionWinner`

  * `replSetElect`

  * `replSetFreeze`

  * `replSetFresh`

  * `replSetGetConfig`

  * `replSetGetRBID`

  * `replSetGetStatus`

  * `replSetHeartbeat`

  * `replSetInitiate`

  * `replSetMaintenance`

  * `replSetReconfig`

  * `replSetRequestVotes`

  * `replSetStepDown`

  * `replSetStepUp`

  * `replSetSyncFrom`

  * `replSetUpdatePosition`

  * `resetError`

  * `resync`

  * `revokePrivilegesFromRole`

  * `revokeRolesFromRole`

  * `revokeRolesFromUser`

  * `setFeatureCompatibilityVersion`

  * `setLogLevel`

  * `setParameter`

  * `setProfilingLevel`

  * `shutdown`

  * `updateRole`

  * `updateUser`

  * `validate`

  
||  
  
### Unsupported Command Line Options

`M0` free clusters and `M2/M5` shared clusters don't support the following
command line tool options:

Command Line Tool

|

Unsupported Options  
  
|  
  
`mongorestore`

|

  * \--restoreDbUsersAndRoles

  * \--oplogReplay

  * \--preserveUUID

  
  
`mongodump`

|

  * \--dumpDbUsersAndRoles

  * \--oplog

  
  
For more information, see Atlas M0 (Free Cluster), M2, and M5 Limitations.

## Unsupported Commands in `M10+` Clusters

Atlas requires clients to authenticate to access an Atlas cluster. Atlas
provides a curated list of Database User Privileges. These privileges provide
access to a subset of MongoDB commands.

### Limited Commands

Atlas limits the `db.killOp()` method to the MongoDB user who ran the
operation.

### Unsupported Commands

The following table lists the most common commands and shell methods that
database user privileges do not support. To ensure cluster stability and
performance, Atlas subsumes or restricts the functionality that these commands
provide.

#### Administrative

Commands

|

Shell Method

|

Privilege Actions  
  
||  
  
`setParameter`

|

`db.setLogLevel()`

Others that use `setParameter`.

|

`setParameter`  
  
`logRotate`

|

|

`logRotate`  
  
`shutdown`

|

`db.shutdownServer()`

|

`shutdown`  
  
`eval`

|

`db.eval()`

|  
  
`fsync`

|

`db.fsyncLock()`

|

`fsync`  
  
`setFeatureCompatibilityVersion`

|

|  
  
#### Sessions

Commands

|

Shell Method

|

Privilege Actions  
  
||  
  
`killAllSessions`

|

|

`killAnySession`  
  
#### Replication

Commands

|

Shell Method

|

Privilege Actions  
  
||  
  
`replSetFreeze`

|

`rs.freeze()`

|

`replSetStateChange`  
  
`replSetInitiate`

|

`rs.initiate()`

|  
  
`replSetMaintenance`

|

|

`replSetStateChange`  
  
`replSetReconfig`

|

`rs.reconfig()`

|  
  
`replSetResizeOplog`

|

|  
  
`replSetStepDown`

|

`rs.stepDown()`

|

`replSetStateChange`  
  
`replSetSyncFrom`

|

`rs.syncFrom()`

|

`replSetStateChange`  
  
`resync`

|

|

`resync`  
  
### Unsupported Command Line Options

`M10+` clusters don't support the \--preserveUUID option for `mongorestore`.

#### Sharding

Commands

|

Shell Method

|

Privilege Actions  
  
||  
  
|

`sh.disableBalancing()`

|  
  
|

`sh.enableBalancing()`

|  
  
`removeShard`

|

|

`removeShard`  
  
`refineCollectionShardKey` [1]

|

|

`refineCollectionShardKey`  
  
[1]|  This command is not supported on global write clusters only.  
|  
  
#### User and Role Management

## Note

As an alternative, see the available Atlas User Roles.

Commands

|

Shell Method

|

Privilege Actions  
  
||  
  
`createUser`

|

`db.createUser()`

|

`createUser`  
  
`getUser` [2]

|

`db.getUser()` and `db.getUsers()` [2]

|  
  
`dropUser`

|

`db.dropUser()`

|

`dropUser`  
  
`grantRolesToUser`

|

`db.grantRolesToUser()`

|

`grantRole`  
  
`revokeRolesFromUser`

|

`db.revokeRolesFromUser()`

|

`revokeRole`  
  
`updateUser`

|

`db.updateUser()`

|  
  
`createRole`

|

`db.createRole()`

|

`createRole`  
  
`dropRole`

|

`db.dropRole()`

|

`dropRole`  
  
`updateRole`

|

`db.updateRole()`

|  
  
[2]|  _(1, 2)_ You can call `getUser` for your own user account.  
|  
  
### MongoDB 4.2+ Incompatibility

MongoDB versions 4.2 and later don't support the following commands and
methods:

Commands

|

Shell Method  
  
|  
  
`parallelCollectionScan`

|  
  
`clone`

|

`db.cloneDatabase()`  
  
`copydb`

|

`db.copyDatabase()`  
  
### Contact Support

Contact Atlas support if your use case requires access to a command that the
Atlas database user privileges don't currently support.

## Unsupported Commands in Serverless Instances

Atlas serverless instances don't support the following database commands and
`mongosh` shell methods:

Database Command

|

Shell Method  
  
|  
  
`addShard`

|

`sh.addShard()`  
  
`addShardToZone`

|

`sh.addShardToZone()`  
  
`applyOps`

|  
  
`balancerCollectionStatus`

|

`sh.balancerCollectionStatus()`  
  
`balancerStart`

|

`sh.startBalancer()`  
  
`balancerStatus`

|  
  
`balancerStop`

|

`sh.stopBalancer()`  
  
`clearJumboFlag`

|  
  
`$currentOp` aggregation pipeline stage

|  
  
`dbHash`

|  
  
`enableSharding`

|

`sh.enableSharding()`  
  
`flushRouterConfig`

|  
  
`geoNear`

(deprecated in MongoDB v4.0)

|  
  
`geoSearch`

|  
  
`getShardMap`

|  
  
`getShardVersion`

|  
  
`listShards`

|  
  
`$listLocalSessions` aggregation pipeline stage

|  
  
`$listSessions` aggregation pipeline stage

|  
  
`mergeChunks`

|  
  
`moveChunk`

|

`sh.moveChunk()`  
  
`movePrimary`

|  
  
`$planCacheStats` aggregation pipeline stage

|  
  
`refineCollectionShardKey`

|  
  
`removeShard`

|  
  
`removeShardFromZone`

|

`sh.removeShardFromZone()`  
  
`profile`

|

`db.setProfilingLevel()`  
  
`shardCollection`

|

`sh.shardCollection()`  
  
`shardConnPoolStats`

(deprecated in MongoDB v4.4)

|  
  
`split`

|

`sh.splitAt()`

`sh.splitFind()`  
  
`top`

|  
  
`updateZoneKeyRange`

|

`sh.updateZoneKeyRange()`  
  
`validate`

|

`db.collection.validate()`  
  
### Unsupported Command Line Options

Serverless instances don't support the following command line tool options:

Command Line Tool

|

Unsupported Options  
  
|  
  
`mongorestore`

|

  * \--oplogReplay

  * \--preserveUUID

  
  
← Atlas M0 (Free Cluster), M2, and M5 LimitationsCommands Available Only in
Free Clusters →

