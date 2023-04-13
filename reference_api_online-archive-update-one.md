Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Update an Online Archive

Share Feedback

On this page

  * Syntax
  * Request Parameters
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Examples
  * Update Date Criteria
  * Update Custom Criteria
  * Pause Online Archive
  * Error Codes

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

You can pause or resume archiving for an online archive or modify the
archiving criteria in an online archive from the API. You can also pause and
resume or edit an online archive from the Atlas UI. You must have the
`GROUP_DATA_ACCESS_ADMIN` (`Project Data Access Admin`) role to update an
online archive.

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

    
    
    PATCH /groups/{GROUP-ID}/clusters/{CLUSTER-NAME}/onlineArchives/{ARCHIVE-ID}  
      
  
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

Name of the cluster that contains the collection whose online archive to
update.  
  
`ARCHIVE-ID`

|

Required

|

Unique identifier of the online archive to update.  
  
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
  
### Request Body Parameters

Name

|

Type

|

Necessity

|

Description  
  
|||  
  
`criteria`

|

object

|

Optional

|

Criteria to use for archiving data. This is only required for modifying the
archiving criteria.  
  
`criteria.type`

|

string

|

Required

|

Type of criteria. Value can be one of the following:

  * `DATE` \- to select documents for archiving based on a date.

  * `CUSTOM` \- to select documents for archiving based on a custom JSON query.

  
  
`criteria.dateField`

|

string

|

Conditional

|

Required if `criteria.type` is `DATE`. Immutable.

Name of an already indexed date field from the documents. Data is archived
when the current date is greater than the value of the date field specified
here plus the number of days specified via the `expireAfterDays` parameter.  
  
`criteria.dateFormat`

|

enum

|

Conditional

|

Required if `criteria.type` is `DATE`. Immutable.

If `criteria.type` is `DATE`, the date format. Value can be one of the
following:

  * `ISODATE` \- ISO-8601 format date (default)

  * `EPOCH_SECONDS` \- Unix timestamp in seconds

  * `EPOCH_MILLIS` \- Unix timestamp in milliseconds

  * `EPOCH_NANOSECONDS` \- Unix timestamp in nanoseconds

  
  
`criteria.expireAfterDays`

|

int

|

Conditional

|

Required if `criteria.type` is `DATE`.

The number of days after which the data in the live Atlas cluster can be
archived.  
  
`criteria.query`

|

string

|

Conditional

|

Required if `criteria.type` is `CUSTOM`.

JSON query to use to select documents to archive. Atlas uses the specified
query with the db.collection.find(query) command. The empty document `{}` to
return all documents is not supported.  
  
`dataExpirationRule`

|

object

|

Optional

|

Rule for specifying when data should be deleted from the archive. This data
expiration rule takes effect only after 24 hours.  
  
`dataExpirationRule.expireAfterDays`

|

int

|

Required

|

Number of days after which Atlas must delete archived data. Value can be
between `7` and `9125` days (25 years). Atlas deletes archived data after the
number of days you specify here.  
  
`paused`

|

boolean

|

Optional

|

Pause or resume archiving for the online archive. Value can be:

  * `true` \- to pause archiving for an active online archive

  * `false` \- to resume archiving for a paused online archive

## Note

The resume request will fail if the collection has another active online
archive.

This is required for pausing an active or resume a paused online archive.

Either `paused` or `criteria` is required.  
  
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
  
## Examples

### Update Date Criteria

The following example request updates the number of days criteria for an
online archive from 5 days to 7 days and the number of days after which Atlas
deletes archived data to 1000 days. The example response contains the updated
archiving criteria and the data expiration rule for the `people.employees`
collection in the cluster named `myTestClstr`.

#### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
    --header "Content-Type: application/json" \  
    --include \  
    --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5e2211c17a3e5a48f5497de3/clusters/myTestClstr/onlineArchives/5ebad3c1fe9c0ab8d37d61e1?pretty=true" \  
    --data '  
      {  
              "criteria": {  
          "type": "DATE",  
          "dateField": "startDate",  
          "dateFormat": "ISODATE",  
                      "expireAfterDays": 7  
        }  
      },  
      {  
        "dataExpirationRule": {  
          "expireAfterDays": 1000  
        }  
      }'  
  
