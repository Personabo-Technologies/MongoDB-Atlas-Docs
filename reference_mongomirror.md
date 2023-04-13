Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# mongomirror

Share Feedback

On this page

  * Syntax
  * Options
  * Examples

`mongomirror` is a tool for manually migrating data from an existing MongoDB
replica set to a MongoDB Atlas replica set.

## Syntax

To run `mongomirror`, you must specify:

  * The source replica set and the target Atlas replica set.

  * A user in the Atlas cluster with appropriate privileges, the corresponding password, and appropriate privileges, if the source replica set requires authentication.

    
    
    mongomirror --host <sourceReplSet> \  
      
       --destination <atlasCluster> \  
       --destinationUsername <atlasAdminUser> \  
       --destinationPassword <atlasPassword> \  
       [Additional options]  
  
You can specify some options in the `config file` instead of including them in
the command.

## Options

`--host <host>`

    

The host information for the source replica set. Specify the replica set name
and a seed list of the members, as in the following:

    
    
    <RSname>/<host1>:<port1>,<host2>:<port2>,<host3>:<port3>  
      
  
`--username <username>`

    

If the source replica set requires authentication, the name of a user in the
source replica set with privileges to read any database, including the `local`
database. A user with the `backup` role provides the appropriate privileges.
For details on the specific privileges required, see Required Access on Source
Replica Set.

`--password <password>`

    

Password for the user specified in `--username`.

`--authenticationDatabase <authenticationDatabase>`

    

The database in the source replica set where the user specified in
`--username` was created. The authentication database for:

  * SCRAM-authenticated users is the `admin` database.

  * X.509-authenticated users is the `$external` database.

  * AWS IAM-authenticated users is the `$external` database.

To learn more, see Authentication Database.

`--authenticationMechanism <authenticationMechanism>`

    

The authentication mechanism to use to authenticate the user to the source
replica set.

Value

|

Description  
  
|  
  
SCRAM-SHA-1

|

RFC 5802 standard Salted Challenge Response Authentication Mechanism using the
SHA-1 hash function.  
  
SCRAM-SHA-256

|

RFC 5802 standard Salted Challenge Response Authentication Mechanism using the
SHA-256 hash function.  
  
MONGODB-CR

|

MongoDB challenge/response authentication.  
  
MONGODB-X509

|

MongoDB TLS/SSL certificate authentication.  
  
GSSAPI (Kerberos)

|

External authentication using Kerberos. This mechanism is available only in
MongoDB Enterprise.  
  
PLAIN (LDAP SASL)

|

External authentication using LDAP. You can also use `PLAIN` for
authenticating in-database users. `PLAIN` transmits passwords in plain text.
This mechanism is available only in MongoDB Enterprise.  
  
MONGODB-IAM

|

 _New in version 0.10.0_

External authentication with AWS IAM.

To authenticate with AWS IAM credentials, use the following options:

  * `--username` <AWS access key id>

  * `--password` <secret access key id>

  * `--awsSessionToken` <AWS session token>

  
  
To learn more, see Authentication Mechanisms.

`--awsSessionToken`

    

 _New in version 0.10.0_

An AWS session token for use with the `MONGODB-IAM` authentication mechanism.

`--compressors <snappy,...>`

    

 _New in version 0.9.0_

Comma-separated list of compressors to enable. Use 'none' to disable. Default:
`snappy,zstd,zlib`

`--config=<file>`

    

YAML file that stores options and values for `mongomirror`. Specify the file
using relative or absolute paths to run `mongomirror` with the options that
the file contains.

The config file supports the following options:

  * `password` <password>

  * `sslPEMKeyPassword` <password>

  * `destinationPassword` <password>

  * `uri` <source cluster URI connection string>

Specify options in the config file using the `option: value` syntax. Don't
include `--` before options in the config file. If you set an option in the
configuration file, you don't need to specify that option within the
`mongomirror` command.

## Example

Create a config file called `myconfig.yaml` that contains the following:

    
    
    password: <passwordForUser>  
      
    destinationPassword: <passwordForDestinationUser>  
  
You can run `mongomirror` without including the `--password` and
`--destinationPassword` flags:

    
    
    mongomirror --host <sourceReplSet> \  
      
       --ssl \  
       --username <atlasAdminUser> \  
       --destinationUsername <atlasAdminUser> \  
       --config=myconfig.yaml \  
       --destination <atlasCluster> \  
       [Additional options]  
  
