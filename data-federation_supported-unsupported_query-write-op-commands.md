Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Query and Write Operation Commands

Share Feedback

On this page

  * `aggregate`
  * `count`
  * `find`

## Note

Atlas Data Federation doesn't include a server-side JavaScript engine. So, it
doesn't support commands like mapReduce that require server-side scripting
enabled.

## `aggregate`

For the aggregate command, the following limitation applies:

  * Atlas Data Federation supports the `explain`, `cursor`, `comment`, and `background` options only.

  * For the `comment` option, Atlas Data Federation supports only type `string`.

  * Atlas Data Federation supports `{"background" : <boolean>}` option for `$out` to S3 and Atlas cluster only. The `background` option is not available for other aggregation pipeline stages. See $out Options for more information.

## Tip

### See also:

Supported Aggregation Pipeline Stages and Operators.

## `count`

For the count command, the following limitations apply:

  * Atlas Data Federation converts `count()` to an aggregation pipeline internal to Data Federation.

  * Atlas Data Federation supports only the `query` option.

## `find`

For find command, Atlas Data Federation supports the following options:

  * `batchSize`

  * `singleBatch`

  * `filter`

  * `limit`

  * `projection`

  * `skip`

  * `sort`

`find()` is converted to an aggregation pipeline internal to the federated
database instance.

← Diagnostic CommandsRole Management Commands →

