Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Get One Online Archive

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Response Elements
  * Example
  * Example Request
  * Example Response
  * Error Codes

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can retrieve an online archive using its ID. You can also view an online
archive from the Atlas UI. You must have `GROUP_READ_ONLY` (`Project Read
Only`) role to retrieve an online archive.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

`https://cloud.mongodb.com/api/atlas/v1.0`

## Syntax

    
    
    GET /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}  
      
  
## Request Parameters

### Request Path Parameters

Path Element

|

Necessity

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Unique identifier of the project that contains the specified cluster.  
  
`CLUSTER-NAME`

|

Required

|

Name of the cluster that contains the collection.  
  
`ARCHIVE-ID`

|

Required

|

Unique identifier of the online archive to retrieve.  
  
### Request Query Parameters

This endpoint might use any of the HTTP request query parameters available to
all Atlas Administration API resources. All of these are optional.

Name

|

Type

|

Necessity

|

Description

|

Default  
  
||||  
  
pretty

|

boolean

|

Optional

|

Flag indicating whether the response body should be in a prettyprint format.

|

`false`  
  
envelope

|

boolean

|

Optional

|

Flag indicating if Atlas should wrap the response in a JSON envelope.

This option may be needed for some API clients. These clients cannot access
the HTTP response headers or status code. To remediate this, set
**envelope=true** in the query.

For endpoints that return one result, the response body includes:

|

|  
  
|  
  
status

|

HTTP response code  
  
envelope

|

Expected response body  
  
`false`  
  
## Response Elements

Name

|

Type

|

Description  
  
||  
  
id

|

string

|

ID of the online archive.  
  
clusterName

|

string

|

Name of the cluster that contains the collection.  
  
collName

|

string

|

Name of the collection.  
  
collectionType

|

string

|

Type of collection. Value can be one of the following:

  * `STANDARD` \- for standard collection

  * `TIMESERIES` \- for time series collection

## Important

### Preview

Online Archive for timeseries collection is available as a Preview. The
feature and corresponding documentation may change at any time in the Preview
stage.

  
  
criteria

|

document

|

Criteria to use for archiving data.  
  
criteria.type

|

string

|

Type of criteria. Value can be one of the following:

  * `DATE` \- to select documents for archiving based on a date.

  * `CUSTOM` \- to select documents for archiving based on a custom JSON query.

  
  
criteria.dateField

|

string

|

If `"criteria.type" : "DATE"`, name of the date field that the online archive
is based on. Data is archived when the current date is after the date
specified here plus the number of days specified via the `expireAfterDays`
parameter.  
  
criteria.dateFormat

|

enum

|

If `"criteria.type" : "DATE"`, the date format. Value can be one of the
following:

  * `ISODATE` \- ISO-8601 format date (default)

  * `EPOCH_SECONDS` \- Unix timestamp in seconds

  * `EPOCH_MILLIS` \- Unix timestamp in milliseconds

  * `EPOCH_NANOSECONDS` \- Unix timestamp in nanoseconds

  
  
criteria.expireAfterDays

|

int

|

If `"criteria.type" : "DATE"`, number of days that specifies the age limit for
the data in the live Atlas cluster. Data is archived when the current date is
greater than the value of the date field specified via the `dateField`
parameter plus the number of days specified here.  
  
criteria.query

|

int

|

If `"criteria.type" : "CUSTOM"`, JSON query used to select documents for
archiving. The specified query is used with the db.collection.find(query)
command.  
  
dataExpirationRule

|

object

|

Rule that specifies when data should be deleted from the archive. The data
expiration rule takes effect only after 24 hours.  
  
dataExpirationRule.expireAfterDays

|

int

|

Number of days after which Atlas must delete archived data. Value can be
between `7` and `9125` days (25 years). Atlas deletes archived data after the
number of days you specify here.  
  
dbName

|

string

|

Name of the database that contains the collection.  
  
groupId

|

string

|

Unique identifier of the project that contains the cluster.  
  
partitionFields

|

document array

|

Fields to use to partition data.  
  
partitionFields.fieldName

|

string

|

Name of the field.  
  
partitionFields.fieldType

|

string

|

Data type of the field.  
  
partitionFields.order

|

int

|

Position of the field in the partition. Value can be:

  * `0` \- for the first position

  * `1` \- for the second position

  * `2` \- for the third position

  
  
paused

|

boolean

|

State of the online archive. Value is:

  * `true` if the online archive is in paused state.

  * `false` if the online archive is in pending or active state.

  
  
state

|

string

|

Status of the online archive. Valid values are:

|

|  
  
|  
  
Pending

|

Indicates documents are queued for archive, but archiving has not yet started.  
  
Archiving

|

Indicates archiving has started. In this state, the documents that meet the
criteria for archiving are being archived.  
  
Idle

|

Indicates online archive is waiting for the next archival job to start.  
  
Pausing

|

Indicates that you have requested to pause archiving. In this state, Atlas is
finishing the running archiving operation and therefore, Atlas has not yet put
archiving on hold. The online archive transitions to the `Paused` state when
the running archiving operation finishes.  
  
Paused

|

Indicates archiving has been temporarily stopped. In this state, previously
archived documents continue to be available on the cloud object storage for
querying, but the specified archiving operation on the active cluster is put
on hold and additional documents are not archived. You can resume archiving
for paused archives at any time.  
  
Orphaned

|

Indicates collection associated with an active or paused online archive was
deleted. Atlas will not automatically delete the archived data. You must
manually delete the online archives associated with the deleted collection.  
  
Deleted

|

Indicates online archive was deleted. When you delete an online archive,
associated archived documents are removed from the cloud object storage.  
  
## Example

The following example request retrieves an online archive by its ID. The
example response contains the online archive with the ID
`5ebad3c1fe9c0ab8d37d61e1` for the `people.employees` collection in the
cluster named `myTestClstr`.

### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/5e2211c17a3e5a48f5497de3/clusters/myTestClstr/onlineArchives/5ebad3c1fe9c0ab8d37d61e1?pretty=true"  
  
### Example Response

    
    
    {  
      
      "_id": "5ebad3c1fe9c0ab8d37d61e1",  
      "clusterName": "myTestClstr",  
      "collName": "employees",  
      "collectionType": "STANDARD",  
      "criteria": {  
         "type": "DATE",  
         "dateField": "created",  
         "dateFormat": "ISODATE",  
         "expireAfterDays": 5  
      },  
      "dataExpirationRule": {  
        "expireAfterDays": 500  
      },  
      "dbName": "people",  
      "groupId": "5e2211c17a3e5a48f5497de3",  
      "partitionFields": [  
         {  
             "fieldName": "firstName",  
             "fieldType": "string",  
             "order": 0  
         },  
         {  
             "fieldName": "lastName",  
             "fieldType": "string",  
             "order": 1  
         },  
         {  
             "fieldName": "created",  
             "fieldType": "date",  
             "order": 2  
         }  
      ],  
      "paused": false,  
      "state": "ACTIVE"  
    }  
  
## Error Codes

If the request fails, it returns the following error:

Error Code

|

Description  
  
|  
  
`RESOURCE_NOT_FOUND`

|

The specified archive ID is not valid.  
  
What is MongoDB Atlas? →