`--destination <destination>`

    

The host information for the target Atlas replica set.

Specify the replica set name and a seed list of the members, as in the
following:

    
    
    <RSname>/<host1>:<port1>,<host2>:<port2>,<host3>:<port3>  
      
  
`--destinationAuthenticationDatabase <authentication database>`

    

Authentication database for the database user in the Atlas cluster. The
authentication database for SCRAM-authenticated users is the `admin` database.

To learn more, see Database User Authentication.

`--destinationAuthenticationMechanism <authentication mechanicsm>`

    

Authentication mechanism for the database user in the Atlas cluster. Atlas
offers the following forms of authentication for database users:

Value

|

Description  
  
|  
  
SCRAM-SHA-1

|

RFC 5802 standard Salted Challenge Response Authentication Mechanism using the
SHA-1 hash function.  
  
SCRAM-SHA-256

|

RFC 5802 standard Salted Challenge Response Authentication Mechanism using the
SHA-256 hash function.  
  
MONGODB-CR

|

MongoDB challenge/response authentication.  
  
PLAIN (LDAP SASL)

|

External authentication using LDAP. You can also use `PLAIN` for
authenticating in-database users. `PLAIN` transmits passwords in plain text.
This mechanism is available only in MongoDB Enterprise.  
  
To learn more, see Database User Authentication.

`--destinationUsername <Atlas user name>`

    

Name of a database user in the Atlas cluster with privileges to read, write,
and admin any database. A user with the Atlas admin role provides the
appropriate privileges. For details on the specific privileges required, see
Required Access on Target Cluster.

`--destinationPassword <password>`

    

Password of the database user specified in `--destinationUsername`.

`--drop`

    

Flag that indicates that `mongomirror` should drop all user collections
(viewable in each database with `listCollections`) on the target cluster. This
option doesn't drop internal collections like `local.system*` and the oplog.

`--noIndexRestore`

    

 _New in version 0.10.0_

Omit indexes when migrating data.

`--includeNamespace <database.collection>`

    

Specify a namespace on the source cluster to mirror to the target cluster. May
be provided multiple times.

## Note

If a transaction spans multiple namespaces, only write operations applied to
the namespaces specified in `--includeNamespace` or `--includeDB` are applied
to the destination cluster.

`--includeDB <database>`

    

Specify a database on the source cluster to mirror to the target cluster. May
be provided multiple times.

## Note

If a transaction spans multiple namespaces, only write operations applied to
the namespaces specified in `--includeNamespace` or `--includeDB` are applied
to the destination cluster.

`--ssl`

    

Enables TLS/SSL encrypted connections to the source replica set.

`--sslPEMKeyFile <file>`

    

The .pem file if the source replica set requires clients to present a
certificate. The .pem file contains both the TLS/SSL certificate and key.
Specify the file using relative or absolute paths.

`--sslPEMKeyPassword <value>`

    

Password to decrypt the certificate-key file specified in `--sslPEMKeyFile`.
Use if the `--sslPEMKeyFile` is encrypted.

`--sslCAFile <file>`

    

The .pem file that contains the root certificate chain from the Certificate
Authority(CA) for the source replica set. Specify the file using relative or
absolute paths.

`--sslCRLFile <filename>`

    

The .pem file that contains the Certificate Revocation List for the source
replica set. Specify the file using relative or absolute paths.

`--sslAllowInvalidHostnames`

    

 _Deprecated. Use_ `tlsInsecure` _instead._

Disables the validation of the TLS/SSL certificates presented by the source
replica set. Allows `mongomirror` to connect to the source replica set if the
hostname in the certificates does not match the specified hostname.

## Important

This option skips all certificate validation, which may result in accepting
invalid certificates.

`--sslAllowInvalidCertificates`

    

 _Deprecated. Use_ `tlsInsecure` _instead._

Bypasses the validation checks for certificates presented by the source
replica set. When using the `--allowInvalidCertificates` setting, MongoDB logs
as a warning the use of the invalid certificate.

## Important

This option skips all certificate validation, which may result in accepting
invalid certificates.

`--tlsInsecure`

    

Bypasses the validation checks for the server's certificate chain and host
name. This allows you to use invalid certificates and host names.

This replaces the deprecated `sslAllowInvalidHostnames` and
`sslAllowInvalidCertificates` options.

`--gssapiServiceName <name>`

    

If the source replica set uses Kerberos authentication, the name of the
service using GSSAPI/Kerberos. Only required if the service does not use the
default name of `mongodb`.

