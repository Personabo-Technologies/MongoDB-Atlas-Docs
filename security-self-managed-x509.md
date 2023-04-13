Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Set Up Self-Managed X.509 Authentication

Share Feedback

On this page

  * Considerations
  * Prerequisites
  * Configure a Project to use a Public Key Infrastructure
  * View or Modify Self-Managed X.509 Authentication Settings
  * Add a Database User using Self-Managed X.509 Authentication

Self-managed X.509 certificates provide database users access to the database
deployments in your project. Database users are separate from Atlas users.
Database users have access to MongoDB databases, while Atlas users have access
to the Atlas application itself.

## Considerations

If you enable LDAP authorization, you can't connect to your database
deployments with users that authenticate with an Atlas-managed X.509
certificate.

After you enable LDAP authorization, you _can_ connect to your database
deployments with users that authenticate with an self-managed X.509
certificate. However, the user's Common Name in their X.509 certificate must
match the Distinguished Name of a user who is authorized to access your
database with LDAP.

You can have both users that authenticate with self-managed certificates and
users that authenticate with Atlas-managed X.509 certificates in the same
database.

## Prerequisites

To use self-managed X.509 certificates, you must have a Public Key
Infrastructure to integrate with MongoDB Atlas.

## Configure a Project to use a Public Key Infrastructure

1

### Turn on Self-Managed X.509 Authentication.

  1. In the Security section of Atlas's left navigation panel, click Advanced.

  2. Toggle Self-Managed X.509 Authentication to ON.

2

### Provide a PEM-encoded Certificate Authority.

Atlas CLI

Atlas UI

To save one customer-managed X.509 configuration for the project you specify
using the Atlas CLI, run the following command:

    
    
    atlas security customerCerts create [options]  
      
  
To learn more about the command syntax and parameters, see the Atlas CLI
documentation for atlas security customerCerts create.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## View or Modify Self-Managed X.509 Authentication Settings

Atlas CLI

Atlas UI

To return the details for one customer-managed X.509 configuration for the
project you specify using the Atlas CLI, run the following command:

    
    
    atlas security customerCerts describe [options]  
      
  
To disable one customer-managed X.509 configuration for the project you
specify using the Atlas CLI, run the following command:

    
    
    atlas security customerCerts disable [options]  
      
  
To learn more about the syntax and parameters for the previous commands, see
the Atlas CLI documentation for atlas security customerCerts describe and
atlas security customerCerts disable.

## Tip

### See: Related Links

  * Install the Atlas CLI

  * Connect to the Atlas CLI

## Add a Database User using Self-Managed X.509 Authentication

1

### Open the Add New Database User dialog.

  1. In the Security section of the left navigation, click Database Access. The Database Users tab displays.

  2. Click __ Add New Database User.

2

### Select CERTIFICATE.

3

### Enter user information.

Field

|

Description  
  
|  
  
Distinguished Name

|

The user's Common Name (CN) and optionally additional Distinguished Name
fields (RFC 4514) from the following table:

|

Name

|

Description

|

Type

|

Size (in MB)  
  
|||  
  
`businesscategory`

|

`businessCategory` attribute that describes the kinds of business performed by
an organization.

|

DirectoryString

|

SIZE(1..128)  
  
`c`

|

Two-letter ISO 3166 country code.

|

StringType

|

SIZE(2)  
  
`cn`

|

Common names of an object. If the object corresponds to a person, it is
typically the person's full name.

|

StringType

|

SIZE(1..64)  
  
`countryofcitizenship`

|

RFC 3039 `CountryOfCitizenship` attribute that contains the identifier of at
least one country of citizenship. Accepts ISO 3166 codes only.

|

PrintableString

|

SIZE(2)  
  
`countryofresidence`

|

RFC 3039 `CountryOfResidence` attribute that contains the value of at least
one country. Accepts ISO 3166 codes only.

|

PrintableString

|

SIZE(2)  
  
`dateofbirth`

|

RFC 3039 `DateOfBirth` attribute, which specifies the date of birth of the
subject.

|

GeneralizedTime in this format: `YYYYMMDD000000Z`.

|  
  
`dc`

|

`domainComponent` attribute type that contains a DNS domain name.

|

StringType

|  
  
`dn`

|

