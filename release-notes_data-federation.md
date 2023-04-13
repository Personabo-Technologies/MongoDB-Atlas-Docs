Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Data Federation Changelog

Share Feedback

On this page

  * 2023 Releases
  * 2022 Releases
  * 2021 Releases
  * 2020 Releases
  * 2019 Releases

## 2023 Releases

## Note

### Release notes mention only releases with feature changes

MongoDB releases Atlas Data Federation every week, continuously improving
Atlas Data Federation performance and stability. These release notes capture
only those releases that contain feature changes. If a particular Atlas Data
Federation release contains only performance and stability improvements, it is
not included in these release notes. To identify which release version you are
using, check the release version string for the release date.

### 04 April 2023 Release

  * Improves error messages when querying a document over 16MB.

  * Fixes a correctness issue for $getFields where Atlas Data Federation differed from MongoDB when querying an empty sub-document.

  * Improves stability and performance for $out to S3 when writing to Parquet.

### 21 February 2023 Release

  * Fixes an issue with `$match` queries that resulted in documents not being returned when querying on nested documents within an array where any nested document was missing the target field.

  * Improves performance and stability when writing to Parquet using `$out` to S3.

  * Adds the ability to use any BSON type with the `$comment` operator and query in $queryHistory.

  * Atlas Data Federation now returns MongoDB 6.2.0 in the buildInfo output.

### 15 February 2023 Release

  * Adds the ability to limit the amount of data that Atlas Data Federation processes for your federated database instances to control costs.

### 07 February 2023 Release

  * Improves error messages when a client attempts to insert, update, or delete a document in a federated database instance.

### 24 January 2023 Release

  * Adds the application name to connections that Atlas Data Federation creates to your Atlas clusters.

  * Adds the ability to set and update the storage configuration using the Atlas Data Federation API.

### 11 January 2023 Release

  * Fixes an issue that caused `maxTimeMS` with a `batchSize` of `0` to fail.

## 2022 Releases

### 19 December 2022 Release

  * Adds new capabilities to the storage configuration to support data provenance and improved flexibility for federation.

  * Adds AWS region `ap-southeast-1` (Singapore).

### 30 November 2022 Release

  * Updates Atlas Data Federation to MongoDB 6.0.2.

### 15 November 2022 Release

  * Supports killOp for collStats.

### 25 October 2022 Release

  * Improves performance and stability.

  * Improves query performance on Atlas Data Lake Datasets using sort metadata to optimize queries.

  * Fixes an issue that caused Atlas Data Federation to fail to read a Parquet file when the top-level or root schema was marked as `REPEATED` or `OPTIONAL`.

  * Improves stability when writing to Parquet using `$out` to S3.

### 13 September 2022 Release

  * Fixes `$not` and `$in` pipeline issue that caused unsupported expression panic.

  * Improves performance for `$out` to S3 queries that write to Parquet file format.

  * Updates the default max row group size to 128MB for the parquet writer.

  * Improves `$group` stages on Data Lake Dataset partition fields.

  * Fixes aggregation pipelines with multiple `$lookup` stages where one stage defines a field and another removes the same field.

  * Fixes how Atlas Data Federation handles files in S3 that end with the delimiter character (e.g. '/').

### 23 August 2022 Release

  * Improves performance and stability.

  * Adds support for optionally specifying an ISODate format to optimize performance for date-type partitions.

### 02 August 2022 Release

  * Improves performance and stability.

  * Performs $merge in chunks.

### 12 July 2022 Release

  * Improves performance and stability.

  * Atlas now charges for the total number of bytes that Atlas Data Federation processes from HTTP sources.

  * Adds support for the background option on the $merge aggregation stage.

### 21 June 2022 Release

  * Improves performance and stability.

  * Adds support for Atlas Data Lake as a "Store Type" to the `createStore` command.

  * Improves error messaging for Federated `$search` queries.

### 07 June 2022 Release

  * Renames and relaunches Atlas Data Lake as Atlas Data Federation.

## Important

The federated query engine service previously called Atlas Data Lake is now
called Atlas Data Federation. To learn more about Atlas Data Federation, see
Set Up and Query Data Federation.

### 31 May 2022 Release

  * Improves performance and stability.

  * Disables support for the MySQL dialect.