This option is available only in MongoDB Enterprise.

`--gssapiHostName <host>`

    

If the source replica set uses Kerberos authentication, the hostname of a
service using GSSAPI/Kerberos. Only required if the hostname of a machine does
not match the hostname resolved by DNS.

This option is available only in MongoDB Enterprise.

`--readPreference <read preference>`

    

 _Deprecated since version 0.9.0_

`mongomirror` always reads from the primary unless the source is a single host
without a replica set name, in which case it makes a direct connection only to
that host.

`--writeConcern <write concern>`

    

 _Deprecated since version 0.2.3_: `mongomirror` always uses majority write
concern.

`--numParallelCollections <num>, -j <num>`

    

 _Default_ : 4

The number of collections to copy and restore in parallel.

`--bypassDocumentValidation`

    

 _Deprecated since version 0.2.3_: `mongomirror` always bypasses document
validation.

`--bookmarkFile <file>`

    

 _Default_ : mongomirror.bookmark

Name of the oplog timestamp bookmark file.

`--forceDump`

    

Flag that indicates that `mongomirror` resync all source collections, even if
a nonempty bookmark file exists.

`--oplogPath <path>`

    

 _New in version 0.5.0_

Enables `mongomirror` to buffer the initial sync oplog window to disk. When
you specify a value for this option, `mongomirror` streams the source oplog
entries to the specified directory in a single file: `<oplogPath>/oplog-
mongomirror.bson.sz`. After the entire oplog file is replayed to the
destination cluster, `mongomirror` removes the file and starts tailing the
source oplog without buffering.

By default, `mongomirror` streams oplog entries from the source and applies
them to the destination cluster. However, the migration may fail if the source
oplog is not large enough to contain the entire initial sync oplog window. To
avoid this error, you can either increase the size of the source oplog, or
specify this option to ensure that the source oplog will not run out of space
during the migration process.

## Important

There must be enough disk space to accommodate all of the source oplog entries
that occur during the initial `mongomirror` sync.

## Example

If the source oplog is 10 GB and covers 24 hours of changes, and
`mongomirror`'s sync is estimated to take 48 hours, there must be at least 20
GB of free disk space in the specified directory.

`--oplogBatchSize <num>`

    

 _Default_ : 10,000

Specify the number of oplog entries to send as a batch. `mongomirror` allows
up to a maximum data volume size of 16 MB of documents to send as a batch.

`--httpStatusPort <num>`

    

Directs `mongomirror` to start an HTTP server on the specified port. You can
retrieve the current status of `mongomirror` by issuing an HTTP `GET` request
to `http://localhost:<num>`.

When running with `--httpStatusPort`, `mongomirror` does not exit when it
encounters an error. Instead, it logs the error as normal and reports the
error over HTTP to the specified port.

`mongomirror` returns a document in response to the HTTP request. The
following example syntax represents all the possible output fields - the
actual response may only return a subset of these fields. See the subsequent
table for a description of the fields and when to expect them.

    
    
    {  
      
       "stage" : "<stage Name>",  
       "phase" : "<phase Name>",  
       "details" : {  
          "currentTimestamp" : "<BSON timestamp>",  
          "latestTimestamp" : "<BSON timestamp>",  
          "lastWriteOnSourceTimestamp" : "<BSON timestamp>",  
          "<namespace>" : {  
             "complete" : <boolean>,  
             "copiedBytes" : <integer>,  
             "totalBytes" : <integer>,  
             "createIndexes" : <integer>  
          },  
          ...  
       },  
       "errorMessage" : "<error message>"  
    }  
  
The following table describes each field and its possible values:

Field

|

Description  
  
|  
  
`stage`

|

The name of the stage in progress. Possible values are:

  * `initializing`

`mongomirror` has started but is not yet copying any data.

  * `initial sync`

`mongomirror` is copying documents and indexes that already exist on the
source deployment. `mongomirror` also tails and applies entries from the
oplog.

  * `oplog sync`

`mongomirror` is tailing and applying entries from the oplog.

  
  
`phase`

|

The name of the phase. Provides more specific details about what part of the
`stage` is in progress.  
  
`details`

|

A document providing a detailed description of the progress of the current
phase.

During the `initial sync` stage, each subdocument in `details` represents a
single collection being copied by `mongomirror`.

Depending on the `stage` or `phase`, `mongomirror` may not include this field
in the response.  
  
