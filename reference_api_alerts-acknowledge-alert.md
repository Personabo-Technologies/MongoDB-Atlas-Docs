Docs Home → Launch & Manage MongoDB → MongoDB Atlas

# Acknowledge an Alert

Share Feedback

On this page

  * Syntax
  * Request Path Parameters
  * Request Query Parameters
  * Request Body Parameters
  * Response Elements
  * Serverless Measurements
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

`https://cloud.mongodb.com/api/atlas/v1.0`

The Atlas Administration API authenticates using HTTP Digest Authentication.
Provide a programmatic API public key and corresponding private key as the
username and password when constructing the HTTP request. To learn how to
configure API access for an Atlas project, see Get Started with the Atlas
Administration API.

## Syntax

    
    
    PATCH /groups/{GROUP-ID}/alerts/{ALERT-ID}  
      
  
### Request Path Parameters

Parameter

|

Required/Optional

|

Description  
  
||  
  
`GROUP-ID`

|

Required

|

Project identifier.  
  
`ALERT-ID`

|

Required

|

Alert identifier.  
  
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

Field

|

Required/Optional

|

Description  
  
||  
  
`acknowledgedUntil`

|

Required.

To acknowledge an alert "forever", set the field value to 100 years in the
future.

To unacknowledge a previously acknowledged alert, set the field value to the
past.

|

The page to return.  
  
`acknowledgementComment`

|

Optional.

|

If you add a comment, Atlas displays the comment next to the message that the
alert has been acknowledged.  
  
## Response Elements

The fields in the return document depend on the alert type:

Name

|

Type

|

Description  
  
||  
  
`acknowledgedUntil`

|

string

|

Timestamp in ISO 8601 date and time format in UTC through which the alert has
been acknowledged. Returned if the alert has been acknowledged.  
  
`acknowledgementComment`

|

string

|

Comment left by the user who acknowledged the alert. Returned if the alert has
been acknowledged.  
  
`acknowledgingUsername`

|

string

|

Username of the user who acknowledged the alert. Returned if the alert has
been acknowledged.  
  
`alertConfigId`

|

string

|

Unique identifier of the alert configuration that triggered this alert.  
  
`clusterName`

|

string

|

Name the cluster to which this alert applies.  
  
`created`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the alert was opened.  
  
`currentValue`

|

object

|

Current value of the metric that triggered the alert.  
  
`currentValue.number`

|

number

|

Value.  
  
`currentValue.units`

|

string

|

Units for the value. Possible units are:

  * `RAW`

  * `BITS`

  * `BYTES`

  * `KILOBITS`

  * `KILOBYTES`

  * `MEGABITS`

  * `MEGABYTES`

  * `GIGABITS`

  * `GIGABYTES`

  * `TERABYTES`

  * `PETABYTES`

  * `NANOSECONDS`

  * `MILLISECONDS`

  * `SECONDS`

  * `MINUTES`

  * `HOURS`

  * `MILLION_MINUTES`

  * `DAYS`

  * `RPU`

  * `THOUSAND_RPU`

  * `MILLION_RPU`

  * `WPU`

  * `THOUSAND_WPU`

  * `MILLION_WPU`

  
  
`eventTypeName`

|

string

|

Human-readable label that indicates the type of event.  
  
`id`

|

string

|

Unique identifier for the alert.  
  
`groupId`

|

string

|

Unique identifier of the project that this alert was opened for.  
  
`hostnameAndPort`

|

string

|

Hostname and port of the host to which the alert applies.  
  
`lastNotified`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the last notification
was sent for this alert. Returned if notifications have been sent.  
  
`metricName`

|

string

|

Name of the metric whose value went outside the threshold.

To learn more about the available metrics, see Host Metrics.

## Note

If you set `eventTypeName` to `OUTSIDE_SERVERLESS_METRIC_THRESHOLD`, you can
specify only metrics available for serverless. To learn more, see Serverless
Measurements.  
  
`replicaSetName`

|

string

|

Name of the replica set, if applicable.  
  
`resolved`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the alert was closed.
Returned if `"status" : "CLOSED"`.  
  
`status`

|

string

|

Current state of the alert. Possible values are:

  * `TRACKING`

Alert condition exists but hasn't persisted beyond the defined notification
delay.

## Tip

### See also:

Request Query Parameters.

  * `OPEN`

  * `CLOSED`

  * `CANCELLED`

  
  
`updated`

|

string

|

Timestamp in ISO 8601 date and time format in UTC when the alert was last
updated.  
  
### Serverless Measurements

Metric Name

|

Description  
  
|  
  
`SERVERLESS_CONNECTIONS`

|

Number of active connections to the serverless instance meets the specified
average.  
  
`SERVERLESS_CONNECTIONS_PERCENT`

|

Number of open connections to the serverless instance exceeds the specified
percentage threshold.  
  
`SERVERLESS_DATA_SIZE_TOTAL`

|

Approximate size of all documents (and their paddings) meets the specified
threshold.  
  
`SERVERLESS_NETWORK_BYTES_IN`

|

Number of bytes sent _to_ MongoDB meets the specified threshold.  
  
`SERVERLESS_NETWORK_BYTES_OUT`

|

Number of bytes sent _from_ MongoDB meets the specified threshold.  
  
`SERVERLESS_NETWORK_NUM_REQUESTS`

|

Number of requests sent to MongoDB meets the specified average.  
  
`SERVERLESS_OPCOUNTER_CMD`

|

Rate of commands performed meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_DELETE`

|

Rate of deletes meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_GETMORE`

|

Rate of `getmore` operations to retrieve the next cursor batch meets the
specified threshold.  
  
`SERVERLESS_OPCOUNTER_INSERT`

|

Rate of inserts meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_QUERY`

|

Rate of queries meets the specified threshold.  
  
`SERVERLESS_OPCOUNTER_UPDATE`

|

Rate of updates meets the specified threshold.  
  
`SERVERLESS_TOTAL_READ_UNITS`

|

Total read units meet the specified threshold.  
  
`SERVERLESS_TOTAL_WRITE_UNITS`

|

Total write units meet the specified threshold.  
  
## Example Request

    
    
    curl -u "{PUBLIC-KEY}:{PRIVATE-KEY}" -H "Content-Type: application/json" --digest -X PATCH "https://cloud.mongodb.com/api/atlas/v1.0/groups/535683b3794d371327b/alerts/524dc45ee4b835ff81ec2a" --data '  
      
    {  
      "acknowledgedUntil" : "2016-10-01T00:00:00-0400",  
      "acknowledgementComment" : "This is normal. Please ignore."  
    }'  
  
## Example Response

    
    
    {  
      
      "id" : "524dc45ee4b835ff81ec2a",  
      "groupId" : "535683b3794d371327b",  
      "eventTypeName" : "OUTSIDE_METRIC_THRESHOLD",  
      "status" : "OPEN",  
      "acknowledgedUntil" : "2016-10-01T04:00:00Z",  
      "acknowledgementComment" : "This is normal. Please ignore.",  
      "acknowledgingUsername" : "someuser@example.com",  
      "created" : "2016-08-23T20:28:14Z",  
      "updated" : "2016-08-23T20:33:14Z",  
      "lastNotified" : "2016-08-23T20:33:23Z",  
      "metricName" : "ASSERTS_REGULAR",  
      "currentValue" : {  
        "number" : 0.0,  
        "units" : "RAW"  
      },  
      "links" : [ ... ]  
    }  
  
What is MongoDB Atlas? →