### 10 May 2022 Release

  * Improves performance and stability.

### 19 April 2022 Release

  * Improves performance and stability.

  * Supports the following new MongoDB 5.2 aggregation operators:

    * `$sortArray`

    * `$topN`

    * `$bottomN`

    * `$maxN`

    * `$firstN`

    * `$lastN`

  * Fixes a bug to allow you to use read preference for sharded clusters.

### 29 March 2022 Release

  * Improves performance and stability.

### 15 March 2022 Release

  * Improves performance and stability.

  * Imposes an upper limit on `maxRowGroupSize`.

### 15 February 2022 Release

  * Improves performance and stability.

  * Renames the `matchComments` field to `queryFilterComments` . To learn more, see Retrieve Federated Database Instance Query History.

### 18 January 2022 Release

  * Improves performance and stability.

  * Adds `matchComments` field to query history. To learn more, see Retrieve Data Lake Query History.

## 2021 Releases

### 28 December 2021 Release

  * Improves performance and stability.

  * Supports queries on collections prefixed with `system`, but doesn't support queries on collections prefixed with `system.`.

### 07 December 2021 Release

  * Improves performance and stability.

  * Adds support for the $maxTimeMS option.

### 16 November 2021 Release

  * Improves performance and stability.

  * Allows connections to Data Lakes via private endpoints.

  * Adds support for X.509 authorization.

  * Adds support for empty `field` parameters with the $setField aggregation expression.

  * Fixes an issue where commands returned zero exit codes on failure.

  * Fixes an issue where documents with empty subdocuments written to Parquet contained empty parquet groups.

  * Updates `EstimateRowGroupSize` to report `UncompressedSize` for documents stored in Parquet.

  * Adjusts the minimum value for `maxRowGroupSize` when using `$out` to Parquet to 16MB.

  * Removes support for using `$out` to write documents that contain duplicate fields to Parquet.

  * Improves error messages for `$out`.

### 27 October 2021 Release

  * Improves performance and stability.

  * Includes X.509 users in the usersInfo command output.

  * Improves SCRAM authentication performance.

### 05 October 2021 Release

  * Improves performance and stability.

  * Adds support for the `authenticate` command.

  * Preserves binary subtypes in the parquet reader/writer.

### 14 September 2021 Release

  * Provides various stability and performance improvements.

  * Adds support for `ap-south-1` region.

  * Outputs customer query logs into multiple lines.

  * Includes `background` field in $queryHistory output.

  * Supports wildcard databases and collections for Atlas data store.

### 25 August 2021 Release

  * Provides various stability improvements.

  * Improves `collStats` and `dbStats` command performance and stability.

  * Adds support for the `$merge` aggregation pipeline stage.

  * Allows `localField` and `foreignField` with a more expressive $lookup aggregation pipeline stage syntax.

  * Implements the `$count` accumulator.

### 03 August 2021 Release

  * Improves performance.

  * Improves error messaging.

  * Adds `computeTime` and `automaticRefreshInProgress` fields to the `collStats` and `dbStats` command outputs.

### 12 July 2021 Release

  * Supports dropping non-existent stores and databases from the storage configuration.

  * Includes `partitions.count` in collStats command output.

### 23 June 2021 Release

  * Allows downloading Data Federation query logs from the UI and API.

  * Removes restriction on large collection namespaces.

  * Adds option to bypass cache for collStats and dbStats to fetch the most recent statistics.

  * Supports serverStatus command.

### 8 June 2021 Release

  * Improves stability and performance.

  * Supports public S3 data stores with the `public` configuration flag.

  * Supports Zstandard compression when federating queries to Atlas clusters.

  * Adds `db` field to `dbStats` result.

### 11 May 2021 Release

  * Supports selecting read preference, read tags, and max staleness through the storage configuration for Atlas Cluster stores.

  * Rejects commands sent with a Versioned API set.

  * Enables the `count` parameter in the Data Lake `$collStats` aggregation stage.

  * No longer permits `$collStats` in `$facet` sub-pipelines.

  * Enforces maximum document size for `$facet` after processing each item.

  * Improves performance for `$match` stages.

  * Improves error messaging.