`details.<namespace>`

|

The full namespace of the collection being copied, displayed as
`<database>.<collection>`.

Only displays during the `initial sync` phase when copying documents or
indexes.  
  
`details.<namespace>.complete`

|

Displays `true` or `false` depending on whether or not `mongomirror` has
copied all documents or indexes from the collection to the target Atlas
cluster.

Only displays during the `initial sync` phase when copying documents or
indexes.  
  
`details.<namespace>.copiedBytes`

|

The number of bytes copied so far. Note that this is a different measurement
from the `mongomirror` logs, which report the current/total number of
_documents_ copied.

Only displays during the `initial sync` phase when copying non-index data.  
  
`details.<namespace>.totalBytes`

|

The total size (in bytes) of the collection.

Only displays during the `initial sync` phase when copying non-index data.  
  
`details.<namespace>.createIndexes`

|

The number of indexes that have been or will be created.

Only displays during the `initial sync` stage when copying indexes.  
  
`details.currentTimestamp`

|

The BSON timestamp value of the oplog entry most recently processed.
`mongomirror` only refreshes this data point every 10 seconds, so
`mongomirror` may be slightly further ahead of the reported time.

Only displays during the `initial sync` or `oplog sync` stages when tailing or
applying oplog entries.  
  
`details.latestTimestamp`

|

During the `initial sync` stage, this represents the BSON timestamp value of
the latest oplog entry available after the initial data was copied during
initial sync.

During the `oplog sync` stage, this represents the BSON timestamp value of the
latest oplog entry available on the source deployment.

Only displays during the `initial sync` or `oplog sync` stages when tailing or
applying oplog entries.  
  
`details`

`.lastWriteOnSourceTimestamp`

|

The BSON timestamp value of the most recent oplog entry that is not a no-op.
No-op entries are generally system-level operations such as heartbearts that
do not write or edit data in the database. `mongomirror` refreshes this value
every 10 seconds. Operations which write or edit data in the database may not
be reported until the next refresh occurs.

The `lastWriteOnSourceTimestamp` field is useful as a confirmation that no new
writes are occurring on the source deployment before cutting over during a
migration.  
  
`errorMessage`

|

A string that describes any error encountered by `mongomirror`.  
  
`--collStatsThreshold <num>`

    

 _New in version 0.9.0_

Maximum number of collections which may exist before collStats is disabled.
Use `-1` to always run collStats or `0` to never run collStats. Default: `-1`

`--removeAutoIndexId`

    

 _New in version 0.12.0_

Removes the `autoIndexId` option from collections during the initial sync to
the target cluster. Also removes the `autoIndexId` option from any collections
that `mongomirror` creates during the migration.

`--preserveUUIDs`

    

Allows Atlas to preserve UUID during live migration. This option works
**only** with the live migration process that Atlas runs. If you use the
`--preserveUUIDs` option on the command line, it will fail due to permission
errors. These errors are expected because this option isn't intended to be
used on the command line in a self-managed migration process that runs
`mongomirror`.

## Examples

### Migrate a Replica Set to Atlas: No Authentication on Source

The following example migrates from a source replica set that doesn't require
authentication:

    
    
    mongomirror --host  sourceRS/source-host1:27017,source-host2:27017 \  
      
             --destination myAtlasRS/atlas-host1:27017,atlas-host2:27017 \  
             --destinationUsername myAtlasUser \  
             --destinationPassword myAtlasPwd  
  
To migrate from a source replica set that doesn't require authentication, run
`mongomirror` with the following options:

  * `--host` <sourceReplSet/seed list of members>

  * `--destination` <Atlas Cluster>

  * `--destinationUsername` <atlasUser>

  * `--destinationPassword` <atlasPassword>

For the target, specify the replica set name followed by a seed list of
members in the following format:

    
    
    <replicaSetName>/<host1>:<port1>,<host2>:<port2>,<host3>:<port3>,...  
      
  
The specified user must have the `Atlas admin` role on Atlas.

### Migrate a Replica Set: Source Replica Set Uses SCRAM-SHA1 Authentication

The following example migrates a source replica set that uses SCRAM-SHA1
authentication to Atlas:

    
    
    mongomirror --host sourceRS/source-host1:27017,source-host2:27017,source-host3:27017 \  
      
       --username mySourceUser \  
       --password mySourcePassword \  
       --authenticationDatabase admin \  
       --destination myAtlasRS/atlas-host1:27017,atlas-host2:27017 \  
       --destinationUsername myAtlasUser \  
       --destinationPassword atlasPassw0Rd  
  
