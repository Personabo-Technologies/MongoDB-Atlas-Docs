Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Administration Commands

Share Feedback

On this page

  * `hello`
  * `killCursors`
  * `listCollections`
  * `listDatabases`

## `hello`

Atlas Data Federation supports the hello command, which is used to describe
the role of the `mongod` instance. In the document returned by the `hello`
command, the `isWritablePrimary` field is set to `true`.

Atlas Data Federation supports the optional `saslSupportedMechs` field set to
the `<db.user>`.

## `killCursors`

The killCursors command kills the specified cursor or cursors for a
collection.

## `listCollections`

The listCollections command retrieves information about the collections in a
database, such as collection names and options. The response contains
information that can be used to create a cursor to the collection information.
Results are ordered alphabetically by collection name.

Atlas Data Federation supports the following options:

  * `filter` (Exact match only.)

  * `nameOnly`

  * `authorizedCollections`

## `listDatabases`

The listDatabases command provides a list of all existing databases in
alphabetical order. You must use the `admin` database to run the
`listDatabases` command.

The following options are supported:

  * `filter` (Exact match only.)

  * `nameOnly`

  * `authorizedDatabases`

The `listDatabases` command always returns `sizeOnDisk: 0` and `empty: false`
so it can return quickly, without scanning all the files in the S3 buckets.

← Supported MongoDB CommandsDiagnostic Commands →