### 21 April 2021 Release

  * Improves stability and performance.

  * Includes improved support for Parquet.

  * Supports `M0`, `M2`, & `M5` Atlas clusters as data sources.

  * Adds regex pattern matching option for wildcard collections from Atlas Clusters.

  * Includes updated error messages for query execution limit.

### 30 March 2021 Release

  * Generates storage configuration automatically for the first time after user authentication.

  * Returns connection ID through the `hello` command.

  * Supports `$geoNear` on Atlas Data Lake collections that span multiple Atlas clusters.

  * Includes various performance improvements.

  * Includes improved error messages for terminated queries.

### 09 March 2021 Release

  * Includes new onboarding and storage configuration interface.

  * Improved SQL schema error message.

  * Support query pushdown to collections comprised of multiple Atlas collections.

  * Improves stability and performance.

### 16 February 2021 Release

  * Adds SQL schema generation for wildcard collections.

  * Fixes stability and performance issues.

### 26 January 2021 Release

  * Adds a new `$sql` `formatVersion` to reduce the data size of the result set.

  * Improves performance of `$lookup`.

  * Adds `"verbosity": "queryPlannerExtended"` support to the explain command to filter out non-matching partitions.

  * Adds support for $$NOW.

  * Reports Atlas Data Lake as MongoDB version 4.4 to tools.

### 5 January 2021 Release

  * Adds support for the background option on the $out to Atlas aggregation stage.

  * Includes stability and performance improvements.

## 2020 Releases

### 16 December 2020 Release

  * Adds `{background: true}` option, which allows queries to run in the background for `$out` to S3 stage.

  * Introduces `$queryHistory` aggregation stage to view past queries.

  * Includes various performance and stability improvements.

### 24 November 2020 Release

  * Supports Parquet, CSV, and TSV formats for `$out` to S3.

  * Adds a rolling limit for cursors.

  * Improves error messages for commands that cannot be parsed.

### 03 November 2020 Release

  * Supports the `$geoNear` and `$graphLookup` aggregation pipeline stages in queries on federated database instance collections that reference a single Atlas collection.

  * Updates summary information in explain output.

### 13 October 2020 Release

  * Supports `defaultFormat` for files in publicly accessible URLs in HTTP stores.

  * Limits the number of simultaneous queries to 30 per federated database instance.

  * Supports `bzip2` compression format.

  * Supports `comment` option for the aggregate command.

  * Includes various performance and stability improvements.

### 22 September 2020 Release

  * Supports killOp command for terminating a long-running query.

  * Adds `configuration` for maximum number of wildcard collections for S3 federated database instance stores.

### 01 September 2020 Release

  * Supports HTTP URLs as a data source.

  * Supports AWS S3 Intelligent Tiering and Standard-Infrequent Access storage classes.

  * Supports `$unionWith` aggregation stage.

  * Restricts federated database instance connection string authentication to one user at a time.

  * Includes general performance and stability improvements.

### 18 August 2020 Release

  * Improves $out to S3 write performance.

  * Includes general performance and stability improvements.

### 13 August 2020 Release

  * Adds `correlationID` to the $currentOp output.

  * Includes general performance and stability improvements.

### 28 July 2020 Release

  * Relaxes `$out` S3 region requirement.

  * Includes improved storage configuration error messages.

  * Includes general performance and stability improvements.

### 14 July 2020 Release

  * Supports `$collStats` aggregation pipeline stage.

  * Includes performance optimizations for ORC files.

  * Includes general performance and stability improvements.

### 07 July 2020 Release

  * Adds support for the `skip` and `limit` fields to the `count()` command.

### 16 June 2020 Release

  * Adds `storageValidateConfig` command to validate your federated database instance storage configuration.

  * Includes bug fixes and performance improvements.

### 02 June 2020 Release

  * Includes general performance and stability improvements.

### 26 May 2020 Release

  * Adds support for Atlas Clusters as a data source.

  * Improves performance for the `$lookup` aggregation pipeline stage.

  * Adds support for evaluating string $convert expressions in the `filename` for `$out` to S3.

  * Updates Parquet support for MAP types.

  * Improves error messaging for `$out` to S3.

  * Adds a command to generate a storage configuration.