To migrate from a source replica set that uses SCRAM-SHA1 authentication, run
`mongomirror` with the following options:

  * `--host` <sourceReplSet/seed list of members>

  * `--username` <sourceUser>

  * `--password` <sourcePassword>

  * `--authenticationDatabase` <sourceDatabase>

  * `--destination` <Atlas Cluster>

  * `--destinationUsername` <atlasUser>

  * `--destinationPassword` <atlasPassword>

The source replica set user must have the required access on source cluster.
The `backup` role provides the appropriate privileges.

For the target, specify the replica set name followed by a seed list of
members in the following format:

    
    
    <replicaSetName>/<replicaMember>,<replicaMember>,<replicaMember>,...  
      
  
The specified user must have the `Atlas admin` on Atlas.

### Migrate a Replica Set: Source Replica Set Requires X.509 Client
Authentication

The following example migrates from a source replica set that uses X.509
authentication:

    
    
    mongomirror --host sourceRS/source-host1:27017,source-host2:27017,source-host3:27017 \  
      
       --username "CN=myName,OU=myOrgUnit,O=myOrg,L=myLocality,ST=myState,C=myCountry" \  
       --authenticationDatabase '$external' \  
       --authenticationMechanism MONGODB-X509 \  
       --ssl \  
       --sslPEMKeyFile <path-to-my-client-certificate.pem> \  
       --sslCAFile <path-to-my-certificate-authority-certificate.pem> \  
       --destination myAtlasRS/atlas-host1:27017,atlas-host2:27017 \  
       --destinationUsername myAtlasUser \  
       --destinationPassword atlasPassw0Rd  
  
To migrate from a source replica set that uses X.509 authentication, run
`mongomirror` with the following options:

  * `--host` <sourceReplSet/seed list of members>

  * `--username` <subject from the client certificate>

  * `--authenticationMechanism` `MONGODB-X509`

  * `--authenticationDatabase` `'$external'`

  * `--ssl`

  * `--sslPEMKeyFile` <path-to-my-client-certificate.pem>

  * `--sslCAFile` <path to root CA PEM file>

  * `--destination` <Atlas Cluster>

  * `--destinationUsername` <atlasUser>

  * `--destinationPassword` <atlasPassword>

The source replica set user must have the required access on source cluster.
The `backup` role provides the appropriate privileges.

For the target, specify the replica set name followed by a seed list of
members in the following format:

    
    
    <replicaSetName>/<replicaMember>,<replicaMember>,<replicaMember>,...  
      
  
The specified user must have the `Atlas admin` on Atlas.

### Migrate a Replica Set: Source Replica Set Requires Kerberos/GSSAPI
Authentication

The following example migrates from a source replica set that uses Kerberos
authentication:

    
    
    mongomirror --host sourceRS/source-host1:27017,source-host2:27017,source-host3:27017 \  
      
       --username sourceUser/administrator@MYREALM.COM \  
       --authenticationDatabase '$external' \  
       --authenticationMechanism GSSAPI \  
       --destination myAtlasRS/atlas-host1:27017,atlas-host2:27017,atlas-host3:27017 \  
       --destinationUsername atlasUser \  
       --destinationPassword atlasPass  
  
To migrate from a source replica set that uses Kerberos authentication, run
`mongomirror` with the following options:

  * `--host` <sourceReplSet/seed list of members>

  * `--username` <Kerberos user principal>

  * `--authenticationDatabase` `'$external'`

  * `--authenticationMechanism` `GSSAPI`

  * `--destination` <Atlas Cluster>

  * `--destinationUsername` <atlasUser>

  * `--destinationPassword` <atlasPassword>

The source replica set user must have the required access on source cluster.
The `backup` role provides the appropriate privileges.

For the target, specify the replica set name followed by a seed list of
members in the following format:

    
    
    <replicaSetName>/<replicaMember>,<replicaMember>,<replicaMember>,...  
      
  
The specified user must have the `Atlas admin` on Atlas.

### Save `mongomirror` Output to a File

You can save the output logs from a `mongomirror` procedure to a file for
later examination and debugging. Use the following format to save output to a
`mongomirror.log` file:

    
    
    mongomirror <args> 2>&1 | tee -a mongomirror.log  
      
  
← Migrate with `mongomirror`mongomirror Changelog →