#### Example Response

    
    
    {  
      
      "_id": "5ebad3c1fe9c0ab8d37d61e1",  
      "clusterName": "onlineArchiveSbx",  
      "collName": "employees",  
      "collectionType": "STANDARD",  
      "criteria": {  
         "type": "DATE",  
         "dateField": "startDate",  
         "dateFormat": "ISODATE",  
         "expireAfterDays": 7  
      },  
      "dataExpirationRule": {  
        "expireAfterDays": 1000  
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
             "fieldName": "startDate",  
             "fieldType": "date",  
             "order": 2  
         }  
      ],  
      "paused": false  
    }  
  
### Update Custom Criteria

The following example request modifies the custom query used to select
documents in the `people.employees` collection from `engineering` department
to `sales` and the `lastDate` field exists. The example response contains the
updated archiving criteria for the `people.employees` collection in the
cluster named `myTestClstr`.

#### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
    --header "Content-Type: application/json" \  
    --include \  
    --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5e2211c17a3e5a48f5497de3/clusters/myTestClstr/onlineArchives/5fca93aa94f65a28923fe0ed?pretty=true" \  
    --data '  
      {  
        "criteria": {  
          "type": "CUSTOM",  
          "query": "{\"department\":\"sales\", lastDate: { $exists: true }}"  
        }  
      }'  
  
#### Example Response

    
    
    {  
      
      "_id": "5fca93aa94f65a28923fe0ed",  
      "clusterName": "myTestClstr",  
      "collName": "employees",  
      "collectionType": "STANDARD",  
      "criteria": {  
         "type": "CUSTOM",  
         "query": "{\"department\":\"sales\", lastDate: { $exists: true }}"  
      },  
      "dbName": "people",  
      "groupId": "5e2211c17a3e5a48f5497de3",  
      "partitionFields": [  
         {  
             "fieldName": "name.firstName",  
             "fieldType": null,  
             "order": 0  
         },  
         {  
             "fieldName": "name.lastName",  
             "fieldType": null,  
             "order": 1  
         }  
      ],  
      "paused": false,  
      "state": "PENDING"  
    }  
  
### Pause Online Archive

The following example request pauses archiving for an online archive specified
by its ID. The example response contains the updated status of the online
archive for the `people.employees` collection in the cluster named
`myTestClstr`.

#### Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" --digest \  
      
    --header "Content-Type: application/json" \  
    --include \  
    --request PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/5e2211c17a3e5a48f5497de3/clusters/myTestClstr/onlineArchives/5ebad3c1fe9c0ab8d37d61e1?pretty=true" \  
    --data '{ "paused": true }'  
  
#### Example Response

    
    
    {  
      
      "_id": "5ebad3c1fe9c0ab8d37d61e1",  
      "clusterName": "myTestClstr",  
      "collName": "employees",  
      "collectionType": "STANDARD",  
      "criteria": {  
         "type": "DATE",  
         "dateField": "startDate",  
         "dateFormat": "ISODATE",  
         "expireAfterDays": 7  
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
             "fieldName": "startDate",  
             "fieldType": "date",  
             "order": 2  
         }  
      ],  
      "paused": true  
    }  
  
## Error Codes

If the request fails, it returns one of the following errors:

Error Code

|

Description  
  
|  
  
`INVALID_GROUP_ID`

|

The specified project ID is not valid.  
  
`CLUSTER_NOT_FOUND`

|

There is no cluster with the specified name in the specified project.  
  
`CLUSTER_DELETE_REQUESTED`

|

The cluster for the online archive is being deleted.  
  
`NAMESPACE_HAS_ONLINE_ARCHIVE`

|

The collection has another active online archive and so, the specified online
archive can't be resumed.  
  
`RESOURCE_NOT_FOUND`

|

The specified archive ID is not valid.  
  
What is MongoDB Atlas? →