### 12 May 2020 Release

  * Automates storage configuration generation for newly created federated database instances.

  * Allows write partitioning-aware data to S3 using the `$out` in Data Federation.

### 05 May 2020 Release

  * Generates Storage Configs when Atlas creates a federated database instance.

  * Adds support for `$out` to S3.

  * Updates support for Apache Parquet LIST element.

  * Upgrades wire protocol support to 4.2 from 3.6.

  * Adds support for verbosity in the explain plan.

### 26 April 2020 Release

  * Fixes stability issues.

### 14 April 2020 Release

  * Improves performance.

  * Supports the $currentOp stage so that you can monitor query progress on long-running queries.

  * Updates the isodate attribute to accept additional formats.

  * Refreshes the metadata catalog when you use Storage Configuration commands.

### 26 March 2020 Release

  * Includes various performance and stability improvements.

  * Supports filename field references for `$out`.

  * Supports $toString in `$out` to S3.

### 09 March 2020 Release

  * Supports optionally granting federated database instance write access to S3 buckets, enabling use of `$out` semantics to write directly to those buckets.

  * Adds incremental store, database, collection, and view commands for storage configuration management.

  * Limits collections returned for wildcard collections to 1,000.

  * Updates the storage configuration format.

### 11 February 2020 Release

  * Supports cross-database `$lookup` queries.

  * Supports lowercase and uppercase file extensions.

  * Template segments now support dot-separated attribute names that correspond to nested fields.

### 21 January 2020 Release

  * Allows the defaultFormat to be specified without a leading dot.

  * Supports filtering based on stripes for files in ORC format.

  * Allows query attributes to be extracted after the first stage.

## 2019 Releases

### 10 December 2019 Release

  * Includes several performance and stability improvements.

  * Supports partition definition for the following:

    * `epoch_secs`, which is seconds since the Unix Epoch

    * `epoch_millis`, which is milliseconds since the Unix Epoch

    * `UUID`, which is binary subtype 4

### 11 November 2019 Release

  * Includes several performance and stability improvements.

  * Adds support for reading Apache ORC files.

### 29 October 2019 Release

  * Supports filtering partitions by Parquet file row group statistics.

  * Supports ObjectIds in the path when specifying partition `databases.<database>.<collection>.[n].definition`.

### 08 October 2019 Release

  * Returns an error if a query produces a document larger than 16 MiB.

  * The `$indexStats` stage now produces an empty list of indexes instead of an error.

  * Supports `$out` to S3 storage format in JSON.

  * `$match` now implicitly treats all terms as conjunctions.

  * No longer parses empty files.

  * Fixes an issue that caused the `{$match: {$expr: {$and: []}}}` expression to terminate the connection.

### 17 September 2019 Release

  * Allows nested fields in partition definitions.

  * No longer enumerates directories on S3 when a single subdirectory containing all the partitions matching the query is identified.

  * Fixes an issue where the new storage configuration did not appear on the issuing connection after running setStorageConfig.

### 21 August 2019 Release

  * Adds support for the `getLastError` database command.

  * Fixes a bug with how union types are handled in Avro.

  * Supports `$out` aggregation pipeline stage to S3.

  * `listIndexes` now always returns an empty list.

  * Translates dot-delimited CSV and TSV keys into subdocuments.

  * Storage configuration error message now includes a link to the documentation.

  * Supports the XLSX file format.

  * Includes the correlation ID in query execution error messages.

  * Returns an error to the client when the cursor storage limit is reached.

  * Returns an error to the client on the last `getMore` if the cursor storage limit is exceeded.

### 30 July 2019

  * Supports `listCommands`. For example: `db.runCommand({"listCommands": 1})`

  * Includes partition size information in the output of `explain()`.

### 08 July 2019

  * Returns the first batch of cursor results more quickly.

  * Improves performance of `$lookup` when combined with `$unwind`.

  * Automatically supports `SCRAM-SHA-1` credentials without requiring drivers to specify this authentication mechanism.

  * Provides a descriptive error message when the file format is unknown.

  * Provides additional validation on setStorageConfig.

### 18 June 2019

Initial public beta release of Set Up and Query Data Federation.

← Atlas ChangelogAtlas Kubernetes Operator Changelog →