`dnQualifier` attribute type that contains disambiguating information to add
to the relative distinguished name of an entry.

|

DirectoryString

|

SIZE(1..64)  
  
`e`

|

Email address in Verisign certificates.

|

|  
  
`emailaddress`

|

`emailAddress` (RSA PKCS#9 extension) attribute that specifies the electronic-
mail address or addresses as an unstructured ASCII string.

|

IA5String

|  
  
`gender`

|

RFC 3039 `Gender` attribute that specifies the value of the gender of the
subject. Accepts `M`, `F`, `m`, or `f`.

|

PrintableString

|

SIZE(1)  
  
`generation`

|

`generationQualifier` attribute type that contains name strings that are
typically the suffix part of a person's name.

|

DirectoryString

|

SIZE(1..64)  
  
`givenname`

|

Name strings that are the part of a person's name that is not their surname.

|

DirectoryString

|

SIZE(1..64)  
  
`initials`

|

Initials of some or all of an individual's names, except the surname(s).

|

DirectoryString

|

SIZE(1..64)  
  
`l`

|

`localityName` attribute that contains names of a locality or place, such as a
city, county, or other geographic region.

|

StringType

|

SIZE(1..64)  
  
`name`

|

(`id-at-name`) Attribute supertype from which user attribute types with the
name syntax inherit.

|

DirectoryString

|

SIZE(1..64)  
  
`nameofbirth`

|

ISIS-MTT `NameAtBirth` attribute that specifies the name of a person at his or
her birth.

|

DirectoryString

|

SIZE(1..64)  
  
`o`

|

Name of an organization.

|

StringType

|

SIZE(1..64)  
  
`ou`

|

Name of an organizational unit.

|

StringType

|

SIZE(1..64)  
  
`placeofbirth`

|

RFC 3039 `PlaceOfBirth` that specifies the value of the place of birth.

|

DirectoryString

|

SIZE(1..128)  
  
`postaladdress`

|

RFC 3039 `PostalAddress`, which includes the `stateOrProvinceName` and the
`localityName` attribute types, if present, to store address and geographical
information.

|

Sequence

|

SIZE (1..6) OF DirectoryString(SIZE(1..30))  
  
`postalcode`

|

`postalCode` attribute that specifies the code used by a Postal Service to
identify postal service zone.

|

DirectoryString

|

SIZE(1..40)  
  
`pseudonym`

|

RFC 3039 `pseudonym` attribute that specifies a pseudonym, such as nicknames
and names with spelling other than defined by the registered name.

|

DirectoryString

|

SIZE(1..64)  
  
`serialnumber`

|

Device serial number name.

|

StringType

|

SIZE(1..64)  
  
`sn`

|

Device serial number name.

|

StringType

|

SIZE(1..64)  
  
`st`

|

State, or province name.

|

StringType

|

SIZE(1..64)  
  
`street`

|

Name of street.

|

StringType

|

SIZE(1..64)  
  
`surname`

|

Naming attributes of type X520name.

|

DirectoryString

|

SIZE(1..64)  
  
`t`

|

`Title` attribute, which contains the designated position or function of the
subject within an organization.

|

DirectoryString

|

SIZE(1..64)  
  
`telephonenumber`

|

`id-at-telephoneNumber`, which is an internationally agreed-upon format for
international telephone numbers.

|

PrintableString

|

SIZE (1..32)  
  
`uid`

|

LDAP User ID.

|

DirectoryString

|  
  
`uniqueidentifier`

|

Unique identifier for an object.

|

DirectoryString

|  
  
`unstructuredaddress`

|

PKCS#9 attribute that specifies the address or addresses of a subject as an
unstructured directory string.

|

DirectoryString

|  
  
`unstructuredname`

|

PKCS#9 attribute that specifies the name or names of a subject as an
unstructured ASCII string..

|

DirectoryString

|

SIZE(1..64)  
  
For more information on Distinguished Name fields, see RFC 4514.

## Example

CN=Jane Doe,O=MongoDB,C=US  
  
User Privileges

|

You can assign roles in one of the following ways:

  * Select `Atlas admin`, which provides the user with `readWriteAnyDatabase` as well as a number of administrative privileges.

  * Select `Read and write to any database`, which provides the user with privileges to read and write to any database.

  * Select `Only read any database` which provides the user with privileges to read any database.

  * Select Select Custom Role to select a custom role previously created in Atlas. You can create custom roles for database users in cases where the built-in database user roles cannot describe the desired set of privileges. For more information on custom roles, see Configure Custom Database Roles.

  * Click Add Default Privileges. When you click this option, you can select individual roles and specify the database on which the roles apply. Optionally, for the `read` and `readWrite` roles, you can also specify a collection. If you do not specify a collection for `read` and `readWrite`, the role applies to all non-`system` collections in the database.

## Note

The following table describes the Atlas specific privileges, the database it
applies to, and the privilege actions they represent.

|

Atlas Specific Privilege

|

Database

|

Privilege Actions  
  
||  
  
`backup`

|

`admin`

|

    * `listDatabases`

    * `listCollections`

    * `listIndexes`

    * `appendOplogNote`

    * `getParameter`

    * `serverStatus`  
  
`clusterMonitor`

|

`admin`

|

    * `checkFreeMonitoringStatus`

    * `connPoolStats`

    * `getCmdLineOpts`

    * `getDefaultRWConcern`

    * `getLog`

    * `getParameter`

    * `getShardMap`

    * `hostInfo`

    * `inprog`

    * `listDatabases`

    * `listSessions`

    * `listShards`

    * `netstat`

    * `replSetGetConfig`

    * `replSetGetStatus`

    * `serverStatus`

    * `setFreeMonitoring`

    * `shardingState`

    * `top`  
  
`dbAdmin`

|

User configured

|

    * `bypassDocumentValidation`

    * `changeStream`

    * `collMod`

    * `collStats`

    * `compact`

    * `convertToCapped`

    * `createCollection`

    * `createIndex`

    * `dbHash`

    * `dbStats`

    * `dropCollection`

    * `dropDatabase`

    * `dropIndex`

    * `enableProfiler`

    * `find`

    * `killCursors`

    * `listCollections`

    * `listIndexes`

    * `planCacheIndexFilter`

    * `planCacheRead`

    * `planCacheWrite`

    * `reIndex`

    * `renameCollectionSameDB`

    * `storageDetails`

    * `validate`  
  
`dbAdminAnyDatabase`

|

User configured except `local` and `config`

|

    * `dbAdminAnyDatabase`  
  
`enableSharding`

|

|

    * `enableSharding`  
  
`read`

|

User configured

|

    * `changeStream`

    * `collStats`

    * `dbHash`

    * `dbStats`

    * `find`

    * `killCursors`

    * `listIndexes`

    * `listCollections`  
  
`readWrite`

|

User configured

|

    * `changeStream`

    * `collStats`

    * `convertToCapped`

    * `createCollection`

    * `dbHash`

    * `dbStats`

    * `dropCollection`

    * `createIndex`

    * `dropIndex`

    * `find`

    * `insert`

    * `killCursors`

    * `listIndexes`

    * `listCollections`

    * `remove`

    * `renameCollectionSameDB`

    * `update`  
  
`killOpSession`

|

User configured

|

    * `inprog`

    * `killop`

    * `killAnySession`

    * `listSessions`  
  
`readWriteAnyDatabase`

|

User configured except `local` and `config`

|

    * `readWriteAnyDatabase`

    * `changeStream`

    * `collStats`

    * `convertToCapped`

    * `createCollection`

    * `dbHash`

    * `dbStats`

    * `dropCollection`

    * `createIndex`

    * `dropIndex`

    * `find`

    * `insert`

    * `killCursors`

    * `listIndexes`

    * `listCollections`

    * `listDatabases`

    * `remove`

    * `renameCollectionSameDB`

    * `update`  
  
`readAnyDatabase`

|

User configured except `local` and `config`

|

    * `readAnyDatabase`

    * `changeStream`

    * `collStats`

    * `dbHash`

    * `dbStats`

    * `find`

    * `killCursors`

    * `listIndexes`

    * `listCollections`

    * `listDatabases`  
  

For information on the built-in Atlas privileges, see Built-in Roles.

For more information on authorization, see Role-Based Access Control and
Built-in Roles in the MongoDB manual.  
  
4

### Click Add User.

← Configure User Authentication and Authorization with OneLogin
VLDAPEncryption at Rest using Customer Key Management →

