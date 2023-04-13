Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Custom Role Actions

Share Feedback

On this page

  * Query and Write Actions
  * Database Management Actions
  * Change Stream Actions
  * Server Administration Actions
  * Session Actions
  * Global Actions
  * Deployment Management Actions
  * Sharding Actions
  * Atlas Data Federation Actions

This document lists the possible privilege actions you can assign to custom
roles via the Atlas Administration API. Specify one of these actions in the
`actions.action` request body parameter when you create or update a custom
role.

## Note

The privilege actions available for custom roles and the custom roles API
represent a subset of the privilege actions available for built-in roles.

To review the list of custom role privileges, see the API reference.

## Query and Write Actions

  * `FIND`

  * `INSERT`

  * `REMOVE`

  * `UPDATE`

  * `BYPASS_DOCUMENT_VALIDATION`

  * `USE_UUID`

## Database Management Actions

  * `CREATE_COLLECTION`

  * `CREATE_INDEX`

  * `DROP_COLLECTION`

  * `ENABLE_PROFILER`

## Change Stream Actions

  * `CHANGE_STREAM`

## Server Administration Actions

  * `COLL_MOD`

  * `COMPACT`

  * `CONVERT_TO_CAPPED`

  * `DROP_DATABASE`

  * `DROP_INDEX`

  * `RE_INDEX`

  * `RENAME_COLLECTION_SAME_DB`

  * `SET_USER_WRITE_BLOCK`

  * `BYPASS_USER_WRITE_BLOCK`

## Session Actions

  * `LIST_SESSIONS`

  * `KILL_ANY_SESSION`

## Global Actions

### Diagnostic Actions

  * `COLL_STATS`

  * `CONN_POOL_STATS`

  * `DB_HASH`

  * `DB_STATS`

  * `GET_CMD_LINE_OPTS`

  * `GET_LOG`

  * `GET_PARAMETER`

  * `GET_SHARD_MAP`

  * `HOST_INFO`

  * `IN_PROG`

  * `LIST_DATABASES`

  * `LIST_COLLECTIONS`

  * `LIST_SHARDS`

  * `LIST_INDEXES`

  * `NETSTAT`

  * `REPLSET_GET_CONFIG`, see Replication Actions

  * `REPLSET_GET_STATUS`, see Replication Actions

  * `SERVER_STATUS`

  * `SHARDING_STATE`

  * `VALIDATE`

  * `TOP`

## Deployment Management Actions

  * `KILL_OP`

## Sharding Actions

  * `ADD_SHARD_TO_ZONE`

  * `REMOVE_SHARD_FROM_ZONE`

  * `UPDATE_ZONE_KEY_RANGE`

  * `FLUSH_ROUTER_CONFIG`

To learn more, see Sharding Actions

## Atlas Data Federation Actions

  * `SQL_GET_SCHEMA`

  * `SQL_SET_SCHEMA`

  * `VIEW_ALL_HISTORY`

  * `OUT_TO_S3`

  * `STORAGE_GET_CONFIG`

  * `STORAGE_SET_CONFIG`

← Return the Latest Targets for PrometheusRead and Write with the Data API →

