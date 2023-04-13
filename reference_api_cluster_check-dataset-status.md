Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Check Status of Cluster Sample Dataset Request

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Example Request
  * Example Response

This API reference is deprecated. It will be removed in a future release. For
the latest API reference, see the MongoDB Atlas Administration API
Specification. This new API specification might take several seconds to load.
MongoDB appreciates your patience as it improves this experience.

## Note

Groups and projects are synonymous terms. Your `{GROUP-ID}` is the same as
your project ID. For existing groups, your group/project ID remains the same.
The resource and corresponding endpoints use the term `groups`.

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

Base URL: `https://cloud.mongodb.com/api/atlas/v1.0`

    
    
    GET /groups/{GROUP-ID}/sampleDatasetLoad/{SAMPLE-DATASET-ID}  
      
  
### Request Path Parameters

Path Element

|

Type

|

Necessity

|

Description  
  
|||  
  
GROUP-ID

|

string

|

Required

|

Unique 24-hexadecimal string that identifies the project containing the
cluster.  
  
SAMPLE-DATASET-ID

|

string

|

Required

|

Unique 24-hexadecimal string that identifies this sample dataset.  
  
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

This endpoint doesn't use HTTP request body parameters.

## Response Elements

Name

|

Type

|

Description  
  
||  
  
clusterName

|

string

|

Label that identifies the cluster into which you loaded the sample dataset.  
  
completeDate

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the dataset load job
completed.  
  
createDate

|

string

|

Timestamp in ISO 8601 date and time format in UTC when you created the dataset
load job.  
  
errorMessage

|

string

|

Description of any issue that arose in loading the data. This endpoint returns
`null` if **state** has a value other than **FAILED**.  
  
id

|

string

|

Unique 24-hexadecimal string that identifies this sample dataset.  
  
state

|

string

|

Condition in which the loading dataset currently exists.

Allowable values include **WORKING** , **COMPLETED** , and **FAILED**  
  
## Example Request

    
    
    curl --user "{PUBLIC-KEY}:{PRIVATE-KEY}" \  
      
         --digest \  
         --header "Content-Type: application/json" \  
         --include \  
         --request GET "https://cloud.mongodb.com/api/atlas/v1.0/groups/{GROUP-ID}/sampleDatasetLoad/{SAMPLE-DATASET-ID}?pretty=true"  
  
## Example Response

    
    
    1| {  
    |  
    2|   "_id": "{SAMPLE-DATASET-ID}",  
    3|   "clusterName": "{CLUSTER-NAME}",  
    4|   "completeDate": "2021-03-26T16:51:34Z",  
    5|   "createDate": "2021-03-26T16:30:47Z",  
    6|   "errorMessage": null,  
    7|   "state": "COMPLETED"  
    8| }  
  
What is MongoDB Atlas? →

